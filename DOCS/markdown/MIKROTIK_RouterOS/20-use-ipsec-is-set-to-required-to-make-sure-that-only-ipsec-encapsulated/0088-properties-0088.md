## Properties 

**==> picture [516 x 234] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>accept-untagged  (yes |  This setting controls whether the PPPoE server will accept untagged (non-VLAN) PPPoE packets on its interface. By default,<br>no; Default:  yes ) untagged PPPoE packets are accepted. If you are using the  pppoe-over-vlan-range  property (which enabled PPPoE<br>over 802.1Q VLANs), this option lets you decide whether to still allow untagged clients on the same interface. If you are not<br>using the  pppoe-over-vlan-range , this setting do not have any effect.<br>authentication  (  Authentication algorithm.<br>mschap2 | mschap1 |<br>chap | pap; Default:  "ms<br>chap2, mschap1, chap,<br>pap" )<br>default-profile  (string;<br>Default:  "default" )<br>interface  (string;  Interface that the clients are connected to.<br>Default: ) ""<br>keepalive-timeout  (time; Defines the time period (in seconds) after which the router is starting to send keepalive packets every second. If there is no<br>Default:  "10" ) traffic and no keepalive responses arrive for that period of time (i.e. 2 * keepalive-timeout), the non responding client is<br>proclaimed disconnected.<br>**----- End of picture text -----**<br>


1253 

**==> picture [516 x 349] intentionally omitted <==**

**----- Start of picture text -----**<br>
max-mru  (integer;  Maximum Receive Unit. The optimal value is the MTU of the interface the tunnel is working over reduced by 20 (so, for 1500-<br>Default:  "1480" ) byte Ethernet link, set the MTU to 1480 to avoid fragmentation of packets)<br>max-mtu  (integer;  Maximum Transmission Unit. The optimal value is the MTU of the interface the tunnel is working over reduced by 20 (so, for<br>Default:  "1480" ) 1500-byte Ethernet link, set the MTU to 1480 to avoid fragmentation of packets)<br>max-sessions  (integer;  Maximum number of clients that the AC can serve. '0' = no limitations.<br>Default:  "0" )<br>mrru  (integer: 512.. Maximum packet size that can be received on the link. If a packet is bigger than tunnel MTU, it will be split into multiple<br>65535 | disabled;  packets, allowing full size IP or Ethernet packets to be sent over the tunnel.<br>Default:  "disabled" )<br>one-session-per-host  (y Allow only one session per host (determined by MAC address). If a host tries to establish a new session, the old one will be<br>es | no; Default:  "no" ) closed.<br>pppoe-over-vlan-range ( This setting allows a PPPoE server to operate over 802.1Q VLANs. By default, a PPPoE server only accepts untagged<br>integer 1..4094; Default: packets on its interface. However, in scenarios where clients are on separate VLANs, instead of creating multiple 802.1Q<br>"") VLAN interfaces and bridging them together or configuring individual PPPoE servers for each VLAN, you can specify the<br>necessary VLANs directly in the PPPoE server settings.<br>When you specify the VLAN IDs, the PPPoE server will accept 802.1Q tagged packets from clients, and it will reply using the<br>same VLAN. You then have an option to accept or drop untagged PPoE clients on the same interface using the  accept-<br>untagged  property.<br>The  pppoe-over-vlan-range  setting can be applied to both CVLAN and SVLAN interfaces, enabling the QinQ setups as<br>well. See the  use-service-tag=yes  option on a VLAN interface. But keep in mind that the inner VLAN tag should be 802.1<br>Q.<br>The setting supports a range of VLAN IDs, as well as individual VLANs specified using comma-separated values. For<br>example: pppoe-over-vlan-range=100-115,120,122,128-130.<br>service-name  (string;  The PPPoE service name. Server will accept clients which sends PADI message with service-names that matches this<br>Default: ) "" setting or if service-name field in PADI message is not set.<br>**----- End of picture text -----**<br>


The PPPoE server (access concentrator) supports multiple servers for each interface - with differing service names. The access concentrator name and PPPoE service name are used by clients to identify the access concentrator to register with. The access concentrator name is the same as the identity of the router displayed before the command prompt. The identity may be set within the /system identity submenu. 

**==> picture [13 x 13] intentionally omitted <==**

Do not assign an IP address to the interface you will be receiving the PPPoE requests on. 

Specifying MRRU means enabling MP (Multilink PPP) over a single link. This protocol is used to split big packets into smaller ones.  Their MRRU is hardcoded to 1614. This setting is useful to overcome PathMTU discovery failures. The MP setting should be enabled on both peers. 

**==> picture [13 x 13] intentionally omitted <==**

The default keepalive-timeout value of 10s is OK in most cases. If you set it to 0, the router will not disconnect clients until they explicitly log out or the router is restarted. To resolve this problem, the one-session-per-host property can be used.
