## Multicast routing with static RP 

In the upcoming example, we'll be working with multiple PIM routers, as shown in the diagram below. PIM-SM uses shared trees and to make this work, we need to designate a specific node as the multicast root distribution point. In PIM, this router is called the Rendezvous Point, or RP. There are various methods for selecting an RP in PIM, such as the Bootstrap Router (BSR) method. However, for this example, we'll be using a straightforward approach known as static RP configuration. This means that the administrator can manually specify one or more RPs for specific multicast groups. 

**==> picture [504 x 410] intentionally omitted <==**

To get started, we'll need to configure IP addresses and set up unicast routing. In this example, we'll use OSPF to exchange routing information between the routers. See more details about OSFP. 

1089 

```
# R1 Rendezvous Point:
/interface bridge
add name=loopback
/ip address
add address=10.0.0.1 interface=loopback network=10.0.0.1
add address=10.0.1.1/24 interface=ether2 network=10.0.1.0
add address=10.0.2.1/24 interface=ether3 network=10.0.2.0
/routing ospf instance
add disabled=no name=ospf-instance-1 router-id=10.0.0.1
/routing ospf area
add disabled=no instance=ospf-instance-1 name=ospf-area-1
/routing ospf interface-template
add area=ospf-area-1 disabled=no interfaces=loopback,ether2,ether3
# R2:
/interface bridge
add name=loopback
/ip address
add address=10.0.0.2 interface=loopback network=10.0.0.2
add address=10.0.1.2/24 interface=ether1 network=10.0.1.0
add address=192.168.20.1/24 interface=ether12 network=192.168.20.0
/routing ospf instance
add disabled=no name=ospf-instance-1 router-id=10.0.0.2
/routing ospf area
add disabled=no instance=ospf-instance-1 name=ospf-area-1
/routing ospf interface-template
add area=ospf-area-1 disabled=no interfaces=loopback,ether1,ether12
# R3:
/interface bridge
add name=loopback
/ip address
add address=10.0.0.3 interface=loopback network=10.0.0.3
add address=10.0.2.3/24 interface=ether1 network=10.0.2.0
add address=192.168.30.1/24 interface=ether12 network=192.168.30.0
/routing ospf instance
add disabled=no name=ospf-instance-1 router-id=10.0.0.3
/routing ospf area
add disabled=no instance=ospf-instance-1 name=ospf-area-1
/routing ospf interface-template
add area=ospf-area-1 disabled=no interfaces=loopback,ether1,ether12
```

As in the previous example with a single router, we need to configure the PIM instance and add the necessary interfaces on all routers. 

```
# R1 Rendezvous Point:
/routing pimsm instance
add disabled=no name=pimsm-instance-1
/routing pimsm interface-template
add instance=pimsm-instance-1 interfaces=loopback,ether2,ether3
# R2:
/routing pimsm instance
add disabled=no name=pimsm-instance-1
/routing pimsm interface-template
add instance=pimsm-instance-1 interfaces=loopback,ether1,ether12
# R3:
/routing pimsm instance
add name=pimsm-instance-1
/routing pimsm interface-template
add instance=pimsm-instance-1 interfaces=loopback,ether1,ether12
```

Now, let's take a look at our PIM neighbors and their current statuses. On R1, there are two neighbors, while on R2 and R3, there's only one neighbor each. 

1090 

```
# R1 Rendezvous Point:
/routing pimsm neighbor print
Flags: R - DESIGNATED-ROUTER; J - JOIN-TRACKING
Columns: INSTANCE, ADDRESS, PRIORITY
#    INSTANCE          ADDRESS          PRIORITY
0 RJ pimsm-instance-1  10.0.1.2%ether2  1
1 RJ pimsm-instance-1  10.0.2.3%ether3  1
# R2:
/routing pimsm neighbor print
Flags: R - DESIGNATED-ROUTER; J - JOIN-TRACKING
Columns: INSTANCE, ADDRESS, PRIORITY
#    INSTANCE          ADDRESS          PRIORITY
0  J pimsm-instance-1  10.0.1.1%ether1  1
```

```
# R3:
/routing pimsm neighbor print
Flags: J - JOIN-TRACKING
Columns: INSTANCE, ADDRESS, PRIORITY
#   INSTANCE          ADDRESS          PRIORITY
0 J pimsm-instance-1  10.0.2.1%ether1  1
```

Finally, we will select one router to act as our Rendezvous Point (RP). We will configure the R1 loopback IP address on all PIM routers. It's important to ensure that each router has the correct routing information to reach the R1 loopback address. 

```
# R1 Rendezvous Point:
/routing pimsm static-rp
add address=10.0.0.1 instance=pimsm-instance-1
# R2:
/routing pimsm static-rp
add address=10.0.0.1 instance=pimsm-instance-1
# R3:
/routing pimsm static-rp
add address=10.0.0.1 instance=pimsm-instance-1
```
