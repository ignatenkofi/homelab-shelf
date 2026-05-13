## `/interface bonding` 

```
add mode=802.3ad name=bond_1-2-3-4 slaves=sfp-sfpplus1,sfp-sfpplus2,sfp-sfpplus3,sfp-sfpplus4
```

**==> picture [13 x 13] intentionally omitted <==**

Interface bonding does not create an interface with a larger link speed. Interface bonding creates a virtual interface that can load balance traffic over multiple interfaces. More details can be found on the LAG interfaces and load balancing page.
