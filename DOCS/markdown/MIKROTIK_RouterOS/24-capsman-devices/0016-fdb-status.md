## FDB Status 

**==> picture [516 x 256] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>mac-address  (MAC address) MAC address corresponding for this FDB entry<br>seq-number  (integer) sequence number used in routing protocol to avoid loops<br>type  (integer) sequence number used in routing protocol to avoid loops<br>interface  (local | outsider | direct | mesh |  type of this FDB entry<br>neighbor | larval | unknown)<br>local -- MAC address belongs to the local router itself<br>outsider -- MAC address belongs to a device external to the mesh network<br>direct -- MAC address belongs to a wireless client on an interface that is in the mesh network<br>mesh -- MAC address belongs to a device reachable over the mesh network; it can be either<br>internal or external to the mesh network<br>neighbor -- MAC address belongs to a mesh router that is a direct neighbor to this router<br>larval -- MAC address belongs to an unknown device that is reachable over the mesh network<br>unknown -- MAC address belongs to an unknown device<br>mesh  (interface name) the mesh interface this FDB entry belongs to<br>on-interface  (interface name) mesh port used for traffic forwarding, kind of a next-hop value<br>lifetime  (time) time remaining to live if this entry is not used for traffic forwarding<br>**----- End of picture text -----**<br>


1493 

age (time) metric (integer 

) 

age of this FDB entry a metric value used by routing protocol to determine the 'best' path
