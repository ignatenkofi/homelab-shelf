## Q. How does it work together with existing mesh setups that are using RSTP? 

A. The internal structure of an RSTP network is transparent to the mesh protocol (because mesh hello packets are forwarded inside the RSTP network). The mesh will see the path between two entry points in the RSTP network as a single segment. On the other hand, a mesh network is not transparent to the RSTP, since RSTP hello packets are not be forwarded inside the mesh network. (This is the behavior since v3.26) 

**==> picture [13 x 13] intentionally omitted <==**

Routing loops are possible if a mesh network is attached to an RSTP network in two or more points! 

Note that if you have a WDS link between two access points, then both ends must have the same configuration (either as ports in a mesh on both ends or as ports in a bridge interface on both ends). 

You can also put a bridge interface as a mesh port (to be able to use a bridge firewall, for example).
