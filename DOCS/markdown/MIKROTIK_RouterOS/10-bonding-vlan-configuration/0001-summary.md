## Summary 

This page will show how to configure multiple switches to use bonding interfaces and port-based VLANs, it will also show a working example with a DHCPServer, inter-VLAN routing, management IP, and invalid VLAN filtering configuration. 

**==> picture [13 x 13] intentionally omitted <==**

This article applies to CRS3xx, CRS5xx, CCR2116, and CCR2216 devices. It doesn't apply to CRS1xx/CRS2xx series. 

For this network topology, we will be using two CRS326-24G-2S+, one CRS317-1G-16S+, and one CCR1072-1G-8S+, but the same principles can be applied to any CRS3xx, CRS5xx series devices, and a router. 

**==> picture [504 x 302] intentionally omitted <==**

In this setup, SwitchA and SwitchC will tag all traffic from ports ether1-ether8 to VLAN ID 10, ether9-ether16 to VLAN ID 20, and ether17-ether24 to VLAN ID 30. Management will only be possible if a user is connecting with tagged traffic with VLAN ID 99 from ether1 on SwitchA or SwitchB, connecting to all devices will also be possible from the router using tagged traffic with VLAN ID 99. The SFP+ ports in this setup are going to be used as VLAN trunk ports while being in a bond to create a LAG interface.
