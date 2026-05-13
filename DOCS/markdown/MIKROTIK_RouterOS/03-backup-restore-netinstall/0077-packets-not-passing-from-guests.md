## Packets not passing from guests 

The problem: after configuring a software interface (VLAN, EoIP, bridge, etc.) on the guest CHR it stops passing data to the outside world beyond the router. 

The solution: check your VMS (Virtualization Management System) security settings, if other MAC addresses are allowed to pass and if packets with VLAN tags are allowed to pass through. Adjust the security settings according to your needs like allowing MAC spoofing or a certain MAC address range. For VLAN interfaces, it is usually possible to define allowed VLAN tags or VLAN tag range. 

126
