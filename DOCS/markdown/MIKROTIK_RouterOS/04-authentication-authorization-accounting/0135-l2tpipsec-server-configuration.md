## L2TP/IPsec server configuration 

Configure the IP pool from which IP addresses will be assigned to the users and assign it to the PPP Profile. 

```
/ip pool
add name=vpn-pool range=192.168.99.2-192.168.99.100
```
