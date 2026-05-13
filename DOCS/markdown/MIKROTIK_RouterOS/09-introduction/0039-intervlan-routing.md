## InterVLAN routing 

If separate VLANs are implemented on a switch, then a router is required to provide communication between VLANs. A switch works at OSI layer 2 so it uses only the Ethernet header to forward and does not check the IP header. For this reason, we must use the router that is working as a gateway for each VLAN. Without a router, a host is unable to communicate outside of its own VLAN. The routing process between VLANs described above is called interVLAN communication. 

To illustrate inter-VLAN communication, we will create a trunk that will carry traffic from three VLANs (VLAN2 and VLAN3, VLAN4) across a single link between a Mikrotik router and a manageable switch that supports VLAN trunking. 

Each VLAN has its own separate subnet (broadcast domain) as we see in the figure above: 

- VLAN 2 – 10.10.20.0/24; VLAN 3 – 10.10.30.0/24; VLAN 4 – 10.10.40.0./24. 

VLAN configuration on most switches is straightforward, we need to define which ports are members of the VLANs and define a 'trunk' port that can carry tagged frames between the switch and the router. 

Create VLAN interfaces: 

503 

```
/interface vlan
```

```
add name=VLAN2 vlan-id=2 interface=ether1 disabled=no
add name=VLAN3 vlan-id=3 interface=ether1 disabled=no
add name=VLAN4 vlan-id=4 interface=ether1 disabled=no
```
