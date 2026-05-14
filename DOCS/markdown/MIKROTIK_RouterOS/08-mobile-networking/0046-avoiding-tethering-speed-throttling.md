## Avoiding tethering speed throttling 

Some operators (TMobile, YOTA etc.) allow unlimited data only for the device the SIM card is used on, all other data coming from mobile hotspots or tethering is highly limited by volume or by throughput speed. Some sources have found out that this limitation is done by monitoring TTL (Time To Live) values from packets to determine if limitations need to be applied (TTL is decreased by 1 for each "hop" made). RouterOS allows changing the TTL parameter for packets going from the router to allow hiding sub networks. Keep in mind that this may conflict with fair use policy. 

824 

```
IPv4 mangle rule:
/ip firewall mangle
add action=change-ttl chain=postrouting new-ttl=set:65 out-interface=lte1 passthrough=yes
IPv6 mangle rule:
/ipv6 firewall mangle
add action=change-hop-limit chain=postrouting new-hop-limit=set:65 passthrough=yes
```

More information: YOTA, TMobile
