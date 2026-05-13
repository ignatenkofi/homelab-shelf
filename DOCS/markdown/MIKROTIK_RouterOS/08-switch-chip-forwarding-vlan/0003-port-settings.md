## Port Settings 

Sub-menu: `/interface ethernet switch port` 

**==> picture [507 x 339] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>vlan-type  (edge-port | network-port;  Port VLAN type specifies whether VLAN ID is used in UFDB learning. The network port learns VLAN ID in<br>Default: network-port ) UFDB, edge port does not - VLAN 0. It can be observed only in IVL learning mode.<br>isolation-leakage-profile-override  (ye Custom port profile for port isolation/leakage configurations.<br>s | no; Default:<br>Port-level isolation profile 0. Uplink port - allows the port to communicate with all ports in the device.<br>!isolation-leakage-profile-override ) Port-level isolation profile 1. Isolated port - allows the port to communicate only with uplink ports.<br>Port-level isolation profile 2 - 31. Community port - allows communication among the same community<br>isolation-leakage-profile  0..31( ;) ports and uplink ports.<br>learn-override  (yes | no; Default: ! Enable or disable MAC address learning and set the MAC limit on the port. MAC learning limit is disabled by<br>learn-override ) default when !learn-override and !learn-limit are set. Property learn-override is replaced with learn under  /int<br>learn-limit  1..1023( ; Default: !learn- erface bridge port menu since RouterOS v6.42.<br>limit )<br>drop-when-ufdb-entry-src-drop  (yes  Enable or disable to drop packets when UFDB entry has action src-drop.<br>| no; Default: yes )<br>allow-unicast-loopback  (yes | no;  Unicast loopback on port. When enabled, it permits sending back when the source port and destination port<br>Default: no ) are the same for known unicast packets.<br>allow-multicast-loopback  (yes | no;  Multicast loopback on port. When enabled, it permits sending back when the source port and destination port<br>Default: no ) are the same for registered multicast or broadcast packets.<br>action-on-static-station-move  (copy- Action for packets when UFDB already contains a static entry with such MAC but with a different port.<br>to-cpu | drop | forward | redirect-to-<br>cpu; Default: forward )<br>drop-dynamic-mac-move  (yes | no;  Prevents MAC relearning until UFDB timeout if MAC is already learned on another port.<br>Default: no )<br>**----- End of picture text -----**<br>


416 

**==> picture [507 x 368] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>allow-fdb-based-vlan-translate  (yes | no; Default: no ) Enable or disable MAC-based VLAN translation on the port.<br>allow-mac-based-service-vlan-assignment-for  (all-frames |  Frame type for which applies MAC-based service VLAN translation.<br>none |<br>tagged-frame-only | untagged-and-priority-tagged-frame-only;<br>Default:<br>none )<br>allow-mac-based-customer-vlan-assignment-for  (all-frames |  Frame type for which applies MAC-based customer VLAN translation.<br>none |<br>tagged-frame-only | untagged-and-priority-tagged-frame-only;<br>Default:<br>none )<br>default-customer-pcp  (0..7; Default: 0 ) Default customer PCP of the port.<br>default-service-pcp  (0..7; Default: 0 ) Default service PCP of the port.<br>pcp-propagation-for-initial-pcp  (yes | no; Default: no ) Enables or disables PCP propagation for initial PCP assignment on ingress.<br>If the port vlan-type is Edge port, the service PCP is copied from the customer<br>PCP.<br>If the port vlan-type is a Network port, the customer PCP is copied from the<br>service PCP.<br>filter-untagged-frame  (yes | no; Default: no ) Whether to filter untagged frames on the port.<br>filter-priority-tagged-frame  (yes | no; Default: no ) Whether to filter tagged frames with priority on the port.<br>filter-tagged-frame  (yes | no; Default: no ) Whether to filter tagged frames on the port.<br>**----- End of picture text -----**<br>


**==> picture [507 x 198] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>egress-vlan-tag-table-lookup-key  (accordin Egress VLAN table (VLAN Tagging) lookup:<br>g-to-bridge-type | egress-vid; Default: egre<br>ss-vid ) egress-vid - Lookup VLAN ID is CVID when Edge port is configured, SVID when Network port is<br>configured.<br>according-to-bridge-type - Lookup VLAN ID is CVID when customer VLAN bridge is configured,<br>SVID when service VLAN bridge is configured. The Customer tag is unmodified for Edge port in<br>service VLAN bridge.<br>egress-vlan-mode  (tagged | unmodified |  Egress VLAN tagging action on the port.<br>untagged; Default: unmodified )<br>egress-pcp-propagation  (yes | no; Default: Enables or disables egress PCP propagation.<br>no )<br>If the port vlan-type is Edge port, the service PCP is copied from the customer PCP.<br>If the port vlan-type is Network port, the customer PCP is copied from the service PCP.<br>**----- End of picture text -----**<br>


