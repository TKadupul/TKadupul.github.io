# Example Paper Note

date: 2026-05-02

> Test


# Preventing Network Bottlenecks: 
# Accelerating Datacenter Services with Hotspot-Aware 
# Placement for Compute and Storage

/ 什么是hotspot
Datacenter network hotspots, defined as links with persistently high utilization, can lead to performance bottlenecks.
网络里的局部热点拥塞点，也就是某一小块网络资源长期或频繁地特别忙，利用率很高，因而拖慢经过它的流量。
类似地图，红色的部分就是拥挤严重的路段
不过，在这里指的是，经常容易堵、并且会持续一段时间的路段

/ 什么是ToR Switch
Top-of-rack switching is a network architecture design in which computing equipment like servers, appliances and other switches located within the same or adjacent rack are connected to an in-rack network switch. The in-rack network switch, in turn, is connected to aggregation switches via fiber optic cables.
服务器
  ↓
ToR switch（机架顶端交换机）
  ↓
Aggregation / Leaf switch（上层交换机）
  ↓
Core / Spine switch（更高层骨干交换机）

## 本文解决的问题：数据中心调度算法非常不智能，导致网络拥塞问题严重。本文通过hotspot-aware调度算法，大幅度降低了数据中心的拥塞程度



在理想的情况下，数据中心应该给所有的应用程序一种假象：不论我的组件在网络中哪个位置存放，我都应该能够得到一个高吞吐量的不受限制的网络带宽
以前的解决办法通常是：
* topology design：把网络拓扑本身设计得更强，比如结构更规整、带宽更高、路径更多
* traffic engineering：更聪明地安排流量怎么走，尽量避开拥堵

/ non-blocking bandwidth provisioning 无阻塞带宽配置 -- 把网络带宽配到“怎么同时发都不会堵”的程度
/ statistical multiplexing 按概率共享 --  不是给每个人都修一条独享高速公路，而是修一条大家共用的路，因为大多数时候大家不会同时把路占满。
/ oversubscription ratio 过订阅 -- ToR downlink bandwidth / uplink bandwidth
 Due to the high cost of non-blocking bandwidth provisioning, statistical multiplexing is employed, resulting in an oversubscription ratio – the ratio of ToR downlink to uplink bandwidth.
意思是-从一开始上传带宽就被确定好了，也就是说，最开始就已经被设定了一个最大值


/ 怎样实现：
直接修改很有难度，要修改文件系统/调度器
但是有两个点可以利用：
ToR利用率超过75%以上才会明显有影响
数据中心平均的ToR利用率很低，所以有很多ToR利用率低于75%

/ Architecture


Rack内服务器 - ToR - Aggregation Switches - Aggregation Blocks/ Spine - DCNI - FBR - other DCNI/ WAN

/ Rack Type 
Disk Rack  - only ssd/hdd
Compute Rack - cpu/minimal local storage
Mixed Rack - both



Bigtable / QuerySys - Colossus / RamStore - D / Memory Host - HDD / SSD / Memory


/telemetry data from switches
用这些数据提供每条网络链路上5分钟的平均利用率 - 即带宽利用率

选用75%作为hotspot阈值，两个原因：
1、留取25%的空间，希望在维护，更新，故障期间尽量减少对程序的影响
2、当利用率超过75%时，本文应用会产生明显的延迟


分析数据：

* ToR - aggregation blocks  10 times than host-ToR
* ToR - aggregation blocks 2 times than DCNI
 
甚至有上下行的区分，所以，策略需要针对上下行都制定，而非一个


/ 现在服务器上的链路占用情况

* 只有1/3能够在一小时内结束
* 40%占用在1-12小时内结束
* 甚至有13%会持续1天到两周

需要对持续时间不同的链路作出不同的优化措施（分层优化）
在较短时间尺度上，也就是分钟级，可以采用响应式的任务迁移；在中等时间尺度上，也就是小时级，可以主动放置数据和网络密集型的长时间运行任务；在更长时间尺度上，也就是天级或更久，可以进行容量规划和重新配置资源。


/ 数据中心中，热点链路通常是什么链路
50%占用是mixed rack ，40%左右时 disk rack
也就是说，有存储参与的90%的rack都会变热

但是其实mixed rack上只有45%的变热情况和存储有关系
不过即使如此，变热的情况确实和存储的拥塞密不可分

！！！！
## What Causes ToR Hotspots
bandwidth demand-supply imbalance on racks,
and bandwidth-independent task/data placement by cluster
schedulers and distributed storage systems.

1、 数据中心一开始会设置好带宽，然后一成不变
可是应用会变，服务器会换，磁盘会升级，业务负载也会变化
这是在考虑性价比情况下搭建的数据中心内在的问题，这种问题不可避免

升级或替换一个 rack 上的少数服务器或磁盘比较容易，但升级 ToR 容量要困难得多。因为后者需要让该 ToR 下承载的所有计算和存储资源离线，并且可能还需要升级 aggregation block。

2、 不考虑带宽的调度决策
这是故意为之，因为无论过去还是现在，设计一个带宽感知的集群调度器和文件系统，同时还要满足性能、可靠性和资源利用率目标的调度器被视为非常困难
调度器通常认为，网络带宽是不受限制的

图7，job 的网络需求差异很大。

图8，网络密集型任务集中放置会让 ToR 更热。

图9，存储 rack 的带宽供给并不均衡。

/ several hotspot-related incidents
* Unintended capacity reduction causes ToR hotspots. -- In a specific instance, a software rollout issue during network maintenance caused a 50%
uplink capacity reduction on multiple ToRs.
* Unintended network imbalances from scheduling constraints -- Local rules can have global side effects.
* Colossus degraded reads exacerbate ToR hotspots -- Degraded reads

Colossus : 
Try to read the required chunk from its normal disk/server.

If the read is too slow, times out, or the server does not respond quickly enough,
treat that chunk as temporarily unavailable.

If the file is erasure-coded,
read other chunks in the stripe and reconstruct the missing one.


## Impact of Hotspots on Storage Systems

 will read it later ... 


 # Hotspot-Aware Placement

 / two hotspot-aware placement strategies:
* ToR-utilization aware task placement and migration (UTP) 
  takes ToR utilization into account
* ToR-capacity aware chunk placement (CCP) 
  takes the imbalance between ToR capacity and rack storage capacity into account 


/ Design
Borg can easily determine if placing a task on a server would over-run the server’s CPU resources
While it is harder to determine how placing a task on a server would impact the server’s ToR utilization





# Finally

Although from an engineering perspective, the change itself seems quite simple, it truly improves performance significantly. In my view, the authors identify many possible factors worth considering and turn them into a practical optimization. It is promising work, and maybe that is why it was accepted by NSDI, even though the paper is not very readable.

