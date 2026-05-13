## Use received prefix for local RA 

Consider following setup: 

**==> picture [505 x 333] intentionally omitted <==**

ISP is routing prefix 2001:DB8::/62 to the router R1 

Router R1 runs DHCPv6 server to delegate /64 prefixes to the customer routers CE1 CE2 DHCP client on routers CE1 and CE2 receives delegated /64 prefix from the DHCP server (R1). Client routers uses received prefix to set up RA on the local interface
