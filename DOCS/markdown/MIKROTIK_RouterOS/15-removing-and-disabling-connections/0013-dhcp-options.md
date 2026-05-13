## DHCP Options 

DHCP client has the possibility to set up options that are sent to the DHCP server. For example, hostname and MAC address. The syntax is the same as for DHCP server options. 

Currently, there are three variables that can be used in options: 

HOSTNAME; 

CLIENT_MAC - client interface MAC address; 

- CLIENT_DUID - client DIUD of the router, same as used for the DHCPv6 client. In conformance with RFC4361 

DHCP client default options include these default Options: 

**==> picture [225 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Name code value<br>clientid_duid 61 0xff$(CLIENT_DUID)<br>clientid 61 0x01$(CLIENT_MAC)<br>hostname 12 $(HOSTNAME)<br>**----- End of picture text -----**<br>
