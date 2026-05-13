## Protocol-based traffic policer: 

```
/interface ethernet switch rule
```

```
add ports=ether1 switch=switch1 mac-protocol=ipx rate=10M
```

There are other options as well, check the ACL section to find out all possible parameters that can be used to match packets. 

**==> picture [13 x 13] intentionally omitted <==**

The Switch Rule table is used for QoS functionality, see this table on how many rules each device supports. 

**==> picture [13 x 13] intentionally omitted <==**

Due to hardware limitations, the `egress-rate` and `storm-rate` settings do not work correctly on 10Gbps switch ports when they are linked at 10/100Mbps, 1/2.5/5Gbps. This applies to 98DX224S, 98DX226S, 98DX2528, 98DX3236 switch chips.
