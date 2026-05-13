## Advanced Setup Examples 

In this example, we will take a closer look at the required L2MTU of all Ethernet-like interfaces including Bridge, VLAN, and VPLS interfaces. 

In this setup we will have 3 routers: 

> Q-in-Q router - this router will receive a standard 1500 byte Ethernet frame and will add two VLAN tags to the packet. Then packet will be sent out via an Ethernet network to the second router 

1716 

VPLS router - this router will remove the outer VLAN tag and will bridge the packet with the remaining VLAN tag with the VPLS tunnel. VPLS tunnel will take a packet through the MPLS network to the third router. 

MPLS Edge router - will remove VPLS and VLAN tags and bridge packet to the client Ethernet network. 

**==> picture [504 x 627] intentionally omitted <==**

1717 

1718
