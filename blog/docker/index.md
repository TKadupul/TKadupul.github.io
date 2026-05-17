# Docker

date: 2026-05-15

> Basic Knowledge of Docker


# Docker
## 虚拟化


将一组物理平台，抽象为多组彼此之间互相隔离的计算平台，每一个计算平台都应该拥有冯氏基本部件中的所有设备


### CPU的虚拟化
CPU从一开始就是虚拟化的，通过time-sharing技术，每个进程都假设自己拥有完整的CPU
虽然操作方法类似，虚拟机要麻烦很多
首先，每个机器都认为自己拥有内核态和用户态，而内核指令默认可以控制所有的系统调用，也就是说，两台虚拟机之间存在争抢：
VMWare是架设在已有的操作系统之上的-Host
每个虚拟机我们称之为Guest
Guest是一个进程而已，是一个软件设备，受Host控制
那么，一个Guest上的系统调用，需要：先经过自己虚拟机的内核，再去Host的内核

出于安全考虑，我们需要host的内核运行在环0上，不能让Guest鸠占鹊巢，
可是如果Guest的内核运行在环3上，内核指令没办法使用，因为内核指令都是按照可以直接操控硬件被设计的
所以，每个guest的cpu，实际上是由host的一个进程甚至一个线程模拟出来的cpu
该cpu也有特权指令，只不过是假的
如果真的有特权指令，将会被拦截到host中执行

因此，基于这种方式实现的虚拟化，性能是非常低的
因为特权指令需要两次调度
（BT）另外，在这种情况下，异构的cpu架构是可以被接受的，只不过中间的翻译开销十分惊人
所以，如果Guest和Host的cpu架构相同，那么Guest的用户指令是完全能够直接被运行在hostcpu上的，所以速度相差无几


CPU：
    模拟；emulation.   --- 模拟ring0，1，2，3
    虚拟：virtualization ---模拟ring0
    full virtualization -- BT（soft）/HVM（Hardware）




如何提升性能呢？
硬件虚拟化
增加了一环，环-1
host内核运行在环-1上，特权指令环
Gust内核运行在环0上
HVM …… Hardware VM 
环0 - 环-1 的转换由硬件完成，所以提升性能较大



Paravirtualization   半虚拟化 
让Guest意识到自己是Guest，自己主动去找Host的内核
Host 改个名字 -- VMware Minitor -- Hypervisor







主机虚拟化：
Type-I : hardware - hypervisior - VM
Type II: HostOS - VMM - VM

确实能够实现再一组硬件平台上所谓“跨平台”的互联，不过带给我们的内核开销是巨大的
很多时候，我们创建虚拟机的目的仅仅是为了实现简单的/几个生产应用而已，代价很大
所以需要减少中间层

