## Properties 

This section describes the ARP table configuration options. 

**==> picture [505 x 336] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IP;  IP address to be mapped<br>Default: )<br>interface  (string Interface name the IP address is assigned to<br>; Default: )<br>mac-address  ( MAC address to be mapped to<br>MAC; Default: 0<br>0:00:00:00:00:<br>00 )<br>published  (yes  Static proxy-arp entry for individual IP addresses. When an ARP query is received for the specific IP address, the device will<br>| no; Default: no ) respond with its own MAC address. No need to set proxy-arp on the interface itself for all the MAC addresses to be proxied. The<br>interface will respond to an ARP request only when the device has an active route towards the destination<br>Read-only properties:<br>Property Description<br>complete  (yes | no) Complete flag is included in ARP entries when the ARP  status  is permanent, reachable, stale, probe,<br>or delay<br>dhcp  (yes | no) Whether the ARP entry is added by DHCP server<br>disabled  (yes | no) Whether the ARP entry is disabled<br>dynamic  (yes | no) Whether the entry is dynamically created<br>invalid  (yes | no) Whether the entry is not valid<br>**----- End of picture text -----**<br>


Read-only properties: 

865 

status (delay | failed | incomplete | Shows the ARP entry state: permanent | probe | reachable | stale ) `delay` - neighbor entry validation is currently delayed `failed` - ARP resolution has failed, the system was not able to obtain the MAC address for the given IP address `incomplete` - system does not have the MAC address information for the IP address, it has not yet been resolved `permanent` - ARP entry is considered permanent and will not be removed from the table, even if it is not actively being used. This is set for manually configured ARP entries `probe` - neighbor is being probed `reachable` - ARP resolution is successful, and the MAC address associated with the IP address is know, the entry is valid until the reachability timeout expires `stale` - entry is still valid, but it is aged. This means that the system has not recently communicated with the device associated with the IP address. VRF (string) Indicates which VRF this ARP entry is associated with. 

**==> picture [13 x 13] intentionally omitted <==**

The default maximum number of ARP entries depends on the installed amount of RAM. It can be adjusted with the command " `/ip settings set max-neighbor-entries=` x", see more details on IPv4 Settings.
