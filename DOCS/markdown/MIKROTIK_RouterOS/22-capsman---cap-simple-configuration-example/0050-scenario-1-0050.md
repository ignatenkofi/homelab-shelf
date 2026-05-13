## Scenario #1 

Scenario, where station's WiFi interface is categorized as a "WAN" interface, which allows station's clients to stay hidden behind NAT. This is a factory configuration applied to most CPE devices. 

An example of such topology: 

**==> picture [505 x 238] intentionally omitted <==**

This type of setup, requires the CPE to have: 

1.  WiFi interface categorized as "WAN" port in the interface list members menu. 

2.  a DHCP-server running on the "other/ethernet" interfaces (it is suggested to ensure that AP's DHCP server and Station's DHCP server networks do not use the same subnet, as it can lead to layer3/routing issues). 

3.  a DHCP-client or a static IP applied to the WiFi interface and a default route configured. 4. `mode=station` configured in the WiFi settings. 

1370
