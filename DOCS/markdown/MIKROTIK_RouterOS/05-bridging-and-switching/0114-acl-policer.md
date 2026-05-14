## ACL Policer 

Sub-menu: `/interface ethernet switch acl policer` 

**==> picture [507 x 42] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name  (string; Default: policerX ) Name of the Policer used in ACL.<br>**----- End of picture text -----**<br>

431 

**==> picture [507 x 404] intentionally omitted <==**

**----- Start of picture text -----**<br>
yellow-rate  (integer) Maximum data rate limit for packets with yellow drop precedence.<br>yellow-burst  (integer; Default: 0 ) Maximum data rate which can be transmitted while the burst is allowed for packets with yellow drop<br>precedence.<br>red-rate  (integer); Default: 0 ) Maximum data rate limit for packets with red drop precedence.<br>red-burst  (integer; Default: 0 ) Maximum data rate which can be transmitted while the burst is allowed for packets with red drop<br>precedence.<br>meter-unit  (bit | packet; Default: bit ) Measuring units for ACL traffic rate.<br>meter-len  (layer-1 | layer-2 | layer-3; Default: la Packet classification which sets the packet byte length for metering.<br>yer-1 )<br>layer-1 - includes entire layer-2 frame + FCS + inter-packet gap + preamble.<br>layer-2 - includes layer-2 frame + FCS.<br>layer-3 - includes only layer-3 + ethernet padding without layer-2 header and FCS.<br>color-awareness  (yes | no; Default: no ) YES makes the policer to take into account pre-colored drop precedence, NO - ignores drop<br>precedence.<br>bucket-coupling  (yes | no; Default: no )<br>yellow-action  (drop | forward | remark; Default: Performed action for exceeded traffic with yellow drop precedence.<br>drop )<br>new-dei-for-yellow  (0..1 | remap) New DEI for yellow drop precedence packets.<br>new-pcp-for-yellow  (0..7 | remap) New PCP for yellow drop precedence packets.<br>new-dscp-for-yellow  (0..63 | remap) New DSCP for yellow drop precedence packets.<br>red-action  (drop | forward | remark; Default: dr Performed action for exceeded traffic with red drop precedence.<br>op )<br>new-dei-for-red  (0..1 | remap) New DEI for red drop precedence packets.<br>new-pcp-for-red  (0..7 | remap) New PCP for red drop precedence packets.<br>new-dscp-for-red  (0..63 | remap) New DSCP for red drop precedence packets.<br>**----- End of picture text -----**<br>
