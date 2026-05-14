## `/routing/igmp-proxy/interface` 

Configure what interfaces will participate as IGMP proxy interfaces on the router. If an interface is not configured as an IGMP proxy interface, then all IGMP traffic received on it will be ignored. 

**==> picture [516 x 162] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>alternative- By default, only packets from directly attached subnets are accepted. This parameter can be used to specify a list of alternative<br>subnets  (IP/Mask; valid packet source subnets, both for data or IGMP packets. Has an effect only on the upstream interface. Should be used when the<br>Default: ) source of multicast data often is in a different IP network.<br>interface  (name;  Name of the interface.<br>Default:  all )<br>threshold  (intege Minimal TTL. Packets received with a lower TTL value are ignored<br>r: 0..4294967295;<br>Default: ) 1<br>upstream  (yes |  The interface is called "upstream" if it's in the direction of the root of the multicast tree. An IGMP forwarding router must have<br>no; Default:  no ) exactly one upstream interface configured. The upstream interface is used to send out IGMP membership requests.<br>**----- End of picture text -----**<br>

**==> picture [516 x 162] intentionally omitted <==**

**----- Start of picture text -----**<br>
It is possible to get detailed status information for each interface using the  print status  command.<br>[admin@MikroTik] /routing igmp-proxy interface print status<br>Flags: X - disabled, I - inactive, D - dynamic; U - upstream<br> 0  U interface=ether2 threshold=1 alternative-subnets="" upstream=yes source-ip-address=192.168.10.10 rx-<br>bytes=3018487500 rx-packets=2012325 tx-bytes=0 tx-packets=0<br> 1    interface=ether3 threshold=1 alternative-subnets="" upstream=no querier=yes source-ip-address=192.<br>168.20.10 rx-bytes=0 rx-packets=0 tx-bytes=2973486000 tx-packets=1982324<br> 2    interface=ether4 threshold=1 alternative-subnets="" upstream=no querier=yes source-ip-address=192.<br>168.30.10 rx-bytes=0 rx-packets=0 tx-bytes=152019000 tx-packets=101346<br>Read-only Property Description<br>**----- End of picture text -----**<br>

966 

**==> picture [377 x 114] intentionally omitted <==**

**----- Start of picture text -----**<br>
querier  (read-only; yes|no) Whether the interface is acting as an IGMP querier.<br>source-ip-address  (read-only; IP address) The detected source IP for the interface.<br>rx-bytes  (read-only; integer) The total amount of received multicast traffic on the interface.<br>rx-packet  (read-only; integer) The total amount of received multicast packets on the interface.<br>tx-bytes  (read-only; integer) The total amount of transmitted multicast traffic on the interface.<br>tx-packet  (read-only; integer) The total amount of transmitted multicast packets on the interface.<br>**----- End of picture text -----**<br>
