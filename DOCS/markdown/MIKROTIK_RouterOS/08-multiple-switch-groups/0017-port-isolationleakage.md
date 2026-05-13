## Port Isolation/Leakage 

The CRS switches support flexible multi-level isolation features, which can be used for user access control, traffic engineering and advanced security and network management. The isolation features provide an organized fabric structure allowing user to easily program and control the access by port, MAC address, VLAN, protocol, flow, and frame type. The following isolation and leakage features are supported: 

- Port-level isolation MAC-level isolation VLAN-level isolation Protocol-level isolation Flow-level isolation Free combination of the above 

Port-level isolation supports different control schemes on the source port and destination port. Each entry can be programmed with access control for either the source port or the destination port. 

When the entry is programmed with source port access control, the entry is 

applied to the ingress packets. 

When the entry is programmed with destination port access control, the entry 

is applied to the egress packets. 

Port leakage allows bypassing egress VLAN filtering on the port. A leaky port is allowed to access other ports for various applications such as security, network control, and management. Note: When both isolation and leakage are applied to the same port, the port is isolated.
