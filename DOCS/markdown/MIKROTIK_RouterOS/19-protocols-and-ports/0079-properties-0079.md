## Properties 

**==> picture [516 x 120] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (none | string; Default: ) Single IP address for the initiator instead of specifying a whole address pool.<br>address-pool  (none | string;  Name of the address pool from which the responder will try to assign address if mode-config is enabled.<br>Default: )<br>address-prefix-length  (integer  Prefix length (netmask) of the assigned address from the pool.<br>[1..32]; Default: )<br>comment  (string; Default: )<br>**----- End of picture text -----**<br>


1201 

**==> picture [516 x 165] intentionally omitted <==**

**----- Start of picture text -----**<br>
name  (string; Default: )<br>responder  (yes | no; Default:  no ) Specifies whether the configuration will work as an initiator (client) or responder (server). The initiator will request for<br>mode-config parameters from the responder.<br>split-dns List of DNS names that will be resolved using a system-dns=yes or static-dns= setting.<br>split-include  (list of IP prefix;  List of subnets in CIDR format, which to tunnel. Subnets will be sent to the peer using the CISCO UNITY extension, a<br>Default: ) remote peer will create specific dynamic policies.<br>src-address-list  (address list;  Specifying an address list will generate dynamic source NAT rules. This parameter is only available with<br>Default: ) responder=no. A roadWarrior client with NAT<br>static-dns  (list of IP; Default: ) Manually specified DNS server's IP address to be sent to the client.<br>system-dns  (yes | no; Default: ) When this option is enabled DNS addresses will be taken from  /ip dns .<br>**----- End of picture text -----**<br>
