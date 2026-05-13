## Summary 

A very common task is to forward only a certain set of VLANs over a Wireless Point-to-Point (PtP) link. This can be done using bridge VLAN filtering and should be used instead of any other methods (including bridging VLAN interfaces). Let's say we need to forward over a Wireless link to 2 different VLANs and all other VLAN IDs should be dropped. VLAN 10 is going to be our Internet traffic while VLAN 99 is going to be for our management traffic. Below you can find the network topology: 

**==> picture [505 x 127] intentionally omitted <==**
