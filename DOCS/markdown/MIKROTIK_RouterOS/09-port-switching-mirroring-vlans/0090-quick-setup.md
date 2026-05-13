## Quick setup 

In this example, we will create a Controlling Bridge (e.g. a CRS317-1G-16S+ switch) that will connect to a single Port Extender (e.g. a CRS326-24G2S+ switch) through an SFP+1 interface. 

First, configure a bridge with enabled VLAN filtering on a CB device: 

```
/interface bridge
add name=bridge1 vlan-filtering=yes
```

On the same device, configure a port that is connected to the PE device and will act as cascade port: 

```
/interface bridge port-controller
```

```
set bridge=bridge1 cascade-ports=sfp-sfpplus1 switch=switch1
```

Last, on a PE device, simply configure a control port, which will be selected as an upstream port: 

```
/interface bridge port-extender
set control-ports=sfp-sfpplus1 switch=switch1
```

539 

Once PE and CB devices are connected, all interfaces that are on the same switch group (except for control ports) will be extended and can be further configured on a CB device. An automatic bridge port configuration will be applied on the CB device which adds all extended ports in a single bridge, this configuration can be modified afterward. 

**==> picture [13 x 13] intentionally omitted <==**

In order to exclude some port from being extended (e.g. for out-of-band management purposes), additionally, configure `excluded-ports` property. 

**==> picture [13 x 13] intentionally omitted <==**

Make sure not to include the `cascade-ports` and `control-ports` in any routing or bridging configurations. These ports are recommended only for a CB and PE usage.
