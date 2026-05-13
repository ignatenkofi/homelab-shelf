## Setup 

To simply configure DHCP server you can use a `setup` command. 

First, you configure an IP address on the interface: 

```
[admin@MikroTik] > /ip address add address=192.168.88.1/24 interface=ether3 disabled=no
```

Then you use `setup` a command which will automatically ask necessary parameters: 

903 

```
[admin@MikroTik] > /ip dhcp-server setup
Select interface to run DHCP server on
```

```
dhcp server interface: ether3
Select network for DHCP addresses
```

```
dhcp address space: 192.168.88.0/24
Select gateway for given network
```

```
gateway for dhcp network: 192.168.88.1
Select pool of ip addresses given out by DHCP server
```

```
addresses to give out: 192.168.88.2-192.168.88.254
Select DNS servers
```

```
dns servers: 10.155.126.1,10.155.0.1,
Select lease time
```

```
lease time: 10m
```

That is all. You have configured an active DHCP server.
