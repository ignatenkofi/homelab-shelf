## Layer 2 Dependency 

Layer 3 hardware processing lies on top of Layer 2 hardware processing. Therefore, L3HW offloading requires L2HW offloading on the underlying interfaces. The latter is enabled by default, but there are some exceptions. For example, CRS3xx devices support only one hardware bridge. If there are multiple bridges, others are processed by the CPU and are not subject to L3HW. 

Another example is ACL rules. If a rule redirects traffic to the CPU for software processing, then hardware routing (L3HW) is not triggered: 

ACL rule to disable hardware processing on a specific port 

```
/interface/ethernet/switch/rule/add switch=switch1 ports=ether1 redirect-to-cpu=yes
```

**==> picture [13 x 13] intentionally omitted <==**

It is recommended to turn off L3HW offloading during L2 configuration. 

To make sure that Layer 3 is in sync with Layer 2 on both the software and hardware sides, we recommend disabling L3HW while configuring Layer 2 features. The recommendation applies to the following configuration: 

adding/removing/enabling/disabling bridge; adding/removing switch ports to/from the bridge; bonding switch ports / removing bond; changing VLAN settings; changing MTU/L2MTU on switch ports; changing ethernet (MAC) addresses. 

In short, disable `l3-hw-offloading` while making changes under `/interface/bridge/` and `/interface/vlan/` :
