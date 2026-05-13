## I can't find my device in WinBox IPv4 Neighbors list or MAC connection fails with "ERROR could not connect to XX-XX-XX-XXXX-XX" 

Most of the network drivers will not enable IP stack unless your host device has an IP configuration. Set IPv4 configuration on your host device. 

Sometimes the device will be discovered due to caching, but MAC connection will still fail with "ERROR: could not connect to XX:XX:XX:XX:XX:XX 

**==> picture [13 x 13] intentionally omitted <==**

WinBox MAC-ADDRESS connection requires MTU value set to 1500, unfragmented. Other values can perform poorly - loss of connectivity can occur. 

272
