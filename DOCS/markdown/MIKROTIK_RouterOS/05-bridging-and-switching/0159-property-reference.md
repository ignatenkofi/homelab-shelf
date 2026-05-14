## Property Reference 

Sub-menu: `/interface/macvlan` 

Configuration settings for the MACVLAN interface. 

Property Description 

456 

**==> picture [516 x 499] intentionally omitted <==**

**----- Start of picture text -----**<br>
arp  (disabled | enabled |  Address Resolution Protocol setting<br>local-proxy-arp | proxy-arp |<br>reply-only; Default: enabled ) disabled  - the interface will not use ARP<br>enabled  - the interface will use ARP<br>local-proxy-arp  -  the router performs proxy ARP on the interface and sends replies to the same interface<br>proxy-arp  - the router performs proxy ARP on the interface and sends replies to other interfaces<br>reply-only  - the interface will only reply to requests originating from matching IP address/MAC address<br>combinations, which are entered as static entries in the IP/ARP table. No dynamic entries will be automatically<br>stored in the IP/ARP table. Therefore, for communications to be successful, a valid static entry must already exist.<br>arp-timeout  (auto | integer;  Sets for how long the ARP record is kept in the ARP table after no packets are received from IP. Value auto equals to<br>Default: auto ) the value of arp-timeout in /ip/settings/ , default is 30s.<br>comment  (string; Default: ) Short description of the interface.<br>disabled  (yes | no; Default: Changes whether the interface is disabled.<br>no )<br>interface  (name; Default: ) The name of the underlying interface on which the MACVLAN will operate. MACVLAN interfaces can be created on any<br>interface that has a MAC address.<br>Adding a VLAN interface on top of a MACVLAN interface is not supported.<br>Adding MACVLAN on interface which is already bridged or bonded is not supported.<br>loop-protect  (on | off |  Enables or disables loop protect on the interface, the default works as turned off.<br>default; Default: default )<br>loop-protect-disable-time  (ti Sets how long the selected interface is disabled when a loop is detected. 0 - forever.<br>me interval | 0; Default: 5m )<br>loop-protect-send-interval  (ti Sets how often loop protect packets are sent on the selected interface.<br>me interval; Default: 5s )<br>mac-address  (MAC;  Static MAC address of the interface. A randomly generated MAC address will be assigned when not specified.<br>Default: )<br>mode  (private | bridge;  Sets MACVLAN interface mode:<br>Default:  bridge )<br>private  - does not allow communication between MACVLAN instances on the same parent  interface .<br>bridge  - allows communication between MACVLAN instances on the same parent  interface .<br>mtu  (integer; Default: 1500 ) Sets Layer 3 Maximum Transmission Unit. For the MACVLAN interface, it cannot be higher than the parent  interface .<br>name  (string; Default: ) Interface name.<br>**----- End of picture text -----**<br>

457
