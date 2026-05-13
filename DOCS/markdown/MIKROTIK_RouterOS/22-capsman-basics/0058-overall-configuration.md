## Overall configuration: 

```
/interface wifi
```

```
set [ find default-name=wifi2 ] configuration.mode=station-bridge configuration.country=Latvia .ssid=router.
ssid.2 disabled=no security.authentication-types=wpa2-psk .passphrase=router.password
set [ find default-name=wifi1 ] configuration.mode=ap configuration.country=Latvia .ssid=router.ssid.5
disabled=no security.authentication-types=wpa2-psk .passphrase=router.password
add configuration.mode=ap .ssid=router.ssid.2 disabled=no master-interface=wifi2 name=wifi3 security.
authentication-types=wpa2-psk .passphrase=router.password
/interface list
add comment=defconf name=WAN
add comment=defconf name=LAN
/interface bridge
add auto-mac=no comment=defconf name=bridge
/interface bridge port
add interface=all bridge=bridge
/interface list member
add comment=defconf interface=bridge list=LAN
/ip dhcp-client
add interface=bridge
```
