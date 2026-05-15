# Empowering_Azure_Storage_with_RDMA

date: 2026-05-05

> Given the wide adoption of disaggregated storage in public clouds, networking is the key to enabling high performance and high reliability in a cloud storage service. In Azure, we choose Remote Direct Memory Access (RDMA) as our transport and aim to enable it for both storage frontend traffic (between compute virtual machines and storage clusters) and backend traffic (within a storage cluster) to fully realize its benefits. As compute and storage clusters may be located in different datacenters within an Azure region, we need to support RDMA at regional scale



# Empowering Azure Storage with RDMA
## Abstract
Seems like a very simple introduction which just tells that they set RDMA on the Azure, without any reason or further details
abbreviation: “Azure Storage depends heavily on the network, so we deployed RDMA at a very large scale. It was useful, but difficult because Azure’s infrastructure is huge and heterogeneous.”

## Introduction

* Failover -- Failure and take over


These are three datacenter networking terms that often appear together in RDMA papers.

* DCQCN

DCQCN = Data Center Quantized Congestion Notification
It is a congestion control mechanism for RoCE RDMA networks.
Very roughly:

Network is getting congested
        ↓
Switch marks packets with congestion signal
        ↓
Receiver notices it
        ↓
Sender reduces sending rate


* PFC

PFC = Priority Flow Control
It is an Ethernet flow-control mechanism. Its goal is to make the network almost lossless for certain priority classes of traffic.
In normal Ethernet, if a switch buffer is full, packets may be dropped.
With PFC:

Switch buffer is almost full
        ↓
Switch sends pause frame
        ↓
Upstream sender pauses that traffic priority
        ↓
Buffer avoids packet loss

* SONiC

SONiC = Software for Open Networking in the Cloud
It is an open-source network operating system originally developed by Microsoft for datacenter switches.
A switch is not just hardware. It also runs software to manage routing, forwarding rules, telemetry, configuration, and so on. SONiC is that software layer for many cloud switches.
In this paper, SONiC probably matters because Azure had to modify or configure the network infrastructure to support RDMA at large scale.
So:

Switch hardware
        ↓
Switch OS: SONiC
        ↓
Network features: routing, QoS, PFC, congestion control support, telemetry

* How they connect
In an RDMA-over-Ethernet datacenter, you may see this combination:

RoCE RDMA traffic
        ↓
PFC prevents packet loss
        ↓
DCQCN controls congestion
        ↓
SONiC configures/manages switches and network behavior

Very compressed explanation:

PFC  = prevents loss by pausing traffic
DCQCN = controls congestion by adjusting sending rate
SONiC = switch operating system used to manage/configure the datacenter network

For this paper, the most important pair is probably DCQCN + PFC.

RDMA wants a low-loss network. PFC tries to avoid loss, while DCQCN tries to avoid persistent congestion. They work together, but tuning them at Azure scale is hard.

/ A small mental model (interesting)
Borg is like the process scheduler / resource manager of the datacenter OS.
SONiC is like part of the network subsystem of the datacenter OS.


