## RDMA over Converged Ethernet (RoCE) 

RoCE allows you to directly access memory on remote storage systems using Ethernet networks without involving the host CPU. This capability significantly reduces latency and CPU overhead, making RoCE ideal for high-performance computing and data center environments. RoCE also enables a converged network, where various services (such as data storage, networking, and multimedia) run over a single Ethernet infrastructure. This simplifies network management and reduces the cost and complexity of maintaining separate networks. 

RoCE achieves this through the use of ECN and PFC mechanisms. These features help prevent network congestion and packet loss, ensuring reliable, lossless communication. See the device feature table for compatible switches. Although switches can support RoCE environments, the end hosts must also be compatible with the RoCE protocol and equipped with RDMA-capable network interface cards (NICs). 

There are two main versions of RoCE. RoCEv1 operates as an Ethernet link layer protocol and uses Ethertype 0x8915. RoCEv2 works over standard IP networks, using UDP destination port number 4791. ECN bits in the IP header are marked to signal network congestion, and a Congestion Notification Packet (CNP) is used to acknowledge congestion to the sender. For traffic prioritization, DSCP 26 is used for RoCEv2 traffic, while DSCP 48 for CNPs. 

The following example can be used for lossless RoCEv2 with PFC and ECN and it assumes that the switch is using its default configuration, which includes a default "bridge" interface and all Ethernet interfaces added as bridge ports. The minimal recommended RouterOS version is 7.17. 

First, configure additional profiles. Non-RoCE traffic will be assigned to already existing "default" profile with traffic-class 1, RoCEv2 to traffic-class 3, and CNP to traffic-class 6. 

462 

```
/interface ethernet switch qos profile
add name=roce traffic-class=3
add name=cnp traffic-class=6
```

Create a QoS mapping to match QoS profiles based on DSCP values. 

```
/interface ethernet switch qos map ip
add dscp=26 profile=roce
add dscp=48 profile=cnp
```

Configure hardware queues and scheduler. We are using ETS ( `schedule=high-priority-group` ) for traffic-class 1 and traffic-class 3 with 50% bandwith assigment each ( `weight=1` ), and strict priority scheduling for traffic-class 6. Additionally, configure a separate shared memory pool ( `sharedpool-index=1` ) for lossless traffic in traffic-class 3 and enable ECN ( `ecn=yes` ) to mark IP packets in the switch that experience congestion. 

```
/interface ethernet switch qos tx-manager queue
set 1 schedule=high-priority-group weight=1
set 3 schedule=high-priority-group weight=1 shared-pool-index=1 ecn=yes
set 6 schedule=strict-priority
```

**==> picture [13 x 13] intentionally omitted <==**

Although using `schedule=low-priority-group` allows you to create separate ETS scheduling and bandwidth allocation for a different set of traffic-classes, it is not recommended to use this setting together with `lldp-dcbx=yes` . The reason is that the ETS Configuration /Recommendation TLVs are designed to handle a single bandwidth allocation across traffic classes, thus `schedule=high-priority-group` should be used instead. 

Configure PFC profile for traffic-class 3 to ensure a lossless environment for RoCEv2 traffic. 

```
/interface ethernet switch qos priority-flow-control
add name=pfc-tc3 rx=yes traffic-class=3 tx=yes
```

Set Layer3 trust mode ( `trust-l3=keep` ) on switch ports where RoCEv2 traffic is expected, set PFC ( `pfc=pfc-tc3` ) and egress-rate for queue3 to comply with PFC requirements ( `egress-rate-queue3=10.0Gbps` ). In this example, 10Gbps SFP+ interfaces are used, and the egress rate can be set to match the physical speed of the interface. Change this property depending on your interface speeds. 

```
/interface ethernet switch qos port
```

```
set sfp-sfpplus1 egress-rate-queue3=10.0Gbps pfc=pfc-tc3 trust-l3=keep
set sfp-sfpplus2 egress-rate-queue3=10.0Gbps pfc=pfc-tc3 trust-l3=keep
set sfp-sfpplus3 egress-rate-queue3=10.0Gbps pfc=pfc-tc3 trust-l3=keep
set sfp-sfpplus4 egress-rate-queue3=10.0Gbps pfc=pfc-tc3 trust-l3=keep
```
