## `/interface bonding` 

```
add mode=802.3ad name=bond1 slaves=sfp-sfpplus1,sfp-sfpplus2
add mode=802.3ad name=bond2 slaves=sfp-sfpplus3,sfp-sfpplus4
/interface bridge port-extender
set control-ports=bond1,bond2 switch=switch1
```

Last, configure the Port Extender 2 device - create a bonding interface and enable PE. Additionally, configure one or multiple `excluded-ports` if necessary. In this example, all switch ports will be extended. 

```
/interface bonding
add mode=802.3ad name=bond1 slaves=sfp-sfpplus1,sfp-sfpplus2
/interface bridge port-extender
set control-ports=bond1 switch=switch1
```

Now the CRS317-1G-16S+ device has extended its ports with additional 48 Gigabit Ethernet ports and packet forwarding can be achieved between all bridged ports. 

Use the `monitor` command in the device menu to see the PE device connection path. Also, use `print` command in the port menu to see which PE interfaces are used as upstream and cascade ports. 

```
[admin@Controller_Bridge] > interface bridge port-controller device monitor [find]
                   name: pe1                    pe2
                 status: active                 active
    connected-via-ports: bond1==pe1-cntrl-bond1 bond1==pe1-cntrl-bond1
                                                pe1-cntrl-bond2==pe2-cntrl-bond1
     connected-via-devs: controller             controller
                                                pe1
[admin@Controller_Bridge] > interface bridge port-controller port print where running or upstream-port
Flags: I - inactive, X - disabled, R - running, U - upstream-port, C - cascade-port
 #    NAME                                                  DEVICE
 0 R  pe1-
ether2                                            pe1
 1 R  pe1-
ether3                                            pe1
 2 R  pe1-
ether4                                            pe1
 3  U pe1-
sfpplus1                                          pe1
 4  U pe1-
sfpplus2                                          pe1
 5 RC pe1-
sfpplus3                                          pe1
 6 RC pe1-
sfpplus4                                          pe1
 7 R  pe2-
ether1                                            pe2
 8 R  pe2-
ether2                                            pe2
 9 R  pe2-
ether3                                            pe2
10 R  pe2-
ether4                                            pe2
11  U pe2-
sfpplus1                                          pe2
12  U pe2-
sfpplus2                                          pe2
```
