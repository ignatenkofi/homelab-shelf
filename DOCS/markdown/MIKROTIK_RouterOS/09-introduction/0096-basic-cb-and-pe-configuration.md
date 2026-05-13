## Basic CB and PE configuration 

In this example, a CRS317-1G-16S+ device is used as a Controller Bridge and CRS328-24P-4S+ as a Port Extender, see the connection scheme below. 

**==> picture [504 x 356] intentionally omitted <==**

543 

First, configure the CB device. This can be done by adding a bridge interface with enabled VLAN filtering. Additionally, add any local interfaces to the same bridge, it allows to forward traffic between any local interfaces and extended interfaces. In this example, an sfp-sfpplus2 interface is added. 

```
/interface bridge
add name=bridge1 vlan-filtering=yes
/interface bridge port
add bridge=bridge1 interface=sfp-sfpplus2
```

To enable CB, specify the bridge, switch and at least one cascade port. Make sure that cascade ports are not included in the bridge or routing configurations. These ports are recommended only for a CB and PE usage. 

```
/interface bridge port-controller
```

```
set bridge=bridge1 cascade-ports=sfp-sfpplus1 switch=switch1
```

To enable PE, configure control ports and switch. Additionally, configure one or multiple interfaces that should not be extended with `excluded-ports` property (e.g. for out-of-band management purposes). In this example, all switch ports will be extended. 

```
/interface bridge port-extender
```

```
set control-ports=sfp-sfpplus4 switch=switch1
```

Once PE and CB devices finish the discovery and start the Control and Status Protocol (CSP), the RouterOS will permanently create new interfaces and add them into bridge on the CB device. Interfaces are named by the automatically assigned PE device name, plus the default interface name, these interface names can be modified afterwards. Note that control and excluded ports will be also displayed into the interface list, but they are not included into the bridge. 

544 

```
[admin@Controller_Bridge] > /interface print where name~"pe"
Flags: D - dynamic, X - disabled, R - running, S - slave
 #     NAME                                TYPE       ACTUAL-MTU L2MTU  MAX-L2MTU
 0  RS pe1-ether1                          extport          1500  1584
 1  RS pe1-ether2                          extport          1500  1584
 2  RS pe1-ether3                          extport          1500  1584
 3   S pe1-ether4                          extport          1500  1584
 4   S pe1-ether5                          extport          1500  1584
 5   S pe1-ether6                          extport          1500  1584
 6   S pe1-ether7                          extport          1500  1584
 7   S pe1-ether8                          extport          1500  1584
 8   S pe1-ether9                          extport          1500  1584
 9   S pe1-ether10                         extport          1500  1584
10   S pe1-ether11                         extport          1500  1584
11   S pe1-ether12                         extport          1500  1584
12   S pe1-ether13                         extport          1500  1584
13   S pe1-ether14                         extport          1500  1584
14   S pe1-ether15                         extport          1500  1584
15   S pe1-ether16                         extport          1500  1584
16   S pe1-ether17                         extport          1500  1584
17   S pe1-ether18                         extport          1500  1584
18   S pe1-ether19                         extport          1500  1584
19   S pe1-ether20                         extport          1500  1584
20   S pe1-ether21                         extport          1500  1584
21   S pe1-ether22                         extport          1500  1584
22   S pe1-ether23                         extport          1500  1584
23   S pe1-ether24                         extport          1500  1584
24  RS pe1-sfpplus1                        extport          1500  1584
25  RS pe1-sfpplus2                        extport          1500  1584
26  RS pe1-sfpplus3                        extport          1500  1584
27     pe1-sfpplus4                        extport          1500  1584
[admin@Controller_Bridge] > interface bridge port print
Flags: X - disabled, I - inactive, D - dynamic, H - hw-offload
 #     INTERFACE              BRIDGE             HW  PVID PRIORITY  PATH-COST INTERNAL-PATH-COST    HORIZON
 0   H sfp-sfpplus2           bridge1            yes    1     0x80         10                 10       none
 1   H pe1-ether1             bridge1            yes    1     0x80         10                 10       none
 2   H pe1-ether2             bridge1            yes    1     0x80         10                 10       none
 3   H pe1-ether3             bridge1            yes    1     0x80         10                 10       none
 4 I H pe1-ether4             bridge1            yes    1     0x80         10                 10       none
 5 I H pe1-ether5             bridge1            yes    1     0x80         10                 10       none
 6 I H pe1-ether6             bridge1            yes    1     0x80         10                 10       none
 7 I H pe1-ether7             bridge1            yes    1     0x80         10                 10       none
 8 I H pe1-ether8             bridge1            yes    1     0x80         10                 10       none
 9 I H pe1-ether9             bridge1            yes    1     0x80         10                 10       none
10 I H pe1-ether10            bridge1            yes    1     0x80         10                 10       none
11 I H pe1-ether11            bridge1            yes    1     0x80         10                 10       none
12 I H pe1-ether12            bridge1            yes    1     0x80         10                 10       none
13 I H pe1-ether13            bridge1            yes    1     0x80         10                 10       none
14 I H pe1-ether14            bridge1            yes    1     0x80         10                 10       none
15 I H pe1-ether15            bridge1            yes    1     0x80         10                 10       none
16 I H pe1-ether16            bridge1            yes    1     0x80         10                 10       none
17 I H pe1-ether17            bridge1            yes    1     0x80         10                 10       none
18 I H pe1-ether18            bridge1            yes    1     0x80         10                 10       none
19 I H pe1-ether19            bridge1            yes    1     0x80         10                 10       none
20 I H pe1-ether20            bridge1            yes    1     0x80         10                 10       none
21 I H pe1-ether21            bridge1            yes    1     0x80         10                 10       none
22 I H pe1-ether22            bridge1            yes    1     0x80         10                 10       none
23 I H pe1-ether23            bridge1            yes    1     0x80         10                 10       none
24 I H pe1-ether24            bridge1            yes    1     0x80         10                 10       none
25   H pe1-sfpplus1           bridge1            yes    1     0x80         10                 10       none
26   H pe1-sfpplus2           bridge1            yes    1     0x80         10                 10       none
27   H pe1-sfpplus3           bridge1            yes    1     0x80         10                 10       none
```

Now the CRS317-1G-16S+ device has extended its ports using the CRS328-24P-4S+ device and packet forwarding can be done between all bridged ports. 

Trunk and Access ports 

545 

In this example, untagged (access) and tagged (trunk) port configuration will be created on the Controller Bridge device, see the network diagram below. 

**==> picture [504 x 409] intentionally omitted <==**

First, configure the CB and PE devices, the configuration is identical to the previous example. Use this configuration for CB device. 

```
/interface bridge
add name=bridge1 vlan-filtering=yes
/interface bridge port
add bridge=bridge1 interface=sfp-sfpplus2
/interface bridge port-controller
set bridge=bridge1 cascade-ports=sfp-sfpplus1 switch=switch1
```

Use this configuration for PE device. 

```
/interface bridge port-extender
set control-ports=sfp-sfpplus4 switch=switch1
```

After extended ports are successfully created and added to the bridge on the CB device, we can start configuring VLAN related properties. First, configure access ports to their respective VLAN ID using a `pvid` property. Use a `print` command in " `/interface bridge port` " menu to find out the exact interface name. 

546 

```
/interface bridge port
```

```
set [find interface=pe1-ether1] pvid=10
set [find interface=pe1-ether2] pvid=20
set [find interface=pe1-ether3] pvid=30
```

Then add bridge VLAN entries and specify tagged, untagged ports. Note that there are two tagged ports - local port named sfp-sfpplus2 and extended port named pe1-sfpplus1.
