## OSPF Configuration 

OSPFv3 and OSPFv2 are now merged into one single menu `/routing ospf` . At the time of writing this article, there are no default instances and areas. To start both OSPFv2 and OSPF v3 instances, first, you need to create an instance for each and then add an area to the instance. 

```
/routing ospf instance
add name=v2inst version=2 router-id=1.2.3.4
add name=v3inst version=3 router-id=1.2.3.4
/routing ospf area
add name=backbone_v2 area-id=0.0.0.0 instance=v2inst
add name=backbone_v3 area-id=0.0.0.0 instance=v3inst
```

At this point, you are ready to start OSPF on the network interface. In the case of IPv6, you add either interface on which you want to run OSPF (the same as ROSv6) or the IPv6 network. In the second case, OSPF will automatically detect the interface. Here are some interface configuration examples: 

1075 

```
/routing ospf interface-template
```

```
add network=192.168.0.0/24 area=backbone_v2
add network=2001:db8::/64 area=backbone_v3
add network=ether1 area=backbone_v3
```

ROSv7 uses templates to match the interface against the template and apply configuration from the matched template.  OSPF menus `interface` and `ne ighbor` contains read-only entries purely for status monitoring. 

~~All route distribution control is now done purely with routing filter select, no more redistribution knobs in the instance~~ (Since the v7.1beta7 redistribution knob is back, you still need to use routing filters to set route costs and type if necessary). This gives greater flexibility on what routes from which protocols you want to redistribute. 

For example, let's say you want to redistribute only static IPv4 routes from the 192.168.0.0/16 network range. 

```
/routing ospf instance
```

```
set backbone_v2 out-filter-chain=ospf_out redistribute=static
```

```
/routing filter rule add chain=ospf_out rule="if (dst in 192.168.0.0/16) {accept}"
```

**==> picture [13 x 13] intentionally omitted <==**

The default action of the routing filter chain is "reject"
