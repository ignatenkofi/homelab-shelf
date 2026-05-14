## A more complicated setup (changes only) 

**==> picture [504 x 197] intentionally omitted <==**

As opposed to the simplest setup, in this example, we have two customers: cust-one and cust-two. 

We configure two VPNs for them, cust-one and cust-two respectively, and exchange all routes between them. (This is also called "route leaking"). 

Note that this could be not the most typical setup, because routes are usually not exchanged between different customers. In contrast, by default, it should not be possible to gain access from one VRF site to a different VRF site in another VPN. (This is the "Private" aspect of VPNs.) Separate routing is a way to provide privacy, and it is also required to solve the problem of overlapping IP network prefixes. Route exchange is in direct conflict with these two requirements but may sometimes be needed (e.g. temp. solution when two customers are migrating to a single network infrastructure).
