## Summary 

Bonding is a technology that allows aggregation of multiple ethernet-like interfaces into a single virtual link, thus getting higher data rates and providing failover. 

**==> picture [13 x 13] intentionally omitted <==**

Interface bonding does not create an interface with a larger link speed. Interface bonding creates a virtual interface that can load balance traffic over multiple interfaces. More details can be found in the LAG interfaces and load balancing page. 

**==> picture [13 x 13] intentionally omitted <==**

CRS3xx, CRS5xx series switches, CCR2116, CCR2216 routers and 88E6393X, 88E6191X, 88E6190 switch chips support bridge hardware offloading with bonding interfaces. 

Only `802.3ad` (LACP), `balance-xor` (static LAG) and `active-backup` bonding modes are hardware offloaded, other bonding modes will use the CPU's resources. 

CRS3xx, CRS5xx series switches, CCR2116, CCR2216 routers will always use Layer2+Layer3+Layer4 for a transmit hash policy, while 88E6393X, 88E6191X, 88E6190 switch chips are limited to Layer2 transmit hash. Changing the transmit hash policy manually while HW offloading is used will have no effect. 

See more details on CRS3xx, CRS5xx, CCR2116, CCR2216 switch chip features 

.
