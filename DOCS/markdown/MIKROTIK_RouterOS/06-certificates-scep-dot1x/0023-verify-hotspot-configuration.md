## Verify HotSpot configuration: 

```
[admin@MikroTik] /ip hotspot> print
Flags: X - disabled, I - invalid, S - HTTPS
# NAME INTERFACE ADDRESS-POOL PROFILE IDLE-TIMEOUT
0 hotspot1 ether3 hs-pool-3 hsprof1 5m
[admin@MikroTik] /ip hotspot>
[admin@MikroTik] /ip pool> print
# NAME RANGES
0 hs-pool-3 10.5.50.2-10.5.50.254
[admin@MikroTik] /ip pool> /ip dhcp-server
[admin@MikroTik] /ip dhcp-server> print
Flags: X - disabled, I - invalid
# NAME INTERFACE RELAY ADDRESS-POOL LEASE-TIME ADD-ARP
0 dhcp1 ether3 hs-pool-3 1h
[admin@MikroTik] /ip dhcp-server> /ip firewall nat
[admin@MikroTik] /ip firewall nat> print
Flags: X - disabled, I - invalid, D - dynamic
0 X ;;; place hotspot rules here
chain=unused-hs-chain action=passthrough
```

```
1 ;;; masquerade hotspot network
chain=srcnat action=masquerade src-address=10.5.50.0/24
[admin@MikroTik] /ip firewall nat>
```
