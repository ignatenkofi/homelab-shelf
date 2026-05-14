## Sub-menu: `/interface bridge nat` 

**==> picture [502 x 139] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>action  (accept | drop | jump | mark-packet | redirect | set- Action to take if the packet is matched by the rule:<br>priority | arp-reply | dst-nat | log | passthrough | return |<br>src-nat; Default: accept ) accept - accept the packet. No action, i.e., the packet is passed through without<br>undertaking any action, and no more rules are processed in the relevant list/chain<br>arp-reply - send a reply to an ARP request (any other packets will be ignored by<br>this rule) with the specified MAC address (only valid in dstnat chain)<br>drop - silently drop the packet (without sending the ICMP reject message)<br>dst-nat - change destination MAC address of a packet (only valid in dstnat chain)<br>jump - jump to the chain specified by the value of the jump-target argument<br>log - log the packet<br>**----- End of picture text -----**<br>

392 

mark - mark the packet to use the mark later 

passthrough - ignore this rule and go on to the next one. Acts the same way as a disabled rule, except for the ability to count packets redirect - redirect the packet to the bridge itself (only valid in dstnat chain) return - return to the previous chain, from where the jump took place set-priority - set priority specified by the new-priority parameter on the packets sent out through a link that is capable of transporting priority (VLAN or WMMenabled wireless interface). Read more 

src-nat - change source MAC address of a packet (only valid in srcnat chain) to-arp-reply-mac-address (MAC address; Default: ) Source MAC address to put in Ethernet frame and ARP payload, when `action=arpreply` is selected to-dst-mac-address (MAC address; Default: ) Destination MAC address to put in Ethernet frames, when `action=dst-nat` is selected to-src-mac-address (MAC address; Default: ) Source MAC address to put in Ethernet frames, when `action=src-nat` is selected
