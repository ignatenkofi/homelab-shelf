## Traffic generator server setup 

```
/ip address
add address=1.1.1.1/24 interface=ether2
add address=2.2.2.1/24 interface=ether3
```

First, we will define which ports will be used as traffic generator tx/rx ports 

```
/tool traffic-generator port
add disabled=no interface=ether2 name=port0
add disabled=no interface=ether3 name=port1
```

To construct the actual packet that will be generated, packet-template is used. 

```
/tool traffic-generator packet-template
```

```
add header-stack=mac,ip,udp ip-dst=2.2.2.1/32 ip-gateway=1.1.1.2 ip-src=1.1.1.1/32 \
    name=routing-1 port=port0
```

```
add header-stack=mac,ip,udp ip-dst=1.1.1.1/25 ip-gateway=2.2.2.2 ip-src=2.2.2.1/32 \
    name=routing-2 port=port1
```

Notice that mac addresses were not specified since the template generator can assume the next-hop mac address automatically by sending ARP messages. Since we are doing routing and destination IP is not directly reachable, we have set the ip-gateway parameter to determine the next-hop macaddress. 

When running print you can see all assumed (detected) values including mac addresses. 

```
[admin@test-host] /tool traffic-generator packet-template> print
```

- `0 name="routing-1" header-stack=mac,ip,udp port=port0` 

```
   assumed-mac-dst=00:0C:42:00:38:9D assumed-mac-src=00:0C:42:40:94:25
   assumed-mac-protocol=ip assumed-ip-dscp=0 assumed-ip-id=0
   assumed-ip-frag-off=0 assumed-ip-ttl=64 assumed-ip-protocol=udp
   ip-src=1.1.1.1/32 ip-dst=2.2.2.1/32 assumed-udp-src-port=100
   assumed-udp-dst-port=200 ip-gateway=1.1.1.2 data=uninitialized data-byte=0
```

- `1 name="routing-2" header-stack=mac,ip,udp port=port1` 

```
   assumed-mac-dst=00:0C:42:00:38:D1 assumed-mac-src=00:0C:42:40:94:26
   assumed-mac-protocol=ip assumed-ip-dscp=0 assumed-ip-id=0
   assumed-ip-frag-off=0 assumed-ip-ttl=64 assumed-ip-protocol=udp
   ip-src=2.2.2.1/32 ip-dst=1.1.1.1/32 assumed-udp-src-port=100
   assumed-udp-dst-port=200 ip-gateway=2.2.2.2 data=uninitialized data-byte=0
```

For example, if any router in SUT were to change, assumed mac-addresses would not be updated automatically. To update packet templates simply issue command: 

1840 

```
/tool traffic-generator packet-template set [find]
```
