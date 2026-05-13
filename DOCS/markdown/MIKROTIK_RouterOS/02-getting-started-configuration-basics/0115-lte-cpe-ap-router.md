## LTE CPE AP router 

This configuration type is applied to routers that have both LTE and wireless interfaces. LTE interface is considered a WAN port protected by a firewall and MAC discovery/connection disabled. The IP address on the WAN port is acquired automatically. Wireless is configured as an access point and bridged with all available Ethernet ports. 

List of routers using this type of configuration: 

- wAP LTE Kit SXT LTE LtAP 4G kit LtAP LTE kit Chateau 

65 

**==> picture [516 x 369] intentionally omitted <==**

**----- Start of picture text -----**<br>
CPE RouterMode:<br>* wireless interface connected to providers network (WAN><br>* WAN port is protected by firewall and enabled DHCP cli><br>LAN Configuration:<br>The IP address 192.168.188.1/24 is set on the bridge (LAN por><br>DHCP Server: enabled;<br>DNS: enabled;<br>WAN (gateway) Configuration:<br>gateway:lte1 ;<br>ip4 firewall: enabled;<br>ip6 firewall: enabled;<br>NAT: enabled;<br>Login<br>admin user protected by a password<br>Configuration  preview  :<br>.<br>**----- End of picture text -----**<br>
