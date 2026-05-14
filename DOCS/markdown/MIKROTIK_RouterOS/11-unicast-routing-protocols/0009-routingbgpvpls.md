## `/routing/bgp/vpls` 

This menu lists all the configured BGP-based VPLS instances. These instances allow the router to advertise VPLS BGP NLRI and indicate that the router belongs to a specific customer VPLS network. 

MP-BGP-based autodiscovery and signaling (RFC 4761). 

Cisco VPLS BGP-based auto-discovery (draft-ietf-l2vpn-signaling-08). 

Support for multiple import/export route target extended communities for BGP-based VPLS (both, RFC 4761 and draft-ietf-l2vpn-signaling-08). 

**==> picture [516 x 305] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bridge  (na The name of the bridge where dynamically created VPLS interfaces should be added as ports.<br>me)<br>bridge-<br>cost  (integ<br>er [0..<br>42949672<br>95])<br>bridge- If set to  none  bridge horizon will not be used.<br>horizon  (n<br>one |<br>integer [0..<br>42949672<br>95])<br>bridge- Used to assign port VLAN ID (pvid) for dynamically bridged interface.<br>pvid  (integ<br>er 1..<br>4094)<br>cisco-id  () Unique identifier. A parameter must be set for cisco-style VPLS signaling. In most cases this should not be used, any modern software<br>supports RFC 4761 style signaling (see site-id parameter). Parameter is a merge of l2-router-id and RD, for example: 10.155.155.1&6550:<br>123<br>comment  ( Short description of the item.<br>string)<br>**----- End of picture text -----**<br>

956 

**==> picture [516 x 536] intentionally omitted <==**

**----- Start of picture text -----**<br>
disabled  ( Defines whether an item is ignored or used.<br>yes | no)<br>export- The setting is used to tag BGP NLRI with one or more route targets which on the remote side is used by  import-route-targets .<br>route-<br>target  (list<br>of RTs)<br>import- The setting is used to determine if BGP NLRI is related to a particular VPLS, by comparing route targets received from BGP NLRI.<br>route-<br>targets  (lis<br>t of RTs)<br>local-pref  (<br>integer[0..<br>42949672<br>95])<br>name  (stri<br>ng;<br>Default: )<br>pw- Enables/disables Control Word usage. Read more in the VPLS Control Word article.<br>control-<br>word  (defa<br>ult |<br>disabled |<br>enabled)<br>pw-l2mtu  ( Advertised pseudowire MTU value.<br>integer<br>[32..<br>65535])<br>pw-type  (r The parameter is available starting from v5.16. It allows choosing advertised encapsulation in NLRI used only for comparison. It does not<br>aw- affect the functionality of the tunnel.  See pw-type usage example >><br>ethernet |<br>tagged-<br>ethernet |<br>vpls)<br>rd  (string) Specifies the value that gets attached to VPLS NLRI so that receiving routers can distinguish advertisements that may otherwise look the<br>same. This implies that a unique route-distinguisher for every VPLS must be used. It is not necessary to use the same route distinguisher<br>for some VPLS on all routers forming that VPLS as distinguisher is not used for determining if some BGP NLRI is related to a particular<br>VPLS (Route Target attribute is used for this), but it is mandatory to have different distinguishers for different VPLSes. Accepts 3 types of<br>formats. Read more>><br>site-id  (int Unique site identifier. Each site must have a unique site-id. A parameter must be set for RFC 4761 style VPLS signaling.<br>eger [0..<br>65535])<br>vrf  (name) Name of the VRF table.<br>**----- End of picture text -----**<br>
