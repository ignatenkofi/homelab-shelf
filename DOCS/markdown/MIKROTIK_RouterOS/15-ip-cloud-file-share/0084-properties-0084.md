## Properties 

**==> picture [516 x 141] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>add-relay-info  (yes |  Adds DHCP relay agent information if enabled according to RFC 3046. Agent Circuit ID Sub-option contains mac address of<br>no; Default:  no ) an interface, Agent Remote ID Sub-option contains MAC address of the client from which request was received.<br>delay-threshold  (time |  If secs field in DHCP packet is smaller than delay-threshold, then this packet is ignored<br>none; Default:  none )<br>dhcp-server  (string;  List of DHCP servers' IP addresses which should the DHCP requests be forwarded to<br>Default: )<br>interface  (string;  Interface name the DHCP relay will be working on.<br>Default: )<br>**----- End of picture text -----**<br>


911 

local-address (IP; The unique IP address of this DHCP relay needed for DHCP server to distinguish relays. If set to 0.0.0.0 - the IP address will Default: 0.0.0.0 ) be chosen automatically from addresses that are assigned to an interface a relay is running relay-info-remote-id (st specified string will be used to construct Option 82 instead of client's MAC address. Option 82 consist of: interface from which ring; Default: ) packets was received + client mac address or relay-info-remote-id name (string; Default: ) Descriptive name for the relay local-address-as-src-ip Use local address as source address for Discover/Request packets sent to the DHCP server ( yes | no; Default: no)
