## Properties 

Property Description 

856 

**==> picture [506 x 456] intentionally omitted <==**

**----- Start of picture text -----**<br>
arp  (disabled | enabled | proxy-arp |  Address Resolution Protocol<br>reply-only; Default: enabled )<br>arp-timeout  (time interval | auto;<br>Default: auto)<br>bridge  (name; Default:)<br>bridge-cost  (integer [1..200000000];  Cost of the bridge port.<br>Default: )<br>bridge-horizon  (none | integer;  If set to none bridge horizon will not be used.<br>Default: none )<br>bridge-pvid  (integer 1..4094;  Used to assign port VLAN ID (pvid) for dynamically bridged interface. This property only has an effect when<br>Default: ) 1 bridge vlan-filtering is set to yes.<br>cisco-static-id  (integer [0.. Cisco-style VPLS tunnel ID.<br>4294967295]; Default: 0 )<br>comment  (string; Default: ) Short description of the item<br>disable-running-check  (yes | no;  Specifies whether to detect if an interface is running or not. If set to no interface will always have the  running<br>Default: no ) flag.<br>disabled  (yes | no; Default: yes ) Defines whether an item is ignored or used. By default VPLS interface is disabled.<br>mac-address  (MAC; Default: )<br>mtu  (integer [32..65536]; Default: 15<br>00 )<br>name  (string; Default: ) Name of the interface<br>pw-l2mtu  (integer [0..65536];  L2MTU value advertised to a remote peer.<br>Default: 1500 )<br>pw-type  (raw-ethernet | tagged- Pseudowire type.<br>ethernet | vpls; Default: raw-ethernet )<br>peer  (IP; Default: ) The IP address of the remote peer.<br>pw-control-word  (disabled | enabled  Enables/disables Control Word usage. Default values for regular and cisco style VPLS tunnels differ. Cisco<br>| default; Default: default ) style by default has control word usage disabled. Read more in the VPLS Control Word article.<br>vpls-id  (AsNum | AsIp; Default: ) A unique number that identifies the VPLS tunnel. Encoding is 2byte+4byte or 4byte+2byte number.<br>**----- End of picture text -----**<br>
