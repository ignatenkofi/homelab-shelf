## Multiple switch groups 

The CRS1xx/2xx series switches allow you to use multiple bridges with hardware offloading, this allows you to easily isolate multiple switch groups. This can be done by simply creating multiple bridges and enabling hardware offloading. 

**==> picture [13 x 13] intentionally omitted <==**

Multiple hardware offloaded bridge configuration is designed as a fast and simple port isolation solution, but it limits a part of the VLAN functionality supported by the CRS switch chip. For advanced configurations use one bridge within the CRS switch chip for all ports, configure VLANs, and isolate port groups with port isolation profile configuration. 

**==> picture [13 x 13] intentionally omitted <==**

CRS1xx/2xx series switches can run multiple hardware offloaded bridges with (R)STP enabled, but it is not recommended since the device is not designed to run multiple (R)STP instances on a hardware level. To isolate multiple switch groups and have (R)STP enabled you should isolate port groups with port isolation profile configuration.
