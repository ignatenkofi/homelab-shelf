## Source NAT 

If you want to hide your local devices behind your public IP address received from the ISP, you should configure the source network address translation (masquerading) feature of the MikroTik router. 

Let`s assume you want to hide both the office computer and server behind the public IP 172.16.16.1, the rule will look like the following one: 

```
/ip firewall nat add chain=srcnat src-address=10.0.0.0/24 action=src-nat to-addresses=172.16.16.1 out-
interface=WAN
```

Now your ISP will see all the requests coming with IP 172.16.16.1 and they will not see your LAN network IP addresses.
