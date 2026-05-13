## `/routing/ospf/static-neighbor` 

Static configuration of the OSPF neighbors. Required for non-broadcast multi-access networks. 

**==> picture [516 x 179] intentionally omitted <==**

**----- Start of picture text -----**<br>
Read-only Property Description<br>address  (IP%iface; ma The unicast IP address and an interface, that can be used to reach the IP of the neighbor. For example,  address=1.2.3.4%<br>ndatory ) ether1  indicates that a neighbor with IP 1.2.3.4 is reachable on the ether1 interface.<br>area  (name; mandatory Name of the area the neighbor belongs to.<br>)<br>comment  (string)<br>disabled  (yes | no)<br>instance-id  (integer [0.<br>.255]; Default: 0)<br>poll-interval  (time;  How often to send hello messages to the neighbors which are in a "down" state (i.e. there is no traffic from them)<br>Default: 2m )<br>**----- End of picture text -----**<br>


974
