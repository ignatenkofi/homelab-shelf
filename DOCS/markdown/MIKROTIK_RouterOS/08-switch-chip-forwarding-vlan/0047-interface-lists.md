## Interface Lists 

It is impossible to use interface lists directly to control `l3-hw-offloading` because an interface list may contain virtual interfaces (such as VLAN) while the `l3-hw-offloading` setting must be applied to physical switch ports only. For example, if there are two VLAN interfaces (vlan20 and vlan30) running on the same switch port (trunk port), it is impossible to enable hardware routing on vlan20 but keep it disabled on vlan30. 

However, an interface list may be used as a port selector. The following example demonstrates how to enable hardware routing on LAN ports (ports that belong to the "LAN" interface list) and disable it on WAN ports: 

```
:foreach i in=[/interface/list/member/find where list=LAN] do={
```

```
    /interface/ethernet/switch/port set [/interface/list/member/get $i interface] l3-hw-offloading=yes
}
```

```
:foreach i in=[/interface/list/member/find where list=WAN] do={
```

```
    /interface/ethernet/switch/port set [/interface/list/member/get $i interface] l3-hw-offloading=no
}
```

Please take into account that since interface lists are not directly used in hardware routing control., modifying the interface list also does not automatically reflect in l3hw changes . For instance, adding a switch port to the "LAN" interface list does not automatically enable `l3-hw-offloading` on it. The user has to rerun the above script to apply the changes. 

MTU 

439 

The hardware supports up to 8 MTU profiles, meaning that the user can set up to 8 different MTU values for interfaces: the default 1500 + seven custom ones. 

It is recommended to disable `l3-hw-offloading` while changing the MTU/L2MTU values on the interfaces. MTU Change Example 

```
/interface/ethernet/switch set 0 l3-hw-offloading=no
/interface set sfp-sfpplus1 mtu=9000 l2mtu=9022
/interface set sfp-sfpplus2 mtu=9000 l2mtu=9022
/interface set sfp-sfpplus3 mtu=10000 l2mtu=10022
/interface/ethernet/switch set 0 l3-hw-offloading=yes
```
