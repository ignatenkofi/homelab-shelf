## `# interface used for AP interconnections` 

```
/interface wireless set wlan1 disabled=no ssid=mesh frequency=2437 band=2ghz-b/g/n mode=ap-bridge \
 wds-mode=static-mesh wds-default-bridge=mesh1
```

```
# interface used for client connections
```

```
 /interface wireless set wlan2 disabled=no ssid=mesh-clients frequency=5180 band=5ghz-a/n/ac mode=ap-bridge
```

```
# a static WDS interface for each AP you want to connect to
```

```
/interface wireless wds add disabled=no master-interface=wlan1 name=<descriptive name of remote end> \
 wds-address=<MAC address of remote end>
```

1494 

Here WDS interface is added manually because static WDS mode is used. If you are using wds-mode = dynamic-mesh , all WDS interfaces will be created automatically. The frequency and band parameters are specified here only to produce valid example configuration; mesh protocol operations are by no means limited to or optimized for, these particular values. 

**==> picture [13 x 13] intentionally omitted <==**

You may want to increase the disconnect-timeout wireless interface option to make the protocol more stable. 

In real-world setups you also should take care of securing the wireless connections, using /interface wireless security-profile . For simplicity, that configuration is not shown here. 

Results on router A (there is one client connected to wlan2): 

```
[admin@A] > /interface mesh print
Flags: X - disabled, R - running
```

```
0 R name="mesh1" mtu=1500 arp=enabled mac-address=00:0C:42:0C:B5:A4 auto-mac=yes
admin-mac=00:00:00:00:00:00 mesh-portal=no hwmp-default-hoplimit=32
```

```
hwmp-preq-waiting-time=4s hwmp-preq-retries=2 hwmp-preq-destination-only=yes
hwmp-preq-reply-and-forward=yes hwmp-prep-lifetime=5m hwmp-rann-interval=10s
hwmp-rann-propagation-delay=1s hwmp-rann-lifetime=22s
```

```
[admin@A] > /interface mesh port print detail
Flags: X - disabled, I - inactive, D - dynamic
```

```
0 interface=wlan1 mesh=mesh1 path-cost=10 hello-interval=10s port-type=auto port-type-used=wireless
```

```
1 interface=wlan2 mesh=mesh1 path-cost=10 hello-interval=10s port-type=auto port-type-used=wireless
```

```
2 D interface=router_B mesh=mesh1 path-cost=105 hello-interval=10s port-type=auto port-type-used=WDS
```

```
3 D interface=router_D mesh=mesh1 path-cost=76 hello-interval=10s port-type=auto port-type-used=WDS
```

The FDB (Forwarding Database) at the moment contains information only about local MAC addresses, non-mesh nodes reachable through a local interface, and direct mesh neighbors: 

```
[admin@A] /interface mesh fdb print
Flags: A - active, R - root
MESH TYPE MAC-ADDRESS ON-INTERFACE LIFETIME AGE
A mesh1 local 00:0C:42:00:00:AA 3m17s
A mesh1 neighbor 00:0C:42:00:00:BB router_B 1m2s
A mesh1 neighbor 00:0C:42:00:00:DD router_D 3m16s
A mesh1 direct 00:0C:42:0C:7A:2B wlan2 2m56s
A mesh1 local 00:0C:42:0C:B5:A4 2m56s
```

```
[admin@A] /interface mesh fdb print detail
Flags: A - active, R - root
A mac-address=00:0C:42:00:00:AA type=local age=3m21s mesh=mesh1 metric=0 seqnum=4294967196
A mac-address=00:0C:42:00:00:BB type=neighbor on-interface=router_B age=1m6s mesh=mesh1 metric=132
seqnum=4294967196
```

```
A mac-address=00:0C:42:00:00:DD type=neighbor on-interface=router_D age=3m20s mesh=mesh1 metric=79
seqnum=4294967196
```

```
A mac-address=00:0C:42:0C:7A:2B type=direct on-interface=wlan2 age=3m mesh=mesh1 metric=10 seqnum=0
A mac-address=00:0C:42:0C:B5:A4 type=local age=3m mesh=mesh1 metric=0 seqnum=0
```

Test if ping works: 

```
[admin@A] > /ping 00:0C:42:00:00:CC
00:0C:42:00:00:CC 64 byte ping time=108 ms
00:0C:42:00:00:CC 64 byte ping time=51 ms
00:0C:42:00:00:CC 64 byte ping time=39 ms
00:0C:42:00:00:CC 64 byte ping time=43 ms
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 39/60.2/108 ms
```

Router A had to discover a path to Router C first, hence the slightly larger time for the first ping. Now the FDB also contains an entry for 00:0C:42:00:00: CC, with type "mesh". 

1495 

Also, test that ARP resolving works and so does IP level ping: 

```
[admin@A] > /ping 10.4.0.3
10.4.0.3 64 byte ping: ttl=64 time=163 ms
10.4.0.3 64 byte ping: ttl=64 time=46 ms
10.4.0.3 64 byte ping: ttl=64 time=48 ms
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 46/85.6/163 ms
```
