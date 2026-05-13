## Protocol Based VLAN 

**==> picture [504 x 397] intentionally omitted <==**

Switch together the required ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
```

```
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```

Set VLAN for IP and ARP protocols: 

556 

```
/interface ethernet switch protocol-based-vlan
```

```
add port=ether2 protocol=arp set-customer-vid-for=all new-customer-vid=0
add port=ether6 protocol=arp set-customer-vid-for=all new-customer-vid=200
add port=ether2 protocol=ip set-customer-vid-for=all new-customer-vid=0
add port=ether6 protocol=ip set-customer-vid-for=all new-customer-vid=200
```
