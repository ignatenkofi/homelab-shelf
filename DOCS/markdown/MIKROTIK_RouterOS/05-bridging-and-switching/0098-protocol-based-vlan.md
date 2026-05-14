## Protocol Based VLAN 

Protocol Based VLAN table is used to assign VID and QoS attributes to related protocol packets per port. 

Sub-menu: `/interface ethernet switch protocol-based-vlan` 

**==> picture [507 x 254] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (yes | no; Default: no ) Enables or disables Protocol Based VLAN entry.<br>frame-type  (ethernet | llc | rfc-1042; Default: ethernet ) Encapsulation type of the matching frames.<br>new-customer-vid  (0..4095; Default: 0 ) The new customer VLAN ID replaces the original customer VLAN ID for the specified<br>protocol. If set to 4095, then traffic is dropped.<br>new-service-vid  (0..4095; Default: 0 ) The new service VLAN ID replaces the original service VLAN ID for the specified protocol.<br>ports  (ports) Matching switch ports for Protocol-based VLAN rule.<br>protocol  (protocol; Default: 0 ) Matching protocol for Protocol-based VLAN rule.<br>qos-group  (none; Default: none ) Defined QoS group from QoS group menu.<br>set-customer-vid-for  (all | none | tagged | untagged-or- Customer VLAN ID assignment command for different packet types.<br>priority-tagged; Default: all )<br>set-qos-for  (all | none | tagged | untagged-or-priority- Frame type for which QoS assignment command applies.<br>tagged; Default: none )<br>set-service-vid-for  (all | none | tagged | untagged-or- Service VLAN ID assignment command for different packet types.<br>priority-tagged; Default: all )<br>**----- End of picture text -----**<br>
