## 7.9 Tunneling Support

The X550 supports the VXLAN and NVGRE tunneling packet formats. As part of this support the
following features are supported:
 • LSO and transmit checksum offloads for tunneled packets as described in Section 7.2.4 and
   Section 7.2.5.
 • RSS forwarding based on inner L3/L4 header as described in Section 7.1.3.7
 • Flow director forwarding based on Tenant ID, inner MAC and inner VLAN as described in
   Section 7.1.3.6
 • New indications in the receive descriptor with information on the tunnel headers and on the outer
   header checksum as described in Section 7.1.5.2
 • New packet split modes based on the tunnel header or outer L2 header as described in
   Section A.2.5

532                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions
