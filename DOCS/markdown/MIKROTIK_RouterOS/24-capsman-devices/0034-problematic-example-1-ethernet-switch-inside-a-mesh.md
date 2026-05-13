## Problematic example 1: Ethernet switch inside a mesh 

1500 

**==> picture [505 x 319] intentionally omitted <==**

Router A is outside the mesh, all the rest of the routers are inside. For routers B, C, D all interfaces are added as mesh ports. 

Router A will not be able to communicate reliably with router C. The problem manifests itself when D is the designated router for Ethernet; if B takes this role, everything is OK. The main cause of the problem is MAC address learning on Ethernet switch. 

Consider what happens when router A wants to send something to C. We suppose router A either knows or floods data to all interfaces. Either way, data arrives at the switch. The switch, not knowing anything about the destination's MAC address, forwards the data to both B and D. 

What happens now: 

1.  B receives the packet on a mesh interface. Since the MAC address is not local for B and B knows that he is not the designated router for the Ethernet network, he simply ignores the packet. 

2.  D receives the packet on a mesh interface. Since the MAC address is not local for B and D is the designated router for the Ethernet network, he initiates the path discovery process to C. 

After path discovery is completed, D has information that C is reachable over B. Now D encapsulates the packet and forwards it back to the Ethernet network. The encapsulated packet is forwarded by the switch, received and forwarded by B, and received by C. So far everything is good. 

Now C is likely to respond to the packet. Since B already knows where A is, he will decapsulate and forward the reply packet. But now the switch will learn that the MAC address of C is reachable through B! That means, next time when something arrives from A addressed to C, the switch will forward data only t o B (and B, of course, will silently ignore the packet)! 

In contrast, if B took up the role of a designated router, everything would be OK, because traffic would not have to go through the Ethernet switch twice. 

Troubleshooting : either avoid such setup or disable MAC address learning on the switch. Note that on many switches that is not possible. 

Also note that there will be no problem, if either: 

router A supports and is configured to use HWMP+; 

or Ethernet switch is replaced with a router that supports HWMP+ and has Ethernet interfaces added as mesh ports.
