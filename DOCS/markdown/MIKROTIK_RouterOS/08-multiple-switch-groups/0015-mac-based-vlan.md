## MAC Based VLAN 

MAC Based VLAN table is used to assign VLAN based on the source MAC. 

Sub-menu: `/interface ethernet switch mac-based-vlan` 

**==> picture [507 x 120] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (yes | no; Default: no ) Enables or disables MAC Based VLAN entry.<br>new-customer-vid  (0..4095;  The new customer VLAN ID replaces the original service VLAN ID for matched packets. If set to 4095, then<br>Default: 0 ) traffic is dropped.<br>new-service-vid  (0..4095; Default: 0 The new service VLAN ID replaces the original service VLAN ID for matched packets.<br>)<br>src-mac-address  (MAC address) Matching source MAC address for MAC based VLAN rule.<br>**----- End of picture text -----**<br>


424 

**==> picture [13 x 13] intentionally omitted <==**

All CRS1xx/2xx series switches support up to 1024 MAC Based VLAN table entries.
