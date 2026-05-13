## VLAN on a bridge in a bridge 

Consider the following scenario, you have a set of interfaces (don't have to be physical interfaces) and you want all of them to be in the same Layer2 segment, the solution is to add them to a single bridge, but you require that traffic from one port tags all traffic into a certain VLAN. This can be done by creating a VLAN interface on top of the bridge interface and by creating a separate bridge that contains this newly created VLAN interface and an interface, which is supposed to add a VLAN tag to all received traffic. A network diagram can be found below: 

**==> picture [504 x 112] intentionally omitted <==**
