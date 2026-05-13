## RADIUS Support 

Since RouterOS v6.43 it is possible to use RADIUS to assign a rate limit per lease, to do so you need to pass the Mikrotik-Rate-Limit attribute from your RADIUS Server for your lease. To achieve this you first need to set your DHCPv4 Server to use RADIUS for assigning leases. Below is an example of how to set it up: 

```
/radius
add address=10.0.0.1 secret=VERYsecret123 service=dhcp
/ip dhcp-server
set dhcp1 use-radius=yes
```

After that, you need to tell your RADIUS Server to pass the Mikrotik-Rate-Limit attribute. In case you are using FreeRADIUS with MySQL, then you need to add appropriate entries into radcheck and radreply tables for a MAC address, that is being used for your DHCPv4 Client. Below is an example for table entries: 

```
INSERT INTO `radcheck` (`username`, `attribute`, `op`, `value`) VALUES
('00:0C:42:00:D4:64', 'Auth-Type', ':=', 'Accept'),
INSERT INTO `radreply` (`username`, `attribute`, `op`, `value`) VALUES
('00:0C:42:00:D4:64', 'Framed-IP-Address', '=', '192.168.88.254'),
('00:0C:42:00:D4:64', 'Mikrotik-Rate-Limit', '=', '10M'),
```

Alerts 

899 

To find any rogue DHCP servers as soon as they appear in your network, the DHCP Alert tool can be used. It will monitor the interface for all DHCP replies and check if this reply comes from a valid DHCP server. If a reply from an unknown DHCP server is detected, an alert gets triggered: 

```
[admin@MikroTik] ip dhcp-server alert>/log print
```

```
00:34:23 dhcp,critical,error,warning,info,debug dhcp alert on Public:
    discovered unknown dhcp server, mac 00:02:29:60:36:E7, ip 10.5.8.236
[admin@MikroTik] ip dhcp-server alert>
```

When the system alerts about a rogue DHCP server, it can execute a custom script. 

As DHCP replies can be unicast, the rogue DHCP detector may not receive any offer to other DHCP clients at all. To deal with this, the rogue DHCP detector acts as a DHCP client as well - it sends out DHCP discover requests once a minute. 

**==> picture [13 x 13] intentionally omitted <==**

The DHCP alert is not recommended on devices that are configured as DHCP clients. Since the alert itself generates DHCP discovery packets, it can affect the operation of the DHCP client itself. Use this feature only on devices that are DHCP servers or using a static IP address.
