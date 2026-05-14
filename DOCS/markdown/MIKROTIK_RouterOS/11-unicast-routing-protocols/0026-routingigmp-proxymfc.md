## `/routing/igmp-proxy/mfc` 

Multicast forwarding cache (MFC) status. 

**==> picture [516 x 120] intentionally omitted <==**

**----- Start of picture text -----**<br>
Read-only Property Description<br>active-downstream-interfaces The packet stream is going out of the router through this interface.<br>(read-only: name)<br>bytes  (read-only: integer) The total amount of received multicast traffic.<br>packets  (read-only: integer) The total amount of received multicast packets.<br>wrong-packets  (read-only:  The total amount of received multicast packets that arrived on a wrong interface, for example, a multicast stream that is<br>integer) received on a downstream interface instead of an upstream interface.<br>**----- End of picture text -----**<br>

RouterOS support static multicast forwarding rules for IGMP proxy. If a static rule is added, all dynamic rules for that group will be ignored. These rules will take effect only if IGMP-proxy interfaces are configured (upstream and downstream interfaces should be set) or these rules won't be active. 

**==> picture [364 x 99] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>downstream-interfaces  (name; Default: ) The received stream will be sent out to the listed interfaces only.<br>group  (IP address) The multicast group address this rule applies.<br>source  (IP address) The multicast data originator address.<br>upstream-interface  ( name) The interface that is receiving stream data.<br>**----- End of picture text -----**<br>

967
