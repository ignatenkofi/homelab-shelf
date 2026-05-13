## `/interface bridge` 

```
set bridge region-name=Rx region-revision=1
```

After we have created 3 different MSTP regions, we need to decide which device is going to be a regional root for each VLAN group. For consistency, we are going to set the first device (_1) in each region as the regional root for VLAN 10,20 and the third device (_3) in each region as the regional root for VLAN 30,40. This can be done by creating an MST Instance for each VLAN group and assigning a bridge priority to it. The MST Instance identifier is only relevant inside an MSTP region, outside an MSTP region these identifiers can be different and mapped to a different VLAN group. 

Use the following commands on R1_1 , R2_1 , R3_1 : 

```
/interface bridge msti
```

```
add bridge=bridge identifier=1 priority=0x1000 vlan-mapping=10,20
add bridge=bridge identifier=2 priority=0x3000 vlan-mapping=30,40
```

Use the following commands on R1_3 , R2_3 , R3_3 : 

```
/interface bridge msti
```

```
add bridge=bridge identifier=1 priority=0x3000 vlan-mapping=10,20
add bridge=bridge identifier=2 priority=0x1000 vlan-mapping=30,40
```

Use the following commands on R1_2 , R2_2 , R3_2 : 

```
/interface bridge msti
```

```
add bridge=bridge identifier=1 priority=0x2000 vlan-mapping=10,20
add bridge=bridge identifier=2 priority=0x2000 vlan-mapping=30,40
```

Now we need to override the port `path-cost` and/or port priority for each MST Instance. This can be done by adding an MST-Override entry for each port and each MST Instance. To achieve that for a certain MST Instance the traffic flow path is different, we simply need to make sure that the port path cost and/or priority is larger. We can either increase the port path cost or decrease the port path cost to ports that are facing toward the regional root bridge. It doesn't matter if you increase or decrease all values, it is important that in the end, one port's path cost is larger than the other's. 

Use the following commands on R1_1 , R2_1 , R3_1 : 

```
/interface bridge port mst-override
add identifier=2 interface=ether1 internal-path-cost=5
add identifier=2 interface=ether2 internal-path-cost=15
```

Use the following commands on R1_2 , R2_2 , R3_2 : 

```
/interface bridge port mst-override
```

```
add identifier=1 interface=ether1 internal-path-cost=5
add identifier=2 interface=ether2 internal-path-cost=9
```

Use the following commands on R1_3 , R2_3 , R3_3 : 

```
/interface bridge port mst-override
```

```
add identifier=1 interface=ether2 internal-path-cost=5
add identifier=1 interface=ether3 internal-path-cost=9
```

619 

In this case for VLAN 10,20 to reach the third device from the first device, it would choose between ether1 and ether2, one port will be blocked and set as an alternate port, and ether1 will have path cost as `5+9=14` and ether2 will have path cost as `10` , ether2 will be elected as the root port for MSTI1 on the third device. In case for VLAN 30,40 to reach the first device from the third device, ether1 will have path cost as `5+9=14` and ether2 will have path cost as `15` , ether1 will be elected as the root port for MSTI2 on the third device. 

Now we can configure the root ports for MSTI0 , which will fall under all VLANs that are not assigned to a specific MST Instance, like in our example VLAN 10,20, and VLAN 30,40. To configure this special MST Instance, you will need to specify `internal-path-cost` to a bridge port. This value is only relevant to MSTP regions, it does not have any effect outside an MSTP region. In this example will choose that all unknown VLANs will be forwarded over the same path as VLAN 30,40, we will simply increase the path cost on one of the ports. 

Use the following commands on R1_3 , R2_3 , R3_3 : 

```
/interface bridge port
```

```
set [find where interface=ether3] internal-path-cost=25
```

At this point, a single region MSTP can be considered as configured, and in general, MSTP is fully functional. It is highly recommended to configure the CIST part, but for testing purposes, it can be left with the default values. Before doing any tests, you need to enable MSTP on all bridges. 

Use the following commands on all devices: 

```
/interface bridge
```

```
set bridge protocol-mode=mstp vlan-filtering=yes
```

When MSTP regions have been configured, you can check if they are properly configured by forwarding traffic, for example, send tagged traffic from the first device to the third device and change the VLAN ID for the tagged traffic to observe different paths based on VLAN ID. When this is working as expected, then you can continue to configure CIST related parameters to elect a CIST root bridge and CIST root ports. For consistency we will choose the first device in the first region to be the CIST root bridge and to ensure consistency in case of failure we can set a higher priority to all other bridges. 

Use the following commands on R1_1: 

```
/interface bridge
set bridge priority=0x1000
```

Use the following commands on R1_2 : 

```
/interface bridge
set bridge priority=0x2000
```

... 

Use the following commands on R3_3 : 

```
/interface bridge
set bridge priority=0x9000
```

We also need to elect a root port on each bridge, for simplicity we will choose the port that is closest to Ŗ1_1 as the root port and has the least hops. At this point, the procedure to elect root ports is the same as the procedure in (R)STP. 

Use the following commands on R3_3: 

```
/interface bridge port
set [find where interface=ether2] path-cost=30
set [find where interface=ether3] path-cost=40
set [find where interface=ether4] path-cost=20
```

Use the following commands on R1_3 and R2_3: 

620 

```
/interface bridge port
set [find where interface=ether2] path-cost=20
set [find where interface=ether3] path-cost=30
```

Use the following commands on R1_2 : 

```
/interface bridge port
set [find where interface=ether1] path-cost=30
```

621
