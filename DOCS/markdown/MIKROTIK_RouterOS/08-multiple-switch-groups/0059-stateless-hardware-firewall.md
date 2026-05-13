## Stateless Hardware Firewall 

While connection tracking and stateful firewalling can be performed only by the CPU, the hardware can perform stateless firewalling via switch rules (ACL). The next example prevents (on a hardware level) accessing a MySQL server from the ether1, and redirects to the CPU/Firewall packets from ether2 and ether3:
