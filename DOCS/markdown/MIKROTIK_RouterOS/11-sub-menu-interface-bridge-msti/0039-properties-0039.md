## Properties 

All properties in the connection list are read-only 

**==> picture [516 x 110] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>assured  (yes | no) Indicates that this connection is assured and that it will not be erased if the maximum possible tracked connection count<br>is reached.<br>confirmed  (yes | no) Connection is confirmed and a packet is sent out from the device<br>connection-mark  (string) Connection mark that was set by the mangle rule.<br>connection-type  (pptp | ftp) Type of connection, the property is empty if connection tracking is unable to determine a predefined connection type.<br>**----- End of picture text -----**<br>


633 

**==> picture [516 x 644] intentionally omitted <==**

**----- Start of picture text -----**<br>
dst-address  (ip) Destination address.<br>dst-port  (integer) Destination port.<br>dstnat  (yes | no) A connection has gone through DST-NAT (for example, port forwarding).<br>dying  (yes | no) The connection is dying due to a connection timeout.<br>expected  (yes | no) Connection is set up using connection helpers (pre-defined service rules).<br>fasttrack  (yes | no) Whether the connection is FastTracked.<br>gre-key  (integer) Contents of the GRE Key field.<br>gre-protocol  (string) Protocol of the encapsulated payload.<br>gre-version  (string) A version of the GRE protocol was used in the connection.<br>connection-mark  (string) Connection mark assigned for the connection from firewall.<br>hw-offload  (yes | no) Hardware offloaded connection.<br>icmp-code  (string) ICMP Code Field<br>icmp-id  (integer) Contains the ICMP ID<br>icmp-type  (integer) ICMP Type Number<br>orig-bytes  (integer) Amount of bytes sent out from the source address using the specific connection.<br>orig-fasttrack-bytes  (integer) Amount of FastTracked bytes sent out from the source address using the specific connection.<br>orig-fasttrack-packets  (integ Amount of FastTracked packets sent out from the source address using the specific connection.<br>er)<br>orig-packets  (integer) Amount of packets sent out from the source address using the specific connection.<br>orig-rate  (integer) The data rate at which packets are sent out from the source address using the specific connection.<br>protocol  (string) IP protocol type<br>repl-bytes  (integer) Amount of bytes received from the destination address using the specific connection.<br>repl-fasttrack-bytes  (string) Amount of FastTracked bytes received from the destination address using the specific connection.<br>repl-fasttrack-packets  (integ Amount of FastTracked packets received from the destination address using the specific connection.<br>er)<br>repl-packets  (integer) Amount of packets received from the destination address using the specific connection.<br>repl-rate  (string) The data rate at which packets are received from the destination address using the specific connection.<br>reply-dst-address  (ip) Destination address expected of return packets.<br>reply-dst-port  (integer) Destination port expected of return packets.<br>reply-src-address  (ip) Source address expected of return packets.<br>reply-src-port  (integer) Source port expected of return packets.<br>seen-reply  (yes | no) The destination address has replied to the source address.<br>src-address  (ip) The source address.<br>src-port  (integer) The source port.<br>srcnat  (yes | no) Connection is going through SRC-NAT, including packets that were masqueraded through NAT.<br>**----- End of picture text -----**<br>


634 

**==> picture [516 x 170] intentionally omitted <==**

**----- Start of picture text -----**<br>
tcp-state  (string) The current state of TCP connection :<br>"established"<br>"time-wait"<br>"close"<br>"syn-sent"<br>"syn-recv"<br>"fin-wait"<br>"close-wait"<br>"last-ack"<br>"listen"<br>timeout  (time) Time after connection will be removed from the connection list.<br>uses-helper  (yes | no) "IP/Firewall/Service Port" helper has been applied to the particular connection.<br>**----- End of picture text -----**<br>


635
