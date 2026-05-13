## Properties 

**==> picture [495 x 118] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>comment  (string; Default: ) Short description of the interface<br>disabled  (yes | no; Default: no ) If set to yes then this configuration is ignored.<br>interface  (name; Default:) Name of the interface or interface-list to match.<br>input  (yes | no; Default: yes ) Whether to allow MPLS input on the interface<br>mpls-mtu  (integer [512..65535]; Default: 1508 ) The option represents how big packets can be carried over the interface with added MPLS labels.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Listed entries are ordered, and the first entry (iterating from the top to the bottom) that matches the interface will be used. 

The order of the entries is important due to the possibility that different interface lists can contain the same interface and in addition, that interface can be referenced directly. 

837 

Selection of the MPLS MTU happens in the following manner: 

If the interface matched the entry from this table, then try to use configured MPLS MTU value If the interface does not match any entry then consider MPLS MTU equal to L2MTU If the interface does not support L2MTU, then consider MPLS MTU equal to L3 MTU 

On the MPLS ingress path, MTU is chosen by min(MPLS MTU - tagsize, l3mtu). This means that on interfaces that do not support L2MTU and default L3 MTU is set to 1500, max path MTU will be 1500 - tag size (the interface will not be able to pass full IP frame without fragmentation). In such scenarios, L3MTU must be increased by max observed tag size. 

Read more on MTUs in the MTU in RouterOS article.