**==> picture [362 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>ingress-mirror-to  (mirror0 | mirror1 | none; Default: none ) Analyzer port for port-based ingress mirroring.<br>ingress-mirroring-according-to-vlan  (yes | no; Default: no )<br>egress-mirror-to  (mirror0 | mirror1 | none; Default: none ) Analyzer port for port-based egress mirroring.<br>**----- End of picture text -----**<br>


417 

**==> picture [507 x 397] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>qos-scheme-precedence  (da-based | dscp-based | ingress-acl-based | pcp- Specifies applied QoS assignment schemes on the ingress of the port.<br>based | protocol-based | sa-based | vlan-based; Default: pcp-based, sa-<br>based, da-based, dscp-based, protocol-based, vlan-based ) da-based<br>dscp-based<br>ingress-acl-based<br>pcp-based<br>protocol-based<br>sa-based<br>vlan-based<br>pcp-or-dscp-based-qos-change-dei  (yes | no; Default: no ) Enable or disable PCP or DSCP based DEI change on port.<br>pcp-or-dscp-based-qos-change-pcp  (yes | no; Default: no ) Enable or disable PCP or DSCP based PCP change on port.<br>pcp-or-dscp-based-qos-change-dscp  (yes | no; Default: no ) Enable or disable PCP or DSCP based DSCP change on port.<br>dscp-based-qos-dscp-to-dscp-mapping  (yes | no; Default: yes ) Enable or disable DSCP to internal DSCP mapping on port.<br>pcp-based-qos-drop-precedence-mapping  (PCP/DEI-range:drop- The new value of drop precedence for the PCP/DEI to drop<br>precedence; Default: 0-15:green ) precedence (drop | green | red | yellow) mapping. Multiple mappings<br>are allowed separated by a comma e.g. "0-7:yellow,8-15:red".<br>pcp-based-qos-dscp-mapping  (PCP/DEI-range:DEI; Default: 0-15:0 ) The new value of DSCP for the PCP/DEI to DSCP (0..63) mapping.<br>Multiple mappings are allowed separated by a comma e.g. "0-7:25,8-<br>15:50".<br>pcp-based-qos-dei-mapping  (PCP/DEI-range:DEI; Default: 0-15:0 ) The new value of DEI for the PCP/DEI to DEI (0..1) mapping. Multiple<br>mappings are allowed separated by a comma e.g. "0-7:0,8-15:1".<br>pcp-based-qos-pcp-mapping  (PCP/DEI-range:DEI; Default: 0-15:0 ) The new value of PCP for the PCP/DEI to PCP (0..7) mapping.<br>Multiple mappings are allowed separated by a comma e.g. "0-7:3,8-<br>15:4".<br>pcp-based-qos-priority-mapping  (PCP/DEI-range:DEI; Default: 0-15:0 ) The new value of internal priority for the PCP/DEI to priority (0..15)<br>mapping. Multiple mappings are allowed separated by a comma e.g.<br>"0-7:5,8-15:15".<br>**----- End of picture text -----**<br>


**==> picture [507 x 120] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>priority-to-queue  (priority-range:queue; Default: 0-15:0,1: Internal priority (0..15) mapping to queue (0..7) per port.<br>1,2:2,3:3 )<br>per-queue-scheduling  (Scheduling-type:Weight; Set port to use either strict or weighted round robin policy for traffic shaping for each<br>queue group, each queue is separated by a comma.<br>Default:  wrr-group0:1,wrr-group0:2,wrr-group0:4,wrr-<br>group0:8,wrr-group0:16,wrr-group0:32,<br>wrr-group0:64,wrr-group0:128 )<br>**----- End of picture text -----**<br>


Property Description 

418 

**==> picture [507 x 341] intentionally omitted <==**

**----- Start of picture text -----**<br>
ingress-customer-tpid-override  (yes Ingress customer TPID override allows accepting specific frames with a custom customer tag TPID. The<br>| no; default value is for the tag of 802.1Q frames.<br>Default: !ingress-customer-tpid-<br>override )<br>ingress-customer-tpid  0..10000( ;<br>Default: 0x8100 )<br>egress-customer-tpid-override  (yes Egress customer TPID override allows custom identification for egress frames with a customer tag. The default<br>| no; Default: value is for the tag of 802.1Q frames.<br>!egress-customer-tpid-override )<br>egress-customer-tpid  0..10000( ;<br>Default:<br>0x8100 )<br>ingress-service-tpid-override  (yes |  Ingress service TPID override allows accepting specific frames with a custom service tag TPID. The default<br>no; Default: value is for the service tag of 802.1AD frames.<br>!ingress-service-tpid-override )<br>ingress-service-tpid  0..10000( ;<br>Default: 0x88A8 )<br>egress-service-tpid-override  (yes |  Egress service TPID override allows custom identification for egress frames with a service tag. The default<br>no; Default: value is for the service tag of 802.1AD frames.<br>!egress-service-tpid-override )<br>egress-service-tpid  0..10000( ;<br>Default:<br>0x88A8 )<br>**----- End of picture text -----**<br>


**==> picture [507 x 283] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>custom-drop-counter-includes  (counters; Default: none ) Custom include to count dropped packets for switch port custom-drop-packet counter.<br>device-loopback<br>fdb-hash-violation<br>exceeded-port-learn-limitation<br>dynamic-station-move<br>static-station-move<br>ufdb-source-drop<br>host-source-drop<br>unknown-host<br>ingress-vlan-filtered<br>queue-custom-drop-counter0-includes  (counters; Default: none Custom include to count dropped packets for switch port tx-queue-custom0-drop-<br>) packet<br>and bytes for tx-queue-custom0-drop-byte counters.<br>red<br>yellow<br>green<br>queue0<br>...<br>queue7<br>**----- End of picture text -----**<br>


419 

**==> picture [507 x 208] intentionally omitted <==**

**----- Start of picture text -----**<br>
queue-custom-drop-counter1-includes  (counters; Default: none Custom include to count dropped packets for switch port tx-queue-custom1-drop-<br>) packet<br>and bytes for tx-queue-custom1-drop-byte counters.<br>red<br>yellow<br>green<br>queue0<br>...<br>queue7<br>policy-drop-counter-includes  (counters; Default: none ) Custom include to count dropped packets for switch port policy-drop-packet counter.<br>ingress-policing<br>ingress-acl<br>egress-policing<br>egress-acl<br>**----- End of picture text -----**<br>
