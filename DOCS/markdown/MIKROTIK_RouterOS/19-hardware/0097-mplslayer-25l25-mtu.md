## MPLS/Layer-2.5/L2.5 MTU 

Configured in the "/mpls interface" menu, specifies the maximal size of the packet, including MPLS labels, that is allowed to send out by the particular interface. 

Make sure that MPLS MTU is smaller or equal to L2MTU. MPLS MTU affects packets depending on what action the MPLS router is performing. It is strongly recommended that MPLS MTU is configured to the same value on all routers forming the MPLS cloud because of the effects MPLS MTU has on MPLS switched packets. This requirement means that all interfaces participating in the MPLS cloud must be configured to the smallest MPLS MTU values among participating interfaces, therefore care must be taken to properly select the hardware to be used. 

1714 

You can read more about MPLS MTU here.
