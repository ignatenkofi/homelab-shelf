## IPv6 Settings 

Sub-menu: `/ipv6 settings` 

**==> picture [13 x 13] intentionally omitted <==**

Changing /ipv6 settings will not dynamically remove the old SLAAC configuration present on your router. A reboot is required to apply the new settings. 

**==> picture [506 x 453] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>accept-redirects  (no | yes-if-forwarding- Whether to accept ICMP redirect messages. Typically should be enabled on the host and disabled on<br>disabled; Default: yes-if-forwarding-disabled ) routers<br>accept-router-advertisements  (no | yes | yes- Accept router advertisement (RA) messages. If enabled, the router will be able to get the address<br>if-forwarding-disabled; Default: yes-if- using stateless address configuration<br>forwarding-disabled )<br>accept-router-advertisements-on  (interface  Specifies on which interfaces to listen for incoming router advertisements (RAs).<br>list; Default:  all )<br>disable-ipv6  (yes | no; Default: no ) Enable/disable system wide IPv6 settings (prevents LL address generation)<br>forward  (yes | no; Default: yes ) Enable/disable packet forwarding between interfaces<br>max-neighbor-entries  (integer [0.. A maximum number or IPv6 neighbors. Since RouterOS version 7.1, the default value depends on<br>4294967295]; Default: ) the installed amount of RAM. It is possible to set a higher value than the default, but it increases the<br>risk of out-of-memory condition.<br>The default values for certain RAM sizes:<br>1024 for 64 MB,<br>2048 for 128 MB,<br>4096 for 256 MB,<br>8192 for 512 MB,<br>16384 for 1024 MB or higher.<br>multipath-hash-policy  (l3 | l4 | l3-inner;  IPv6 Hash policy used for ECMP routing in  /ipv6/settings  menu<br>Default: l3 )<br>l3 -- layer-3 hashing of src IP, dst IP, flow label, IP protocol<br>l3-inner -- layer-3 hashing or inner layer-3 hashing if available<br>l4 -- layer-4 hashing of src IP, dst IP, IP protocol, src port, dst port<br>disabled-link-local-address (no | yes ;  Disable automatic link-local address generation for non-VPN interfaces. This can be used when<br>Default: no) manually configured link-local addresses are being used.<br>stale-neighbor-timeout (time ; Default: 60) Timeout after which stale IPv6/Neighbor entries should be purged.<br>min-neighbor-entries (integer ; Default: 4096) Minimal number of IPv6/Neighbor entries, for which device must allocate memory.<br>soft-max-neighbor-entries (integer ; Default: Expected maximum number of IPv6/Neighbor entries which system should handle.<br>8192)<br>**----- End of picture text -----**<br>

192 

max-neighbor-entries (integer ; Default: 16 Maximum number of entries for IPv7/Neighbor list. 384 ) allow-fast-path (yes | no; Default: yes) Allows Fast Path. 

Read-Only Properties 

**==> picture [241 x 136] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>ipv6-fast-path-active  (yes | no) Indicates whether fast-path is active<br>ipv6-fast-path-bytes  (integer) Amount of fast-pathed bytes<br>ipv6-fast-path-packets  (integer) Amount of fast-pathed packets<br>ipv6-fasttrack-active  (yes | no) Indicates whether fasttrack is active<br>ipv6-fasttrack-bytes  (integer) Amount of fasttracked bytes<br>ipv6-fasttrack-packets  (integer) Amount of fasttracked packet.<br>**----- End of picture text -----**<br>

193
