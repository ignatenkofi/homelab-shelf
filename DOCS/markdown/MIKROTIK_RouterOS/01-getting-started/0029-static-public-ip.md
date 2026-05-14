## Static Public IP 

When configuring a static address, your ISP provides specific parameters, such as: 

IP: 1.2.3.100/24 Gateway: 1.2.3.1 DNS: 8.8.8.8 

These are three basic parameters that you need to get the internet connection working. 

To configure this in RouterOS, we'll manually add an IP address, add a default route with a provided gateway, and set up a DNS server 

```
/ip address add address=1.2.3.100/24 interface=ether1
/ip route add gateway=1.2.3.1
/ip dns set servers=8.8.8.8
```
