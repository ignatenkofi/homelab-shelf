## VLAN Table 

The VLAN table supports 4096 VLAN entries for storing VLAN member information as well as other VLAN information such as QoS, isolation, forced VLAN, learning, and mirroring. 

Sub-menu: `/interface ethernet switch vlan` 

**==> picture [507 x 254] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (yes | no; Default: no ) Indicate whether the VLAN entry is disabled. Only enabled entry is applied to the lookup process and forwarding<br>decision.<br>flood  (yes | no; Default: no ) Enables or disables forced VLAN flooding per VLAN. If the feature is<br>enabled, the result of the destination MAC lookup in the UFDB or MFDB is ignored,<br>and the packet is forced to flood in the VLAN.<br>ingress-mirror  (yes | no; Default: Enable the ingress mirror per VLAN to support the VLAN-based mirror function.<br>no )<br>learn  (yes | no; Default: yes ) Enables or disables source MAC learning for VLAN.<br>ports  (ports) Member ports of the VLAN.<br>qos-group  (none; Default: none ) Defined QoS group from QoS group menu.<br>svl  (yes | no; Default: no ) FDB lookup mode for lookup in UFDB and MFDB.<br>Shared VLAN Learning (svl) - learning/lookup is based on MAC addresses - not on VLAN IDs.<br>Independent VLAN Learning (ivl) - learning/lookup is based on both MAC addresses and VLAN IDs.<br>vlan-id  (0..4095) VLAN ID of the VLAN member entry.<br>**----- End of picture text -----**<br>
