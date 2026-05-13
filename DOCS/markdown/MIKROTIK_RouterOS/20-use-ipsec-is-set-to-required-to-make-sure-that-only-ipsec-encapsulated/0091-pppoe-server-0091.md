## PPPoE Server 

To configure MikroTik RouterOS to be an Access Concentrator (PPPoE Server): 

add an IP address pool for the clients from 10.0.0.2-10.0.0.5; add PPP profile; add PPP secret (username/password); add the PPPoE server itself; 

```
[admin@MikroTik] > /ip pool
add name=pppoe-pool ranges=10.0.0.2-10.0.0.5
[admin@MikroTik] > /ppp profile
add local-address=10.0.0.1 name=for-pppoe remote-address=pppoe-pool
[admin@MikroTik] > /ppp secret
add name=MT-User password=StrongPass profile=for-pppoe service=pppoe
[admin@MikroTik] > /interface pppoe-server server
add default-profile=for-pppoe disabled=no interface=ether3 service-name=pppoeservice
```
