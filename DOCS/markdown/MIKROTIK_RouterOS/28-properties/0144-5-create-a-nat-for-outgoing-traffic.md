## 5.  Create a NAT for outgoing traffic: 

```
/ip/firewall/nat/add chain=srcnat action=masquerade src-address=172.17.0.0/24
```
