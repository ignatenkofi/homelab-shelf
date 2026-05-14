## `/interface/ethernet/switch/rule` 

```
add switch=switch1 ports=sfp-sfpplus1 vlan-id=10 dst-address=10.0.0.0/8 new-dst-ports=""
```

The matched packets will be dropped on the hardware level. It is much better than letting all guest packets to the CPU for Firewall filtering. 

Of course, ACL rules cannot match everything. For instance, ACL rules cannot filter connection states: accept established, drop others. That is where Fasttrack HW Offloading gets into action - redirect the packets to the CPU by default for firewall filtering, then offload the established Fasttrack connections. However, disabling `l3-hw-offloading` for the entire switch, port is not the only option. 

**==> picture [13 x 13] intentionally omitted <==**

Define ACL rules with **`redirect-to-cpu=yes`** instead of setting `l3-hw-offloading=no` of the switch port for narrowing down the traffic that goes to the CPU.
