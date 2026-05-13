## Properties 

**==> picture [516 x 230] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>add-default-route  (y Whether to install default route in routing table received from DHCP server. By default, the RouterOS client complies with RFC<br>es | no | special- and ignores option 3 if classless option 121 is received. To force the client not to ignore option 3 set special-classless. This<br>classless; Default:  y parameter is available in v6rc12+<br>es )<br>yes  - adds classless route if received, if not then add default route (old behavior)<br>special-classless  - adds both classless routes if received and a default route (MS style)<br>allow-reconfigure  (y Allows to receive Reconfigure (forcerenew) message from DHCP server. For changes in existing dhcp-client, renew the lease.<br>es | no; Default:  no )<br>check-gateway  (non Method on how to check route gateway reachability.<br>e | arp | bgd | ping ;<br>Default:  none)<br>client-id  (string;  Corresponds to the settings suggested by the network administrator or ISP. If not specified, the client's MAC address will be sent<br>Default: )<br>comment  (string;  Short description of the client<br>Default: )<br>**----- End of picture text -----**<br>


884 

**==> picture [516 x 676] intentionally omitted <==**

**----- Start of picture text -----**<br>
default-route-tables List of routing tables to which default route must be added. Table name can be proceeded with ":x" where x would be the<br>(table:distance;  distance for the route to be installed with.<br>Default: main)<br>default-route- Default route distance.<br>distance  (integer:0..<br>255; Default: )<br>disabled  (yes | no;  Whether client is disabled.<br>Default:  yes )<br>dscp  (integer:0..63;  Sets the DSCP (Differentiated Services Code Point) value for outgoing DHCP client packets. This value is part of the IP header<br>Default: ) 0 and is used to indicate the desired Quality of Service (QoS) level for network traffic.<br>host-name  (string;  The hostname of the client is sent to a DHCP server. If not specified, the client's system identity will be used.<br>Default: )<br>interface  (string;  The interface on which the DHCP client will be running.<br>Default: )<br>script  (script;  Execute script when DHCP client obtains a new lease or loses an existing one, received gateway address or DNS server list is<br>Default: ) changed.<br>Variables that are accessible for the event script:<br>bound - 1 - lease is added/changed; 0 - lease is removed<br>server-address - server address<br>lease-address - lease address provided by a server<br>interface - name of the interface on which the client is configured<br>gateway-address - gateway address provided by a server<br>vendor-specific - stores value of option 43 received from DHCP server<br>lease-options - an array of received options<br>Example >><br>use-broadcast  (alwa Whether to set broadcast bit in DHCPDISCOVER and DHCPREQUEST messages.<br>ys both never|  |  ;<br>Default:  both ) always - broadcast bit is set always<br>both - broadcast bit is set only first 15 seconds<br>always - broadcast bit is not set<br>use-peer-dns  (yes |  Whether to accept the DNS settings advertised by DHCP Server. (Will override the settings put in the  /ip dns  submenu.<br>no; Default:  yes )<br>use-peer-ntp  (yes |  Whether to accept the NTP settings advertised by DHCP Server. (Will override the settings put in the  /system ntp client<br>no; Default:  yes ) submenu)<br>vlan-priority  (integer If the DHCP client is running on a VLAN interface (/interface/vlan), you can specify the Priority Code Point (PCP) value. PCP is a<br>:0..7; Default: ) 0 3-bit field in the VLAN header used to mark the priority of packets within a VLAN, allowing traffic to be prioritized accordingly. This<br>setting applies only to VLAN interfaces and affects the priority of outgoing DHCP client packets.<br>Read-only properties<br>Property Description<br>address  (IP/Netmask) IP address and netmask, which is assigned to DHCP Client from the Server<br>dhcp-server  (IP) The IP address of the DHCP server.<br>expires-after  (time) A time when the lease expires (specified by the DHCP server).<br>gateway  (IP) The IP address of the gateway which is assigned by the DHCP server<br>invalid  (yes | no) Shows whether a configuration is invalid.<br>netmask  (IP)<br>**----- End of picture text -----**<br>


885 

**==> picture [516 x 154] intentionally omitted <==**

**----- Start of picture text -----**<br>
primary-dns  (IP) The IP address of the first DNS resolver, which was assigned by the DHCP<br>server<br>primary-ntp  (IP) The IP address of the primary NTP server, assigned by the DHCP server<br>secondary-dns  (IP) The IP address of the second DNS resolver, assigned by the DHCP server<br>secondary-ntp  (IP) The IP address of the secondary NTP server, assigned by the DHCP server<br>status  (bound | error | rebinding... | requesting... | searching... |  Shows the status of the DHCP Client<br>stopped)<br>reconfigure-key  (string) Reconfiguration authentication key<br>reconfigure-last-counter  (time) Count of recieved Recongure (forcerenew) messages<br>**----- End of picture text -----**<br>


Menu specific commands 

**==> picture [516 x 82] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>release  (nu Release current binding and restart the DHCP client<br>mbers)<br>renew  (num Renew current leases. If the renewal operation was not successful, the client tries to reinitialize the lease (i.e. it starts the lease request<br>bers) procedure (rebind) as if it had not received an IP address yet)<br>**----- End of picture text -----**<br>
