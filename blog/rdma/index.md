# RDMA

date: 2026-05-05

> Basic Knowledge of RDMA

# RDMA
## 1.1 the basic principle and advantage of RDMA - Why ethernet socket communcation copys data from user space to kernel space

### the process of Ethernet Communcation
![Process](https://www.cs.dartmouth.edu/~cs50/Lectures/sockets/ethernetccp.jpg)

首先在用户态， 
由用户发起调用，该调用将从用户态被拷贝到内核态
为什么要拷贝？ -- 稍后说明

在内核态中，由cpu负责，添加报文头，数据封装，添加校验信息之类的操作
加载完成后，以太网卡通过DMA，读取内核态的数据，拷贝到网卡上
再由发送端网卡发送给接收端网卡

接收端接收到数据后，拷贝到接收端的内核态
在内核态中，由cpu完成数据的解包，数据的校验之类的工作

最后拷贝到用户空间，供用户使用


所以缺点一目了然：
1. 用户态内核态切换开销
2. 用户态和内核态之间数据拷贝
3. cpu参与，负载很高

为什么需要拷贝
网卡没有映射机制，所以没发读取虚拟地址，因此，只能要求DMA能懂的地址
用户虚拟地址
    ↓
找到对应的物理页
    ↓
pin 住这些页，防止被换出/移动/释放
    ↓
建立 DMA mapping
    ↓
得到 DMA address / IOVA
    ↓
把 DMA address 写给设备

因此，需要内核的参与

![RDMA](https://www.eizorugged.com/wp-content/uploads/2024/09/Figure-1_RoCe-2048x735.jpg)



RDMA 优点
1. 数据传输时没有系统调用，不存在两态切换
2. 零拷贝
3. 数据包的封装和解析，由NiC完成，降低CPU负载



基本逻辑是 -- 
cpu在内核态需要完成的操作：
查用户地址是否合法
访问页表 / 找到物理页
pin 住页面
配置 IOMMU 映射
调用 DMA mapping API
操作网卡 descriptor / MMIO 寄存器

// 其实
pin 住页面，配置 IOMMU 映射，调用 DMA mapping API
这三步是一直重复的动作，我是否可以pin住一段逻辑地址，对应的物理地址，对应的dma地址，然后建立dma和逻辑地址的映射，这样，我每次只需要检查用户程序地址是否合法（或许不用，因为只要用户地址不处于映射区间就不合法），以及操作网卡就可以了
因为中间的部分
访问页表 / 找到物理页
pin 住页面
配置 IOMMU 映射
调用 DMA mapping API
全部被一步搞定了


--- zero copy 
RDMA  -- lkey/rkey

RDMA具体结构 
[RDMA基本元素](https://blog.csdn.net/lianghuaju/article/details/140075613)

