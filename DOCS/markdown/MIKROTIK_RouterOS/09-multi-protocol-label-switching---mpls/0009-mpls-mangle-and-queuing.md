## MPLS Mangle and Queuing 

RouterOS firewall works only with IP traffic, which means that it is not possible to mark MPLS packets directly in mangle and limit by queues. Queuing had to be done on ingress edge router before MPLS header is added or on egress edge router after MPLS label is removed. 

Starting from ROS v7.17 MPLS Mangle is added. This allows to add packet mark based on exp bit, or change the assigned exp bit on label switching (P) routers or on PE output after MPLS encapsulation. 

This configuration is accessible from `/mpls/mangle` menu.
