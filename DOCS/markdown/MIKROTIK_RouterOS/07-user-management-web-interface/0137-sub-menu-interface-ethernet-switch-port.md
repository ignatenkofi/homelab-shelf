## Sub-menu: `/interface ethernet switch port` 

**==> picture [516 x 197] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>limit-broadcasts  (yes | no; Default: yes ) Limit broadcast traffic on a switch port.<br>limit-unknown-multicasts  (yes | no; Default: Limit unknown multicast traffic on a switch port.<br>no )<br>limit-unknown-unicasts  (yes | no; Default: no Limit unknown unicast traffic on a switch port.<br>)<br>storm-rate  (integer 0..100; Default: 100 ) Amount of broadcast, unknown multicast and/or unknown unicast traffic is limited to in percentage of the<br>link speed.<br>Devices with 98DX224S, 98DX226S, 98DX2528, 98DX3236 switch chip cannot distinguish unknown multicast traffic from all multicast traffic.<br>For example, CRS326-24G-2S+ will limit all multicast traffic when limit-unknown-multicasts and storm-rate is used. For other<br>devices, for example, CRS317-1G-16S+ the limit-unknown-multicasts parameter will limit only unknown multicast traffic (addresses that<br>are not present in  /interface bridge mdb).<br>**----- End of picture text -----**<br>


For example, to limit 1% (10Mbps) of broadcast and unknown unicast traffic on ether1 (1Gbps), use the following commands: 

```
/interface ethernet switch port
```

```
set ether1 storm-rate=1 limit-broadcasts=yes limit-unknown-unicasts=yes
```

**==> picture [13 x 13] intentionally omitted <==**

Due to hardware limitations, the `egress-rate` and `storm-rate` settings do not work correctly on 10Gbps switch ports when they are linked at 10/100Mbps, 1/2.5/5Gbps. This applies to 98DX224S, 98DX226S, 98DX2528, 98DX3236 switch chips.
