## Untagged from tagged port 

It is possible to allow access to the device from the trunk (tagged) port with untagged traffic. To do so, assign an IP address on the bridge interface: 

```
/ip address
add address=10.0.0.1/24 interface=bridge1
```

497 

Specify which ports are allowed to access the CPU. Use `vlan-id` that is used in `default-vlan-id` for switch-cpu and trunk ports, by default it is set to 0 or 1. 

```
/interface ethernet switch vlan
```

```
add ports=ether1,switch1-cpu switch=switch1 vlan-id=1
```

When the VLAN table is configured, you can enable `vlan-mode=secure` to limit access to the CPU: 

```
/interface ethernet switch port
```

```
set ether1 default-vlan-id=1 vlan-header=add-if-missing vlan-mode=secure
set switch1-cpu default-vlan-id=1 vlan-header=leave-as-is vlan-mode=secure
```

**==> picture [13 x 12] intentionally omitted <==**

This configuration example is not possible for devices with the Atheros8316 and Atheros7240 switch chips. For devices with QCA8337 and Ather os8327 switch chips, it is possible to use any other `default-vlan-id` as long as it stays the same on switch-cpu and trunk ports. For devices with Atheros8227 switch chip only `default-vlan-id=0` can be used and the trunk port must use `vlan-header=leave-as-is` .
