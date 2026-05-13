## Simple DHCP client 

Add a DHCP client on the ether1 interface: 

```
/ip dhcp-client add interface=ether1 disabled=no
```

After the interface is added, you can use the "print" or "print detail" command to see what parameters the DHCP client acquired: 

```
[admin@MikroTik] ip dhcp-client> print detail
Flags: X - disabled, I - invalid
```

```
 0   interface=ether1 add-default-route=yes use-peer-dns=yes use-peer-ntp=yes
     status=bound address=192.168.0.65/24 gateway=192.168.0.1
     dhcp-server=192.168.0.1 primary-dns=192.168.0.1 primary-ntp=192.168.0.1
     expires-after=9m44s
```

```
[admin@MikroTik] ip dhcp-client>
```

**==> picture [13 x 13] intentionally omitted <==**

If the interface used by the DHCP client is part of the VRF configuration, then the default route and other received routes from the DHCP server will be added to the VRF routing table. 

DHCP client status can be checked with: 

```
/ip dhcp-client print detail
```
