## Access Control List 

Access Control List contains of ingress policy and egress policy engines and allows configuration of up to 128 policy rules (limited by RouterOS). It is an advanced tool for wire-speed packet filtering, forwarding, shaping, and modifying based on Layer2, Layer3, and Layer4 protocol header field conditions. 

**==> picture [13 x 13] intentionally omitted <==**

See the Summary section for Access Control List supported Cloud Router Switch devices. 

**==> picture [13 x 13] intentionally omitted <==**

Due to hardware limitations, it is not possible to match broadcast/multicast traffic on specific ports. You should use port isolation, drop traffic on ingress ports, or use VLAN filtering to prevent certain broadcast/multicast traffic from being forwarded.
