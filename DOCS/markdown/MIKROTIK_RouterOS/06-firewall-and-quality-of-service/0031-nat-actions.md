## NAT Actions 

Table lists NAT actions and their associated properties. Other actions are listed here. 

**==> picture [500 x 150] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>action  (action name;<br>Default: accept )<br>dst-nat  - replaces the destination address and/or port of an IP packet with values specified by  to-addresses  a<br>nd  to-ports  parameters<br>masquerade  - replaces the source port of an IP packet with one specified by  to-ports parameter and replace<br>the source address of an IP packet to the IP determined by the routing facility.<br>netmap  - creates a static 1:1 mapping of one set of IP addresses to another one. Often used to distribute public<br>IP addresses to hosts on private networks<br>redirect  - replaces the destination port of an IP packet with one specified by  to-ports  parameter and<br>destination address to the address of the virtual or physical incoming interface (interface that recieved the packet).<br>**----- End of picture text -----**<br>

654 

`same` - gives a particular client the same source/destination IP address from a supplied range for each connection. This is most frequently used for services that expect the same client address for multiple connections from the same client. IPv4 only `src-nat` - replaces the source address of an IP packet with values specified by `to-addresses` and `to-ports` parameters `endpoint-independent-nat` - uses endpoint-independent mapping and filtering. Works only with UDP protocol. IPv4 only. `socksify` - routes traffic specified by firewall rules through SOCKS proxy server. Requires `socks5-server` and `socks5-port` parameters or socksify-service parameter.(relevant socksify information) same-not-by-dst (yes | Specifies whether to take into account or not the destination IP address when selecting a new source IP address. no; Default: ) Applicable if `action=same` to-addresses (IP address Replace the original address with the specified one. Applicable if action is `dst-nat` , `netmap` , `same` , `src-nat` [-IP address]; Default: 0. 0.0.0 ) to-ports (integer[Replace the original port with the specified one. Applicable if action is `dst-nat` , `redirect` , `masquerade` , `netmap` , `sa` integer]: 0..65535; `me` , `src-nat` Default: ) 

655
