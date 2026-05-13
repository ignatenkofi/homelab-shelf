## MLAG settings and monitoring 

This section describes the available MLAG settings and monitoring options. 

Sub-menu: `/interface bridge mlag` 

Property Description 

780 

**==> picture [516 x 523] intentionally omitted <==**

**----- Start of picture text -----**<br>
bridge  (interface; D The bridge interface where MLAG is being created.<br>efault:  none )<br>heartbeat  (time: 1s.. This setting controls how often heartbeat messages are sent to check the connection between peers. If no heartbeat message is<br>10s | none; Default:  received for three intervals in a row, the peer logs a warning about potential communication problems. If set to  none , heartbeat<br>00:00:05 ) messages are not sent at all.<br>peer-port  (interface An interface that will be used as a peer port. Both peer devices are using inter-chassis communication over these peer ports to<br>; Default:  none ) establish MLAG and update the host table. Peer port should be isolated on a different untagged VLAN using a  pvid  setting. Peer<br>port can be configured as a bonding interface.<br>priority  (integer: 0.. This setting changes the priority for selecting the primary MLAG node. A lower number means higher priority. If both MLAG nodes<br>128; Default:  128 ) have the same priority, the one with the lowest bridge MAC address will become the primary device.<br>Use the  monitor commands to see the current MLAG status.<br>[admin@Peer1] > /interface/bridge/mlag/monitor<br>       status: connected<br>    system-id: 74:4D:28:11:70:6B<br>  active-role: primary<br>The " not hw offloaded " error will appear under the /interface/bridge/mlag menu if the peer-port does not use Layer 2 hardware offloading.<br>MLAG setup must be done where both the peer-port and bonded ports (using  mlag-id  property) are using hardware offloading. Using ports<br>that do not support hardware offloading (e.g., management interfaces) can lead to undefined behavior.<br>Property Description<br>status  (connected The MLAG status.<br>| connecting |<br>disabled)<br>system-id  (MAC  The lowest MAC address between both peer bridges will be used as the  system-id . This  system-id  is used for (R/M)STP BPDU<br>address) bridge identifier and LACP system ID.<br>active-role  (primar The peer with the lowest  priority  will act as the primary device. If the priorities are the same, the peer with the lowest bridge<br>y | secondary) MAC address will become the primary. The  system-id  of the primary device is used for sending the (R/M)STP BPDU bridge<br>identifier and LACP system ID.<br>Sub-menu: /interface bonding<br>Property Description<br>mlag-id  (integer: 0.. Changes MLAG ID for bonding interface. The same MLAG ID should be used on both peer devices to successfully create a<br>4294967295; Default:) single LAG for the client device. The  peer-port should not be configured with the MLAG ID.<br>**----- End of picture text -----**<br>


LACP bonding interface and bonding slave ports can be monitored with `monitor` and `monitor-slaves` commands. See more details on Bonding monitoring. 

781
