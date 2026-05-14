## Sub-menu: `/ip traffic-flow` 

This section lists the configuration properties of Traffic-Flow. 

**==> picture [516 x 250] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>interfaces  (string | all;  Names of those interfaces will be used to gather statistics for traffic-flow. To specify more than one interface, separate<br>Default:  all ) them with a comma.<br>cache-entries  (128k | 16k |  Number of flows which can be in router's memory simultaneously.<br>1k | 256k | 2k | ... ; Default:<br>4k )<br>active-flow-timeout  (time;  Maximum life-time of a flow.<br>Default:  30m )<br>inactive-flow-timeout  (time;  How long to keep the flow active, if it is idle. If a connection does not see any packet within this timeout, then traffic-flow<br>Default:  15s ) will send a packet out as a new flow. If this timeout is too small it can create a significant amount of flows and overflow the<br>buffer.<br>packet-sampling  (no | yes;  Enable or disable packet sampling feature.<br>Default:  no )<br>sampling-interval  (integer;  The number of packets that are consecutively sampled.<br>Default: ) 0<br>sampling-space  (integer;  The number of packets that are consecutively omitted.<br>Default: ) 0<br>**----- End of picture text -----**<br>

1822 

**==> picture [13 x 13] intentionally omitted <==**

info 

Packet sampling is available in RouterOS v7. 

In the following example: 

```
/ip/traffic-flow/set packet-sampling=yes sampling-interval=2222 sampling-space=1111
```

2222 packet consecutive packets will be sampled and then 1111 will be omitted. Then the sampling cycle repeats in such a manner.
