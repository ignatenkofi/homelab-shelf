## Sub-menu: `/ipv6 dhcp-server binding` 

DUID is used only for dynamic bindings, so if it changes then the client will receive a different prefix than previously. 

**==> picture [516 x 310] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IPv6  IPv6 prefix that will be assigned to the client<br>prefix; Default: )<br>allow-dual-stack- Creates a single simple queue entry for both IPv4 and IPv6 addresses, uses the MAC address and DUID for identification. Requires I<br>queue  (yes | no;  Pv4 DHCP Server to have this option enabled as well to work properly.<br>Default: yes )<br>comment  (string; Short description of an item.<br>Default: )<br>disabled  (yes |  Whether an item is disabled<br>no; Default: no )<br>dhcp-option  (stri Add additional DHCP options from the option list.<br>ng; Default: )<br>dhcp-option-set  ( Add an additional set of DHCP options.<br>string; Default: )<br>life-time  (time;  The time period after which binding expires.<br>Default: 3d )<br>duid  (hex string;  DUID value. Should be specified only in hexadecimal format.<br>Default: )<br>iaid  (integer [0.. Identity Association Identifier, part of the Client ID.<br>4294967295];<br>Default: )<br>**----- End of picture text -----**<br>

906 

prefix-pool (string Prefix pool that is being advertised to the DHCPv6 Client. ; Default: ) rate-limit (integer Adds a dynamic simple queue to limit IP's bandwidth to a specified rate. Requires the lease to be static. Format is: rx-rate[/tx-rate] [rx[/integer] [integer burst-rate[/tx-burst-rate] [rx-burst-threshold[/tx-burst-threshold] [rx-burst-time[/tx-burst-time]]]]. All rates should be numbers with [/integer] [integer optional 'k' (1,000s) or 'M' (1,000,000s). If tx-rate is not specified, rx-rate is as tx-rate too. Same goes for tx-burst-rate and tx-burst[/integer] [integer threshold and tx-burst-time. If both rx-burst-threshold and tx-burst-threshold are not specified (but burst-rate is specified), rx-rate and [/integer]]]]; tx-rate is used as burst thresholds. If both rx-burst-time and tx-burst-time are not specified, 1s is used as default. Default: ) server (string | Name of the server. If set to all , then binding applies to all created DHCP-PD servers. all; Default: all )
