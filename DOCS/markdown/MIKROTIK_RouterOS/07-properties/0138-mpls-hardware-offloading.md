## MPLS hardware offloading 

Since RouterOS v6.41 it is possible to offload certain MPLS functions to the switch chip, the switch must be a (P)rovider router in a PE-P-PE setup in order to achieve hardware offloading. A setup example can be found in the Basic MPLS setup example manual page. The hardware offloading will only take place when LDP interfaces are configured as physical switch interfaces (e.g. Ethernet, SFP, SFP+). 

405 

**==> picture [13 x 13] intentionally omitted <==**

Currently only `CRS317-1G-16S+` and `CRS309-1G-8S+` using RouterOS v6.41 and newer are capable of hardware offloading certain MPLS functions. `CRS317-1G-16S+` and `CRS309-1G-8S+` built-in switch chip is not capable of popping MPLS labels from packets, in a PE-P-PE setup you either have to use explicit null or disable TTL propagation in MPLS network to achieve hardware offloading. 

**==> picture [13 x 13] intentionally omitted <==**

The MPLS hardware offloading has been removed since RouterOS v7.
