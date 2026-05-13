## Properties 

**==> picture [516 x 357] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>clamp-tcp-mss  ( Controls whether to change MSS size for received TCP SYN packets. When enabled, a router will change the MSS size for received<br>yes | no;  TCP SYN packets if the current MSS size exceeds the tunnel interface MTU (taking into account the TCP/IP overhead).The received<br>Default:  yes ) encapsulated packet will still contain the original MSS, and only after decapsulation the MSS is changed.<br>dont-fragment  (i Whether to include DF bit in related packets:<br>nherit | no;<br>Default:  no ) no - fragment if needed, inherit - use Dont Fragment flag of original packet.<br>(Without Dont Fragment: inherit - packet may be fragmented).<br>dscp  (inherit |  Set dscp value in IPIP header to a fixed value or inherit from dscp value taken from tunnelled traffic<br>integer [0-63];<br>Default: )<br>ipsec-secret  (str When secret is specified, router adds dynamic ipsec peer to remote-address with pre-shared key and policy with default values (by<br>ing; Default: ) default phase2 uses sha1/aes128cbc).<br>local-address  (IP IP address on a router that will be used by IPIP tunnel<br>; Default: )<br>mtu  (integer;  Layer3 Maximum transmission unit<br>Default:  1500 )<br>keepalive  (integ Tunnel keepalive parameter sets the time interval in which the tunnel running flag will remain even if the remote end of tunnel goes<br>er[/time],integer  down. If configured time,retries fail, interface running flag is removed. Parameters are written in following format:  KeepaliveInterv<br>0..4294967295;  al,KeepaliveRetries  where KeepaliveInterval is time interval and KeepaliveRetries - number of retry attempts. By default<br>Default:  10s,10 ) keepalive is set to 10 seconds and 10 retries. To disable set *set ipipv6-tunnel1 !keepalive<br>name  (string;  Interface name<br>Default: )<br>remote-address IP address of remote end of IPIP tunnel<br>(IP; Default: )<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

There is no authentication or 'state' for this interface. The bandwidth usage of the interface may be monitored with the monitor feature from the interface menu. 

1186
