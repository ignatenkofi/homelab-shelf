## Sub-menu: `/interface/ethernet/switch/qos/map/vlan` 

Matches VLAN priorities (802.1p PCP/DEI fields) to QoS profiles. By default, all values are matched to the default QoS profile. 

**==> picture [346 x 99] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>dei-only  (yes | no; Default:  no ) Map only packets with DEI (formerly CFI) bit set in the VLAN header.<br>map  (name; Default:  default ) The name of the mapping table.<br>profile  (name; Default: ) The name of the QoS profile to assign to the matched packets.<br>pcp  (range: 0..7; Default: ) 0 VLAN priority (PCP) value(-s) for the lookup.<br>**----- End of picture text -----**<br>
