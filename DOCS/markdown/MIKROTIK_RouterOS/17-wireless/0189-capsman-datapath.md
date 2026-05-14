## CAPsMAN datapath 

Datapath settings control data forwarding related aspects. On CAPsMAN datapath settings are configured in the datapath profile menu /caps-man datapath or directly in a configuration profile or interface menu as settings with datapath. prefix. 

There are 2 major forwarding modes: 

local forwarding mode, where CAP is locally forwarding data to and from wireless interface 

1467 

manager forwarding mode, where CAP sends to CAPsMAN all data received over wireless and only sends out the wireless data received from CAPsMAN. In this mode, even client-to-client forwarding is controlled and performed by CAPsMAN. 

Forwarding mode is configured on a per-interface basis - so if one CAP provides 2 radio interfaces, one can be configured to operate in local forwarding mode and the other in manager forwarding mode. The same applies to Virtual-AP interfaces - each can have different forwarding mode from master interface or other Virtual-AP interfaces. 

Most of the datapath settings are used only when in manager forwarding mode, because in local forwarding mode CAPsMAN does not have control over data forwarding. 

There are the following datapath settings: 

bridge -- bridge interface to add interface to, as a bridge port, when enabled 

- bridge-cost -- bridge port cost to use when adding as bridge port 

- bridge-horizon -- bridge horizon to use when adding as bridge port 

- client-to-client-forwarding -- controls if client-to-client forwarding between wireless clients connected to interface should be allowed, in local forwarding mode this function is performed by CAP, otherwise it is performed by CAPsMAN. 

- local-forwarding -- controls forwarding mode 

- openflow-switch -- OpenFlow switch to add interface to, as port when enabled 

- vlan-id -- VLAN ID to assign to interface if vlan-mode enables use of VLAN tagging 

- vlan-mode -- VLAN tagging mode specifies if VLAN tag should be assigned to interface (causes all received data to get tagged with VLAN tag and allows interface to only send out data tagged with given tag)
