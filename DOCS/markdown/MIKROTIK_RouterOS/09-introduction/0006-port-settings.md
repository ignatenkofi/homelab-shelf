## Port Settings 

Properties under this menu are used to configure VLAN switching and filtering options for switch chips that support a VLAN Table. These properties are only available to switch chips that have VLAN Table support, check the Switch Chip Features table to make sure your device supports such a feature. 

**==> picture [13 x 13] intentionally omitted <==**

Ingress traffic is considered as traffic that is being sent IN a certain port, this port is sometimes called ingress port . Egress traffic is considered as traffic that is being sent OUT of a certain port, this port is sometimes called egress port . Distinguishing them is very important to properly set up VLAN filtering since some properties apply only to either ingress or egress traffic. 

**==> picture [516 x 154] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>vlan-mode  (check |  Changes the VLAN lookup mechanism against the VLAN Table for ingress traffic.<br>disabled | fallback |<br>secure; Default: disab disabled  - disables checking against the VLAN Table completely for ingress traffic. No traffic is dropped when set on the<br>led ) ingress port.<br>fallback  - checks tagged traffic against the VLAN Table for ingress traffic and forwards all untagged traffic. If ingress<br>traffic is tagged and the egress port is not found in the VLAN table for the appropriate VLAN ID, then traffic is dropped. If a<br>VLAN ID is not found in the VLAN Table, then traffic is forwarded. Used to allow known VLANs only in specific ports.<br>check  - checks tagged traffic against the VLAN Table for ingress traffic and drops all untagged traffic. If ingress traffic is<br>tagged and the egress port is not found in the VLAN table for the appropriate VLAN ID, then traffic is dropped.<br>secure  - checks tagged traffic against the VLAN Table for ingress traffic and drops all untagged traffic. Both ingress and<br>egress port must be found in the VLAN Table for the appropriate VLAN ID, otherwise, traffic is dropped.<br>**----- End of picture text -----**<br>


483 

vlan-header (add-ifSets action which is performed on the port for egress traffic. missing | always-strip | leave-as-is; Default: `add-if-missing` - adds a VLAN tag on egress traffic and uses default-vlan-id from the ingress port. Should be used for leave-as-is ) trunk ports. `always-strip` - removes a VLAN tag on egress traffic. Should be used for access ports. `leave-as-is` - does not add nor remove a VLAN tag on egress traffic. Should be used for hybrid ports. default-vlan-id (auto | Adds a VLAN tag with the specified VLAN ID on all untagged ingress traffic on a port, should be used with vlan-header set to `al` integer: 0..4095; `ways-strip` on a port to configure the port to be the access port. For hybrid ports default-vlan-id is used to tag untagged Default: auto ) traffic. If two ports have the same default-vlan-id, then VLAN tag is not added since the switch chip assumes that traffic is being forwarded between access ports. 

**==> picture [13 x 13] intentionally omitted <==**

On QCA8337 and Atheros8327 switch chips, a default `vlan-header=leave-as-is` property should be used. The switch chip will determine which ports are access ports by using the `default-vlan-id` property. The `default-vlan-id` should only be used on access/hybrid ports to specify which VLAN the untagged ingress traffic is assigned to.
