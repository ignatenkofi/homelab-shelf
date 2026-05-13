## Push Route 

Push route support are added in 7.14, the maximum of possible input is limited to 1400 characters. IPv6 support added in 7.21_ab220. example: route network/IP [netmask] [gateway] [metric]. 

```
/interface ovpn-server server set myServer push-routes="192.168.102.0 255.255.255.0 192.168.109.1 9"
```

```
/interface/ovpn-server/server/set push-routes-ipv6="fdaa::/64,2001:db8::/32" 0
```
