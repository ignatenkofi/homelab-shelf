## Configuration 

VRF table is created in **`/ip vrf`** menu. After the VRF config is created routing table mapping is added (a dynamic table with the same name is created). Each active VRF will always have a mapped routing table. 

```
[admin@arm-bgp] /ip/vrf> print
Flags: X - disabled; * - builtin
 0  * name="main" interfaces=all
[admin@arm-bgp] /routing/table> print
Flags: D - dynamic; X - disabled, I - invalid; U - used
 0 D   name="main" fib
```

Note that the order of the added VRFs is significant. To properly match which interface will belong to the VRF care must be taken to place VRFs in the correct order (matching is done starting from the top entry, just like firewall rules). 

**==> picture [13 x 13] intentionally omitted <==**

Since each VRF has mapped routing table, count of max unique VRFs is limited to 1024. 

Let's look at the following example: 

1035 

```
[admin@arm-bgp] /ip/vrf> print
Flags: X - disabled; * - builtin
 0  * name="main" interfaces=all
 1    name="myVrf" interfaces=lo_vrf
```

Since the first entry is matching all the interfaces, the second VRF will not have any interfaces added. To fix the problem order of the entries must be changed. 

```
[admin@arm-bgp] /ip/vrf> move 1 0
[admin@arm-bgp] /ip/vrf> print
Flags: X - disabled; * - builtin
 0    name="myVrf" interfaces=lo_vrf
 1  * name="main" interfaces=all
```

Connected routes from the interfaces assigned to the VRF will be installed in the right routing table automatically. 

**==> picture [13 x 13] intentionally omitted <==**

When the interface is assigned to the VRF as well as connected routes it does not mean that RouterOS services will magically know which VRF to use just by specifying the IP address in the configuration. Each service needs VRF support to be added and explicit configuration. Whether the service has VRF support and has VRF configuration options refer to appropriate service documentation. 

For example, let's make an SSH service to listen for connections on the interfaces belonging to the VRF: 

```
[admin@arm-bgp] /ip/service> set ssh vrf=myVrf
[admin@arm-bgp] /ip/service> print
Flags: X, I - INVALID
Columns: NAME, PORT, CERTIFICATE, VRF
#   NAME     PORT  CERTIFICATE  VRF
0   telnet     23               main
1   ftp        21
2   www        80               main
3   ssh        22               myVrf
4 X www-ssl   443  none         main
5   api      8728               main
6   winbox   8291               main
7   api-ssl  8729  none         main
```

Adding routes to the VRF is as simple as specifying the routing-table parameter when adding the route and specifying in which routing table to resolve the gateway by specifying @name after the gateway IP: 

```
/ip route add dst-address=192.168.1.0/24 gateway=172.16.1.1@myVrf routing-table=myVrf
```

Traffic leaking between VRFs is possible if the gateway is explicitly set to be resolved in another VRF, for example: 

```
# add route in the myVrf, but resolve the gateway in the main table
/ip route add dst-address=192.168.1.0/24 gateway=172.16.1.1@main routing-table=myVrf
```

```
# add route in the main table, but resolve the gateway in the myVrf
/ip route add dst-address=192.168.1.0/24 gateway=172.16.1.1@myVrf
```

**==> picture [13 x 12] intentionally omitted <==**

If the gateway configuration does not have an explicitly configured table to be resolved in, then it is considered, that gateway should be resolved in the "main" table.
