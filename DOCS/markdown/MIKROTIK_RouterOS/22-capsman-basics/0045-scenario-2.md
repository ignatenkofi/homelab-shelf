## Scenario #2 

In case, you want to have the AP itself act as a DHCP-server for stations: 

**==> picture [505 x 249] intentionally omitted <==**

1.  Configure ethernet port as an uplink/WAN port, i.e. setup DHCP-client or static IP for the ethernet interface, set up a default route and categorize the port as "WAN" port in the interface list settings. 

2.  Setup DHCP-server on top of the WiFi interface (or on top of the bridge, which WiFi port is a part of) and add a respective IP address to that interface.
