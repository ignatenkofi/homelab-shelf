## Cascading multiple Port Extenders and using bonding interface 

In this example, two PE devices (CRS328-24P-4S+ and CRS326-24G-2S+) will be added to the CB (CRS317-1G-16S+). To increase throughput for upstream and cascade ports, bonding interfaces will be created. See the network diagram below. 

547 

**==> picture [504 x 463] intentionally omitted <==**

The CB and PE configuration is similar to the first example, the main difference is the bonding interface usage. First, configure the CB device - create a bonding interface for cascade port, create a bridge and add any needed local bridge ports, last enable the CB. Use the following commands: 

```
/interface bonding
add mode=802.3ad name=bond1 slaves=sfp-sfpplus1,sfp-sfpplus2
/interface bridge
add name=bridge1 vlan-filtering=yes
/interface bridge port
add bridge=bridge1 interface=sfp-sfpplus3
/interface bridge port-controller
set bridge=bridge1 cascade-ports=bond1 switch=switch1
```

Then configure the Port Extender 1 device. This device needs two bonding interfaces - the first one will be used as an upstream port and the second one will be a cascade port for the Port Extender 2 device. Additionally, configure one or multiple interfaces that should not be extended with `excluded -ports` property (e.g. for out-of-band management purposes). In this example, all switch ports will be extended. 

548
