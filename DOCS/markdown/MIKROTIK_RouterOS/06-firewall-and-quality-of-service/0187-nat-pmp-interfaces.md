## NAT PMP Interfaces 

Available from `/ip nat-pmp interfaces` menu. 

**==> picture [447 x 117] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>interface  (string; Default: ) Interface name on which PMP will be running on<br>type  (external | internal; Default: no ) PMP interface type:<br>external  - the interface a global IP address is assigned to<br>internal  - router's local interface the clients are connected to<br>forced-ip  (Ip; Default: ) Allow specifying what public IP to use if the external interface has more than one IP available.<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

In more complex setups with VLANs, where the VLAN interface is part of the LAN, for PMP to work properly, the VLAN interface itself should be specified as the internal interface. 

755
