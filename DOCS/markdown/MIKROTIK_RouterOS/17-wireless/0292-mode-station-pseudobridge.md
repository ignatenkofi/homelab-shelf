## Mode station-pseudobridge 

From the wireless connection point of view, this mode is the same as standard station mode. It has limited support for L2 bridging by means of some services implemented in station: 

- MAC address translation for IPv4 packets - station maintains IPv4-to-MAC mapping table and replaces source MAC address with its own address when sending frame to AP (in order to be able to use 3 address frame format), and replaces destination MAC address with address from mapping table for frames received from AP. IPv4-to-MAC mappings are built also for VLAN encapsulated frames. 

- single MAC address translation for the rest of protocols - station learns source MAC address from first forwarded non-IPv4 frame and uses it as default for reverse translation - this MAC address is used to replace destination MAC address for frames received from AP if IPv4-to-MAC mapping can not be performed (e.g. - non-IPv4 frame or missing mapping). 

This mode is limited to complete L2 bridging of data to single device connected to station (by means of single MAC address translation) and some support for IPv4 frame bridging - bridging of non-IP protocols to more than one device will not work. Also MAC address translation limits access to station device from AP side to IPv4 based access - the rest of protocols will be translated by single MAC address translation and will not be received by station itself. 

1536 

This mode is available for all protocols except nv2 and should be avoided when possible . The usage of this mode can only be justified if AP does not support better mode for L2 bridging (e.g. when non-RouterOS AP is used) or if only one end-user device must be connected to network by means of station device.
