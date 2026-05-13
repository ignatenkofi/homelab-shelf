## Ingress Port Policer 

Sub-menu: `/interface ethernet switch ingress-port-policer` 

**==> picture [507 x 300] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>burst  (integer; Default: 100k ) Maximum data rate which can be transmitted while the burst is allowed.<br>disabled  (yes | no; Default: no ) Enables or disables ingress port policer entry.<br>meter-len  (layer-1 | layer-2 | layer-3; Default: layer-1 ) Packet classification which sets the packet byte length for metering.<br>layer-1 - includes entire layer-2 frame + FCS + inter-packet gap + preamble.<br>layer-2 - includes layer-2 frame + FCS.<br>layer-3 - includes only layer-3 + ethernet padding without layer-2 header and<br>FCS.<br>meter-unit  (bit | packet; Default: bit ) Measuring units for traffic ingress port policer rate.<br>new-dei-for-yellow  (0..1 | remap; Default: none ) Remarked DEI for exceeded traffic if yellow-action is remark.<br>new-dscp-for-yellow  (0..63 | remap; Default: none ) Remarked DSCP for exceeded traffic if yellow-action is remark.<br>new-pcp-for-yellow  (0..7 | remap; Default: none ) Remarked PCP for exceeded traffic if yellow-action is remark.<br>packet-types  (packet-types; Default: all types from  Matching packet types for which ingress port policer entry is valid.<br>description )<br>port  (port) Physical port or trunk for ingress port policer entry.<br>rate  (integer) Maximum data rate limit.<br>yellow-action  (drop | forward | remark; Default: drop ) Performed action for exceeded traffic.<br>**----- End of picture text -----**<br>
