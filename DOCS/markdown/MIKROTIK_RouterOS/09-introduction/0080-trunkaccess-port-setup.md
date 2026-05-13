## Trunk/Access port setup 

Below you can find a very common diagram for a very typical type of setup that consists of a trunk port and multiple access ports: 

525 

**==> picture [504 x 224] intentionally omitted <==**

This setup is very common since it gives the possibility to divide your network into multiple segments while using a single switch and maybe a single router, such a requirement is very common for companies that want to separate multiple departments. With VLANs you can use different DHCP Servers, which can give out an IP address from a different subnet based on the VLAN ID, which makes creating Firewall rules and QoS a lot easier. 

In such a setup you would connect some generic devices like Desktop PCs to ether2 and ether3 , these can be considered as workstations and they generally only use untagged traffic (it is possible to force a VLAN tag for all traffic that is sent out a generic workstation, though it is not very common). To isolate some workstations from other workstations you must add a VLAN tag to all packets that enter ether2 or ether3 , but to decide what VLAN ID should the packet get, you need to use a concept called Port-based VLANs . In this concept, packets get a VLAN tag with a VLAN ID based on the bridge port to which the device is connected. For example, in this setup the device on ether2 will get a VLAN tag with VLAN20 and the device on ether3 will get a VLAN tag with VLAN30 , this concept is very scalable as long as you have enough bridge ports. This should give you the understanding that traffic between the bridge and devices behind ether2/ether3 is untagged (since there is no VLAN tag, hence the name). 

When we have determined our untagged ports, we can now determine our tagged ports. Tagged ports are going to be the trunk ports (the port, that carries multiple VLANs) and usually, this port is connected to a router or another switch/bridge, you can have multiple trunk ports as well. Tagged ports are always carrying packets with a VLAN tag (hence the name) and you must ALWAYS specify the tagged ports for each VLAN ID you want this port to forward. It is possible that a port is a tagged port for one VLAN ID and the same port is an untagged port for a different VLAN ID, but this is for a different type of setup (Hybrid port setup). 

A special note must be added for the PVID property. This property should be used on access ports, but it can be used for trunk ports as well (in Hybrid port setup). By using the PVID property you are adding a new VLAN tag with a VLAN ID that is specified in the PVID to all UNTAGGED packets that are received on that specific bridge port. The PVID does not have any effect on tagged packets, this means that, for example, if a packet with a VLAN tag of VL AN40 is received on ether2 that has `PVID=20` , then the VLAN tag is NOT changed and forwarding will depend on the entries from the bridge VLAN table. 

To configure the trunk/access port setup, you need to first create a bridge: 

```
/interface bridge
add name=bridge1
```

**==> picture [13 x 13] intentionally omitted <==**

Don't enable VLAN filtering yet as you might get locked out from the device because of the lack of management access, which is configured at the end. 

Add the bridge ports and specify PVID for each access port: 

```
/interface bridge port
add bridge=bridge1 interface=ether1
add bridge=bridge1 interface=ether2 pvid=20
add bridge=bridge1 interface=ether3 pvid=30
```

526 

**==> picture [13 x 13] intentionally omitted <==**

PVID has no effect until VLAN filtering is enabled. 

Add appropriate entries in the bridge VLAN table:
