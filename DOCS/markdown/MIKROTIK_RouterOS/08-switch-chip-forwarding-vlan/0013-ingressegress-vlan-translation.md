## Ingress/Egress VLAN Translation 

The Ingress VLAN Translation table allows for up to 15 entries for each port. One or multiple fields can be selected from the packet header for lookup in the Ingress VLAN Translation table. The S-VLAN or C-VLAN or both configured in the first matched entry are assigned to the packet. 

Sub-menu: `/interface ethernet switch ingress-vlan-translation` 

422 

Sub-menu: `/interface ethernet switch egress-vlan-translation` 

**==> picture [507 x 386] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>customer-dei  (0..1; Default: none ) Matching DEI of the customer tag.<br>customer-pcp  (0..7; Default: none ) Matching PCP of the customer tag.<br>customer-vid  (0..4095; Default: none ) Matching the VLAN ID of the customer tag.<br>customer-vlan-format  (any | priority-tagged-or-tagged |  Type of frames with customer tag for which VLAN translation rule is valid.<br>tagged | untagged-or-tagged; Default: any )<br>disabled  (yes | no; Default: no ) Enables or disables VLAN translation entry.<br>new-customer-vid  (0..4095; Default: none ) The new customer VLAN ID replaces the matching customer VLAN ID. If set to 4095<br>and ingress VLAN translation is used, then traffic is dropped.<br>new-service-vid  (0..4095; Default: none ) The new service VLAN ID replaces the matching service VLAN ID.<br>pcp-propagation  (yes | no; Default: no ) Enables or disables PCP propagation.<br>If the port type is Edge, the customer PCP is copied from the service PCP.<br>If the port type is Network, the service PCP is copied from the customer PCP.<br>ports  (ports) Matching switch ports for VLAN translation rule.<br>protocol  (protocols; Default: none ) Matching Ethernet protocol. (only for Ingress VLAN Translation)<br>sa-learning  (yes | no; Default: no ) Enables or disables source MAC learning after VLAN translation. (only for Ingress<br>VLAN Translation)<br>service-dei  (0..1; Default: none ) Matching DEI of the service tag.<br>service-pcp  (0..7; Default: none ) Matching PCP of the service tag.<br>service-vid  (0..4095; Default: none ) Matching VLAN ID of the service tag.<br>service-vlan-format  (any | priority-tagged-or-tagged |  Type of frames with service tag for which VLAN translation rule is valid.<br>tagged | untagged-or-tagged; Default: any )<br>**----- End of picture text -----**<br>


Below is a table of traffic that triggers a rule that has a certain VLAN format set, note that traffic that is tagged with VLAN ID 0 is a special case that is also taken into account. 

**==> picture [216 x 247] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>any Accepts:<br>Untagged traffic<br>Tagged traffic<br>Tagged traffic with priority set<br>VLAN 0 traffic<br>VLAN 0 traffic with priority set<br>priority-tagged-or-tagged Accepts:<br>Tagged traffic<br>Tagged traffic with priority set<br>VLAN 0 traffic<br>VLAN 0 traffic with priority set<br>tagged Accepts:<br>Tagged traffic<br>Tagged traffic with priority set<br>**----- End of picture text -----**<br>


423 

untagged-or-tagged Accepts: Untagged traffic Tagged traffic Tagged traffic with priority set If `VLAN-format` is set to `any` , then `customer-vid/service-vid` set to  will trigger the switch rule with VLAN 0 traffic. In this case, the `0` switch rule will be looking for untagged traffic or traffic with a VLAN 0 tag, and only `untagged-or-tagged` will filter out VLAN 0 traffic in this case.
