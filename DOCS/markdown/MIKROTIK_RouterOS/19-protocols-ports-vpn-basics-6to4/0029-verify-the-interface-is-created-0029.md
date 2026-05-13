## Verify the interface is created: 

```
[admin@Station] >  /interface eoip print
Flags: X - disabled; R - running
```

```
 0  R name="eoip-main" mtu=auto actual-mtu=1458 l2mtu=65535 mac-address=FE:4B:71:05:EA:8B arp=enabled
      arp-timeout=auto loop-protect=default loop-protect-status=off loop-protect-send-interval=5s
      loop-protect-disable-time=5m local-address=0.0.0.0 remote-address=10.0.0.1 tunnel-id=0
      keepalive=10s,10 dscp=inherit clamp-tcp-mss=yes dont-fragment=no allow-fast-path=yes
```

Next, we will bridge local interfaces with EoIP tunnel on our AP. If you already have a local bridge interface, simply add EoIP interface to it: 

1181 

```
/interface bridge port add bridge=bridge1 interface=eoip-remote
```

The bridge port list should list all local LAN interfaces and the EoIP interface: 

```
[admin@AP] > /interface bridge port print
Flags: I - INACTIVE; H - HW-OFFLOAD
Columns: INTERFACE, BRIDGE, HW, PVID, PRIORITY, PATH-COST, INTERNAL-PATH-COST, HORIZON
#    INTERFACE       BRIDGE   HW   PVID  PRIORITY  PATH-COST  INTERNAL-PATH-COST  HORIZON
0  H ether2          bridge1  yes     1  0x80             10                  10  none
1  H ether3          bridge1  yes     1  0x80             10                  10  none
2    eoip-remote     bridge1  yes     1  0x80             10                  10  none
```

On Station router, if you do not have a local bridge interface, create a new bridge and add both EoIP and local LAN interfaces to it: 

```
/interface bridge add name=bridge1
/interface bridge port add bridge=bridge1 interface=ether2
/interface bridge port add bridge=bridge1 interface=eoip-main
```

Verify the bridge port section: 

```
[admin@Station] > /interface bridge port print
Flags: I - INACTIVE; H - HW-OFFLOAD
Columns: INTERFACE, BRIDGE, HW, PVID, PRIORITY, PATH-COST, INTERNAL-PATH-COST, HORIZON
#    INTERFACE     BRIDGE   HW   PVID  PRIORITY  PATH-COST  INTERNAL-PATH-COST  HORIZON
0  H ether2        bridge1  yes     1  0x80             10                  10  none
2    eoip-main     bridge1  yes     1  0x80             10                  10  none
```

Now both sites are in the same Layer2 broadcast domain. You can set up IP addresses from the same network on both sites. 

1182
