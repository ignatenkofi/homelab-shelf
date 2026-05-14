## Interface settings 

Sub-menu: `/interface/macsec` 

Configuration settings for the MACsec interface. 

**==> picture [516 x 235] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>cak  (string; Default: ) A 16-byte pre-shared connectivity association key (CAK). To enable MACsec, configure the matching CAK and<br>CKN on both ends of the link. When not specified, RouterOS will automatically generate a random value.<br>ckn  (string; Default: ) A 32-byte connectivity association name (CKN). To enable MACsec, configure the matching CAK and CKN on<br>both ends of the link. When not specified, RouterOS will automatically generate a random value.<br>comment  (string; Default: ) Short description of the interface.<br>disabled  (yes | no; Default: no ) Changes whether the interface is disabled.<br>interface  (name; Default: ) Ethernet interface name where MACsec is created on, limited to one MACsec interface per Ethernet.<br>mtu  (integer; Default: 1468 ) Sets the maximum transmission unit. The l2mtu will be set automatically according to the associated interfa<br>ce (subtracting 32 bytes corresponding to the MACsec encapsulation). The l2mtu cannot be changed.<br>name  (string; Default: macsec1 ) Name of the interface.<br>profile  (name; Default: default ) Sets MACsec profile, used for determining the key server in a point-to-point connection.<br>status  (read-only: disabled |initializing Shows the current MACsec interface status.<br>| invalid | negotiating | open-encrypted)<br>**----- End of picture text -----**<br>

454
