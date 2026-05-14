## Using CAPsMAN Forwarding Mode 

1546 

**==> picture [505 x 296] intentionally omitted <==**

In CAPsMAN Forwarding Mode all traffic that is coming from a CAP is encapsulated with a special CAPsMAN header, which can only be removed by a CAPsMAN router, this means that a switch will not be able to distinguish the VLAN ID set by the CAP since the VLAN tag is also going to be encapsulated. This mode limits the possibility to divert traffic in Layer2 networks, but gives you the possibility to forward traffic from each CAP over Layer3 networks for a distant CAPsMAN router to process the traffic, this mode is useful when you want to control multiple CAPs in remote locations, but want to use a central gateway.
