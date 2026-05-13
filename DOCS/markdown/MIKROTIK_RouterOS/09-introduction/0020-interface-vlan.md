## `/interface vlan` 

```
add name=VLAN100 vlan-id=100 interface=bridge1
/ip address
add address=192.168.100.1/24 interface=VLAN100
```

Specify which access (untagged) ports are allowed to access the CPU: 

```
/interface ethernet switch vlan
```

```
add ports=ether1,ether2,switch1-cpu switch=switch1 vlan-id=100
```

**==> picture [13 x 13] intentionally omitted <==**

Most commonly an access (untagged) port is accompanied by a trunk (tagged) port. In case of untagged access to the CPU, you are forced to specify both the access port and the trunk port, this gives access to the CPU from the trunk port as well. Not always this is desired and a Firewall might be required on top of VLAN filtering. 

When the VLAN table is configured, you can enable `vlan-mode=secure` to limit access to the CPU: 

```
/interface ethernet switch port
```

```
set ether1 vlan-header=add-if-missing vlan-mode=secure
set ether2 default-vlan-id=100 vlan-header=always-strip vlan-mode=secure
set switch1-cpu vlan-header=leave-as-is vlan-mode=secure
```

**==> picture [13 x 13] intentionally omitted <==**

To setup the management port using untagged traffic on a device with the Atheros7240 switch chip, you will need to set `vlan-header=addif-missing` for the CPU port.
