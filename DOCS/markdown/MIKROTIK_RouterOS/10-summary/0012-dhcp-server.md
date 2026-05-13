## DHCP-Server 

577 

To get the DHCP-Server working for each VLAN ID, the server must be set up on the previously created VLAN interfaces (one server for each VLAN ID). Preferably each VLAN ID should have its own subnet and its own IP pool. A DNS Server could be specified as the router's IP address for a particular VLAN ID or a global DNS Server could be used, but this address must be reachable. 

To set up the DHCP-Server, use these commands on the Router : 

```
/ip pool
add name=VLAN10_POOL ranges=192.168.10.100-192.168.10.200
add name=VLAN20_POOL ranges=192.168.20.100-192.168.20.200
add name=VLAN30_POOL ranges=192.168.30.100-192.168.30.200
/ip dhcp-server
add address-pool=VLAN10_POOL disabled=no interface=VLAN10 name=VLAN10_DHCP
add address-pool=VLAN20_POOL disabled=no interface=VLAN20 name=VLAN20_DHCP
add address-pool=VLAN30_POOL disabled=no interface=VLAN30 name=VLAN30_DHCP
/ip dhcp-server network
add address=192.168.10.0/24 dns-server=192.168.10.1 gateway=192.168.10.1
add address=192.168.20.0/24 dns-server=192.168.20.1 gateway=192.168.20.1
add address=192.168.30.0/24 dns-server=192.168.30.1 gateway=192.168.30.1
```

In case the router's DNS Server is being used, don't forget to allow remote requests and make sure DNS Servers are configured on the router. Use these commands on the Router : 

```
/ip dns
```

```
set allow-remote-requests=yes servers=8.8.8.8
```

**==> picture [13 x 13] intentionally omitted <==**

Make sure to secure your local DNS Server with Firewall from the outside when using `allow-remote-requests` set to `yes` since your DNS Server can be used for DDoS attacks if it is accessible from the Internet by anyone. 

Don't forget to create NAT, assuming that sfp-sfpplus8 is used as WAN port, use these commands on the Router : 

```
/ip firewall nat
```

```
add action=masquerade chain=srcnat out-interface=sfp-sfpplus8
```
