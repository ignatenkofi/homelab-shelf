## Notes 

**==> picture [13 x 13] intentionally omitted <==**

The routing protocol configuration upgrade is triggered only once. This means that if a router was downgraded to ROSv6, the configuration was modified and the router got upgraded back to ROSv7, then the resulting configuration is the one that was present before the downgrade. To retrigger v6 configuration conversion, load ROSv6 backup with the option `force-v6-to-v7-configuration-upgrade=yes` .
