## `/routing/bgp/vpn` 

L3VPN VPNv4/VPNv6 instance configuration 

**==> picture [516 x 103] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (yes | no)<br>export  - a group of parameters associated with the vpnv4 export<br>.filter-chain  (name) The name of the routing filter chain that is used to filter prefixes before exporting.<br>.filter-select (name) The name of the select filter chain that is used to select prefixes to be exported exporting.<br>**----- End of picture text -----**<br>

957 

**==> picture [516 x 251] intentionally omitted <==**

**----- Start of picture text -----**<br>
.redistribute (bgp | connected | dhcp | fantasy |  Enable redistribution of specified route types from VRF to VPNv4.<br>modem | ospf | rip | static | vpn)<br>.route-targets (rt[,rt]) List of route targets added when exporting VPNv4 routes. The accepted RT format is similar<br>to the one for Route Distinguishers.<br>import  - a group of parameters associated with the vpnv4 import<br>.filter-chain  (name) The name of the routing filter chain that is used to filter prefixes during import.<br>.route-targets (rt[,rt]) List of route targets that will be used to import VPNv4 routes. The accepted RT format is<br>similar to the one for Route Distinguishers.<br>.router-id (name | ip) The router ID of the BGP instance that will be used for the BGP best path selection algorithm.<br>label-allocation-policy  (per-prefix | per-vrf)<br>name<br>route-distinguisher  (rd) Helps to distinguish between overlapping routes from multiple VRFs. Should be unique per<br>VRF. Accepts 3 types of formats. Read more>><br>vrf  (name) Name of the VRF table that this VPN instance will use.<br>instance  (name) Name of the instance this VPN is assigned to.<br>**----- End of picture text -----**<br>
