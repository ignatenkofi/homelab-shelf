## RADIUS Support 

Since RouterOS v6.43 it is possible to use RADIUS to assign a rate-limit per DHCPv6 binding, to do so you need to pass the Mikrotik-Rate-Limit attribute from your RADIUS Server for your DHCPv6 binding. To achieve this you first need to set your DHCPv6 Server to use RADIUS for assigning bindings. Below is an example of how to set it up: 

```
/radius
```

```
add address=10.0.0.1 secret=VERYsecret123 service=dhcp
/ipv6 dhcp-server
set dhcp1 use-radius=yes
```

After that, you need to tell your RADIUS Server to pass the Mikrotik-Rate-Limit attribute. In case you are using FreeRADIUS with MySQL, then you need to add appropriate entries into radcheck and radreply tables for a MAC address, that is being used for your DHCPv6 Client. Below is an example for table entries: 

908 

```
INSERT INTO `radcheck` (`username`, `attribute`, `op`, `value`) VALUES
('000c4200d464', 'Auth-Type', ':=', 'Accept'),
 INSERT INTO `radreply` (`username`, `attribute`, `op`, `value`) VALUES
('000c4200d464', 'Delegated-IPv6-Prefix', '=', 'fdb4:4de7:a3f8:418c::/66'),
('000c4200d464', 'Mikrotik-Rate-Limit', '=', '10M');
```

**==> picture [13 x 12] intentionally omitted <==**

By default allow-dual-stack-queue is enabled and will add a single dynamic queue entry if the MAC address from the IPv4 lease (or DUID, if the DHCPv4 Client supports `Node-specific Client Identifiers` from RFC4361), but DUID from DHCPv6 Client is not always based on the MAC address from the interface on which the DHCPv6 client is running on, DUID is generated on a per-device basis. For this reason, a single dynamic queue entry might not be created, separate dynamic queue entries might be created instead.
