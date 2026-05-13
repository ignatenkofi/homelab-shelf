## Sub-menu: `/interface/ethernet/switch/qos/port` 

Switch port QoS settings. Assigns a QoS profile to ingress packets on the given port. The assigned profile can be changed via match rules if the port is considered trusted. 

By default, ports are untrusted and receive the default QoS profile (Best-Effort, PCP=0, DSCP=0), where priority fields are cleared from the egress packets. 

**==> picture [516 x 240] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>egress-rate-queue0 .. egress-rate-queue7  ( Sets egress traffic limitation (bits per second) for specific output queue. It is possible to specify the limit<br>integer: 0..18446744073709551615;  using suffixes like k, M, or G to represent kbps, Mbps, or Gbps. This setting can be combined with the<br>Default !egress-rate-queuex ) overall per-port limit egress-rate  (see /in/eth/sw/port ).<br>map  (name; Default:  default ) Allows user-defined QoS priority-to-profile mapping in the case of a trusted port or host (see  /in/eth/sw<br>/qos/map ).<br>pfc  (name; Default:  disabled ) The name of the PFC profile to control ingress priority-based traffic flow (see  /in/eth/sw/qos<br>/priority-flow-control ).<br>profile  (name; Default:  default ) The name of the QoS profile to assign to the ingress packets by default (see  /in/eth/sw/qos/profile<br>).<br>trust-l2  (ignore | trust | keep; Default:  ignore Whenever to trust the Layer 2 headers of the incoming packets (802.1p PCP field):<br>)<br>ignore  - ignore L2 header; use the port's  profile  value for all incoming packets;<br>trust  - use PCP field of VLAN-tagged packets for QoS profile lookup in  map . Untagged packets use<br>the port's  profile  value. Forwarded VLAN or priority-tagged packets receive the PCP value from the<br>selected QoS profile (overwriting the original value).<br>keep  - trust but keep the original PCP value in forwarded packets.<br>**----- End of picture text -----**<br>


469 

trust-l3 (ignore | trust | keep; Default: ignore Whenever to trust the Layer 3 headers of the incoming packets (IP DSCP field): ) ignore - ignore L3 header; use either L2 header or the port's profile (depends on trust-l2 ). trust - use DSCP field of IP packets for QoS profile lookup in map . Forwarded/routed IP packets receive the DSCP value from the selected QoS profile (overwriting the original value). keep - trust but keep the original DSCP value in forwarded/routed packets. tx-manager (name; Default: default ) The name of the Transmission Manager that is responsible for enqueuing and transmitting packets from the given port (see **`/in/eth/sw/qos/tx-manager`** ). 

**==> picture [516 x 239] intentionally omitted <==**

**----- Start of picture text -----**<br>
L3 trust mode has higher precedence than L2 unless trust-l3=ignore or the packet does not have an IP header.<br>Forwarded/routed packets obtain priority field values (PCP, DSCP) from the selected QoS profile, overwriting the original values unless the<br>respective trust mode is set to  keep .<br>Commands.<br>Command Description<br>print Print the above properties in a human-friendly format.<br>print stats Print port statistics: total and per-queue transmitted/dropped packets/bytes.<br>reset-counters Reset all counters in port statistics to zero.<br>print usage Print queue usage/resources.<br>print pfc Pring Priority Flow Control stats<br>print rates Print per-queue egress traffic limitation (set by egress-rate-queueX )<br>**----- End of picture text -----**<br>
