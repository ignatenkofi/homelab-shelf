## WISP Bridge 

The configuration is the same as PTP Bridge in AP mode, except that wireless mode is set to ap_bridge for PTMP setups. The router can be accessed directly using a MAC address. If the device is connected to the network with an enabled DHCP server, configured DHCP client configured on the bridge interface will get the IP address, that can be used to access the router. 

List of routers using this type of configuration: 

- RB 911,912,921,922 - with Level4 license Groove A, RB 711 A BaseBox, NetBox mANTBox, NetMetal wAP 60G AP - with level4 license LtAP CME 

**==> picture [13 x 13] intentionally omitted <==**

WISP Bridge: 

* wireless and LAN interfaces are bridged; wlan1 Configuration: mode: ap-bridge; band: 2ghz-b/g/n; tx-chains: 0;1; rx-chains: 0;1; installation:   outdoor; wpa2: no; ht-extension:   20/40mhz-XX; wlan2 Configuration: mode: ap-bridge; band: 5ghz-a/n/ac; tx-chains: 0;1; rx-chains: 0;1; installation:   outdoor; wpa2: no; ht-extension:   20/40/80mhz-XXXX; LAN Configuration: DHCP Client: enabled on bridge (LAN port); Login admin user protected by a password Configuration preview : 

**==> picture [150 x 114] intentionally omitted <==**

Switch 

69 

This configuration utilizes switch chip features to configure a basic switch. All Ethernet ports are added to switch group and default IP address 192.168.88.1 /24 is set on bridge interface. 

List of routers using this type of configuration: 

**==> picture [516 x 323] intentionally omitted <==**

**----- Start of picture text -----**<br>
FiberBox<br>CRS without wireless interface<br>Switch mode:<br>All interfaces switched;<br>Login<br>admin user protected by a password<br>Configuration  preview  :<br>**----- End of picture text -----**<br>
