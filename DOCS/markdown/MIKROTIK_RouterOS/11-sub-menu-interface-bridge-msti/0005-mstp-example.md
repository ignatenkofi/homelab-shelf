## MSTP example 

Let's say that we need to design topology and configure MSTP in a way that VLAN 10,20 will be forwarded in one path, but VLAN 30,40 will be forwarded in a different path, while all other VLAN IDs will be forwarded in one of those paths. This can easily be done by setting up MST Instances and assigning port path costs, below you can find a network topology that needs to do load balancing per VLAN group with 3 separate regions as an example: 

617 

**==> picture [505 x 233] intentionally omitted <==**

The topology of an MSTP-enabled network with load balancing per VLAN group 

Start by adding each interface to a bridge, initially, you should create a (R)STP bridge without VLAN filtering enabled, this is to prevent losing access to the CPU. Each device in this example is named by the region that it is in (Rx) and a device number (_x). For larger networks configuring MSTP can be confusing because of the number of links and devices, we recommend using The Dude to monitor and design a network topology. 

Use the following commands on R1_1 , R1_3 , R2_1 , R2_3 , R3_1 , R3_3 : 

```
/interface bridge
```

```
add name=bridge protocol-mode=rstp vlan-filtering=no
/interface bridge port
add bridge=bridge interface=ether1
add bridge=bridge interface=ether2
add bridge=bridge interface=ether3
add bridge=bridge interface=ether4
```

Use the following commands on R1_2 , R2_2 , R3_2 : 

```
/interface bridge
add name=bridge protocol-mode=rstp vlan-filtering=no
/interface bridge port
add bridge=bridge interface=ether1
add bridge=bridge interface=ether2
```

Make sure you allow the required VLAN IDs on these devices, here we will consider that each device will receive tagged traffic that needs to be load balanced per VLAN group, use these commands on R1_1 , R1_3 , R2_1 , R2_3 , R3_1 , R3_3 : 

```
/interface bridge vlan
```

```
add bridge=bridge tagged=ether1,ether2,ether3,ether4 vlan-ids=10,20,30,40
```

Use the following commands on R1_2 , R2_2 , R3_2 : 

```
/interface bridge vlan
```

```
add bridge=bridge tagged=ether1,ether2 vlan-ids=10,20,30,40
```

**==> picture [13 x 13] intentionally omitted <==**

Make sure you add all the needed VLAN IDs and ports to the bridge VLAN table, otherwise, your device will not forward all required VLANs, and /or you will lose access to the device. 

618 

We need to assign a region name for each bridge that we want to be in a single MSTP region, you can also specify the region revision, but it is optional, though they need to match. In this example, if all bridges will have the same region name, then they will all be in a single MSTP bridge. In this case, we want to separate a group of 3 bridges in a different MSTP region to do load balancing per VLAN group and to create diversity and scalability. 

Set the appropriate region name (and region revision) for each bridge, and use the following commands on each device ( change the region name! )
