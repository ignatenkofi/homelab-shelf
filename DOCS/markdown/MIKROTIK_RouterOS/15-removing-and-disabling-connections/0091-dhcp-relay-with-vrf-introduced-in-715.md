## DHCP Relay with VRF (introduced in 7.15) 

Let's take the previous setup but we'll consider that the interface to the DHCP server and interfaces to DHCP clients are added in VRF: 

```
/ip vrf
add interfaces=To-DHCP-Server name=vrf_server
add interfaces=Local2 name=vrf2
add interfaces=Local1 name=vrf1
```

In the DHCP-relay configuration dhcp-server-vrf should be added: 

```
/ip dhcp-relay/set dhcp-server-vrf=vrf_server numbers=0,1
```

Due to VRF configuration there are several routing-tables - we should add additional routes: 

```
/ip route
```

```
add disabled=no distance=1 dst-address=192.168.0.0/24 gateway=To-DHCP-Server@vrf_server pref-src="" routing-
table=vrf1 scope=10 suppress-hw-offload=no \
```

```
    target-scope=10
```

```
add disabled=no distance=1 dst-address=192.168.0.0/24 gateway=To-DHCP-Server@vrf_server pref-src="" routing-
table=vrf2 scope=10 suppress-hw-offload=no \
```

```
    target-scope=10
```

```
add disabled=no dst-address=192.168.1.0/24 gateway=Local1@vrf1 routing-table=vrf_server suppress-hw-offload=no
add disabled=no distance=1 dst-address=192.168.2.0/24 gateway=Local2@vrf2 pref-src="" routing-table=vrf_server
scope=30 suppress-hw-offload=no \
```

```
    target-scope=10
```

To achieve successful DHCP-server - DHCP-relay communication we should add NAT rules: 

914 

```
/ip firewall nat
```

```
add action=dst-nat chain=dstnat dst-address=192.168.2.1 dst-port=67 in-interface=To-DHCP-Server protocol=udp
src-address=192.168.0.1 to-addresses=\
    192.168.0.2
```

```
add action=dst-nat chain=dstnat dst-address=192.168.1.1 dst-port=67 in-interface=To-DHCP-Server protocol=udp
src-address=192.168.0.1 to-addresses=\
    192.168.0.2
```

915
