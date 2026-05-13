## Sub-menu: `/interface/ethernet/switch/qos/profile` 

QoS profiles determine priority field values (PCP, DSCP) for the forwarded/routed packets. Congestion avoidance/resolution is based on QoS profiles. Each packet gets a QoS profile assigned based on the ingress switch port QoS settings (see `/in/eth/sw/port` ). 

**==> picture [516 x 224] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>color  (green  Traffic color for color-aware drop precedence management. Leave the default value (green) for color-blind drop precedence<br>| yellow | red; management.<br>Default:  green<br>)<br>dscp  (integer IPv4/IPv6 DSCP field value for the egress packets assigned to the QoS profile.<br>: 0..63;<br>Default: ) 0<br>name  (string; The user-defined name of the QoS profile.<br>Default: )<br>pcp  (integer:  VLAN priority value (IEEE 802.1q PCP - Priority Code Point). Used only if the egress packets assigned to the QoS profile are VLAN-<br>0..7;  tagged (have the 802.1q header). The value can be further altered via the QoS Egress Map.<br>Default: ) 0<br>traffic-class  (i The traffic class determines the packet priority and the egress queue (see  tx-manager ). The queue number is usually the same as the<br>nteger: 0..7;  traffic class (packets with tc0 go into queue0, tc1 - queue1, ... tc7 - queue7). Unlike pcp, where 0 means the default priority but 1 - the<br>Default: ) 0 lowest one (and further customizable), traffic classes are strictly ordered. TC0 always selects the lowest priority, etc.<br>**----- End of picture text -----**<br>


475
