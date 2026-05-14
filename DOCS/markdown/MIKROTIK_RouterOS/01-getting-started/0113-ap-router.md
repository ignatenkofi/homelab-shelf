## AP Router 

This type of configuration is applied to home access point routers to be used straight out of the box without additional configuration (except router passwords and wireless keys) 

First Ethernet is always configured as a WAN port (protected by a firewall, enabled DHCP client, and disabled MAC connection/discovery). Other Ethernet ports and wireless interfaces are added to the local LAN bridge with 192.168.88.1/24 address set and configured DHCP server. In the case of dual-band routers, one wireless is configured as a 5 GHz access point and the other as a 2.4 GHz access point. 

List of routers using this type of configuration: 

RB 450,751,850,951,953,2011,3011,4011 hEX, PowerBox mAP wAP, wAP R (without LTE card) hAP cAP OmniTIK CRS series with wireless interface L009 series Audience Knot PWR 

66 

**==> picture [13 x 13] intentionally omitted <==**

RouterMode: 

* WAN port is protected by firewall and enabled DHCP cli> 

* Wireless and Ethernet interfaces (except WAN port/s) are part of the LAN bridge 

LAN Configuration: 

The IP address 192.168.88.1/24 is set on the bridge (LAN port) DHCP Server: enabled; DNS: enabled; 

wlan1 Configuration: 

mode: ap-bridge; band: 2ghz-b/g/n; tx-chains: 0;1; rx-chains: 0;1; installation: indoor; wpa2: no; ht-extension: 20/40mhz-XX; 

WAN (gateway) Configuration: 

ip4 firewall: enabled; ip6 firewall: enabled; NAT: enabled; DHCP Client: enabled; Login 

admin user protected by a password 

Configuration preview : 

**==> picture [150 x 113] intentionally omitted <==**
