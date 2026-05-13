## Sub-menu: `/interface bridge port` 

**==> picture [502 x 125] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>frame-types  (admit-all | admit- Specifies allowed ingress frame types on a bridge port. This property only has an effect when  vlan-filtering<br>only-untagged-and-priority- is set to yes .<br>tagged | admit-only-vlan-tagged;<br>Default: admit-all )<br>ingress-filtering  (yes | no;  Enables or disables VLAN ingress filtering, which checks if the ingress port is a member of the received VLAN<br>Default: yes ) ID in the bridge VLAN table. Should be used with frame-types to specify if the ingress traffic should be tagged<br>or untagged. This property only has effect when vlan-filtering is set to yes . The setting is enabled by<br>default since RouterOS v7.<br>**----- End of picture text -----**<br>


373 

pvid (integer 1..4094; Default: 1 ) Port VLAN ID (pvid) specifies which VLAN the untagged ingress traffic is assigned to. This property only has an effect when `vlan-filtering` is set to `yes` . tag-stacking (yes | no; Default: no Forces all packets to be treated as untagged packets. Packets on ingress port will be tagged with another VLAN ) tag regardless if a VLAN tag already exists, packets will be tagged with a VLAN ID that matches the `pvid` value and will use EtherType that is specified in `ether-type` . This property only has effect when `vlan-filtering` i s set to `yes` .
