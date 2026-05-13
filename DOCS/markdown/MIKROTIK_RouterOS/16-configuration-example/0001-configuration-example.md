## Configuration Example 

941 

Example demonstrates very basic L2 untagged packet forwarding between sfp-sfplus1-2 ports. Faucet is used a controller. 

```
/openflow
```

```
add controllers=tcp/10.155.101.182/6653 datapath-id=1/DC:2C:6E:A4:B4:2E disabled=no name=faucet
```

```
/openflow port
add disabled=no interface=sfp-sfpplus1 port-id=1 switch=faucet
add disabled=no interface=sfp-sfpplus2 port-id=2 switch=faucet
```

**==> picture [13 x 13] intentionally omitted <==**

If you intend to use also Gauge, then add Gauge's IP and port  in the controllers list. Example, where 6654 is Gauge port: `controllers=tcp /10.155.101.182/6653,tcp/10.155.101.182/6654` 

Faucet configuration. dp_id must be the same as datapath-id from ROS configuration in hex format ( 1/DC:2C:6E:A4:B4:2E →  0x0001dc2c6ea4b42e ): 

```
---
vlans:
    100:
        description: "untagged"
acls:
    1:
        - rule:
            actions:
                allow: 1
dps:
    test_switch:
        dp_id: 0x0001dc2c6ea4b42e
        hardware: "Generic"
        drop_broadcast_source_address: false
        drop_spoofed_faucet_mac: false
        interfaces:
            1:
                name: "h1"
                description: "host1 container"
                native_vlan: 100
                acl_in: 1
            2:
                name: "h2"
                description: "host2 container"
                native_vlan: 100
                acl_in: 1
```

Faucet installed flows can be seen from `/openflow/flow` menu: 

```
[admin@CCR2004_2XS_111] /openflow/flow>  print detail
Flags: I - inactive
```

- `0   switch=faucet version=4 match=" [ { ethdst_m=01000cccccccffffffffffff } ]" actions=" []" info="priority 8240, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=4` 

- `1   switch=faucet version=4 match=" [ { ethdst_m=01000ccccccdffffffffffff } ]" actions=" []" info="priority 8240, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=4` 

```
 2   switch=faucet version=4 match=" [ { ethdst_m=ffffffffffffffffffffffff }; { vlanvid=1064 } ]"
     actions=" [ { apply-actions= [ { popvlan={} }; { output={ port=1; max_len=0 } }; { output={ port=2;
max_len=0 } } ]
```

```
        } ]"
     info="priority 8240, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=4
```

- `3   switch=faucet version=4 match=" [ { ethdst_m=0180c2000000fffffffffff0 } ]" actions=" []"` 

942 

```
     info="priority 8236, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=4
```

```
 4   switch=faucet version=4 match=" [ { ethdst_m=0180c2000000ffffff000000 }; { vlanvid=1064 } ]"
     actions=" [ { apply-actions= [ { popvlan={} }; { output={ port=1; max_len=0 } }; { output={ port=2;
max_len=0 } } ]
```

```
        } ]"
```

```
     info="priority 8216, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=4
```

- `5   switch=faucet version=4 match=" [ { ethdst_m=01005e000000ffffff000000 }; { vlanvid=1064 } ]" actions=" [ { apply-actions= [ { popvlan={} }; { output={ port=1; max_len=0 } }; { output={ port=2; max_len=0 } } ]` 

```
        } ]"
```

```
     info="priority 8216, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=4
```

```
 6   switch=faucet version=4 match=" [ { ethdst_m=333300000000ffff00000000 }; { vlanvid=1064 } ]"
     actions=" [ { apply-actions= [ { popvlan={} }; { output={ port=1; max_len=0 } }; { output={ port=2;
max_len=0 } } ]
```

- `} ]"` 

```
     info="priority 8208, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=4
```

- `7   switch=faucet version=4 match=" [ { vlanvid=1064 } ]"` 

- `actions=" [ { apply-actions= [ { popvlan={} }; { output={ port=1; max_len=0 } }; { output={ port=2; max_len=0 } } ]` 

```
        } ]"
```

```
     info="priority 8192, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=4
```

- `8   switch=faucet version=4 match=" []" actions=" []"` 

```
     info="priority 0, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=4
```

- `9   switch=faucet version=4 match=" []" actions=" [ { goto=4 } ]"` 

```
     info="priority 0, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=3
```

- `10   switch=faucet version=4 match=" [ { ethtype=9000 } ]" actions=" []"` 

```
     info="priority 20490, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=2
```

- `11   switch=faucet version=4 match=" [ { vlanvid=1064 } ]"` 

```
     actions=" [ { apply-actions= [ { output={ port=4294967293; max_len=96 } } ] }; { goto=3 } ]"
     info="priority 4096, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=2
```

- `12   switch=faucet version=4 match=" []" actions=" [ { goto=3 } ]"` 

```
     info="priority 0, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=2
```

- `13   switch=faucet version=4 match=" [ { inport=00000001 }; { vlanvid=0000 } ]"` 

```
     actions=" [ { apply-actions= [ { pushvlan={ ethertype=33024 } }; { setfield={ vlanvid=1064 } } ] }; {
goto=2 } ]"
     info="priority 4096, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=1
```

- `14   switch=faucet version=4 match=" [ { inport=00000002 }; { vlanvid=0000 } ]"` 

```
     actions=" [ { apply-actions= [ { pushvlan={ ethertype=33024 } }; { setfield={ vlanvid=1064 } } ] }; {
goto=2 } ]"
```

```
     info="priority 4096, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=1
```

- `15   switch=faucet version=4 match=" []" actions=" []"` 

```
     info="priority 0, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=1
```

- `16   switch=faucet version=4 match=" [ { inport=00000001 } ]" actions=" [ { goto=1 } ]"` 

```
     info="priority 20480, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=0
```

- `17   switch=faucet version=4 match=" [ { inport=00000002 } ]" actions=" [ { goto=1 } ]"` 

```
     info="priority 20480, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=0
```

- `18   switch=faucet version=4 match=" []" actions=" []"` 

```
     info="priority 0, idletimeout 0, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=0
```

- `19   switch=faucet version=4 match=" [ { ethdst=dc2c6ec5a7ff }; { vlanvid=1064 } ]"` 

```
     actions=" [ { apply-actions= [ { popvlan={} }; { output={ port=1; max_len=0 } } ] } ]"
     info="priority 8192, idletimeout 413, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=3
```

```
20   switch=faucet version=4 match=" [ { inport=00000001 }; { ethsrc=dc2c6ec5a7ff }; { vlanvid=1064 } ]"
     actions=" [ { goto=3 } ]" info="priority 8191, idletimeout 0, hardtimeout 263, cookie 1524372928,
removenotify 0"
```

943 

```
     table-id=2
```

```
21   switch=faucet version=4 match=" [ { ethdst=dc2c6e46f893 }; { vlanvid=1064 } ]"
     actions=" [ { apply-actions= [ { popvlan={} }; { output={ port=2; max_len=0 } } ] } ]"
     info="priority 8192, idletimeout 417, hardtimeout 0, cookie 1524372928, removenotify 0" table-id=3
```

```
22   switch=faucet version=4 match=" [ { inport=00000002 }; { ethsrc=dc2c6e46f893 }; { vlanvid=1064 } ]"
     actions=" [ { goto=3 } ]" info="priority 8191, idletimeout 0, hardtimeout 267, cookie 1524372928,
removenotify 0"
```

```
     table-id=2
```

Statistics of the flows can be seen with **`stats`** parameter: 

```
[admin@CCR2004_2XS_111] /openflow/flow>  print stats
Columns: SWITCH, MATCH, BYTES, PACKETS, DURATION
 # SWITCH  MATCH                                                                BYTES  PACKETS  DURATION
 0 faucet   [ { ethdst_m=01000cccccccffffffffffff } ]                            3590       25  6m26s890ms
 1 faucet   [ { ethdst_m=01000ccccccdffffffffffff } ]                               0        0  6m26s890ms
 2 faucet   [ { ethdst_m=ffffffffffffffffffffffff }; { vlanvid=1064 } ]          5552       26  6m26s890ms
 3 faucet   [ { ethdst_m=0180c2000000fffffffffff0 } ]                            4917       25  6m26s890ms
 4 faucet   [ { ethdst_m=0180c2000000ffffff000000 }; { vlanvid=1064 } ]             0        0  6m26s890ms
 5 faucet   [ { ethdst_m=01005e000000ffffff000000 }; { vlanvid=1064 } ]             0        0  6m26s890ms
 6 faucet   [ { ethdst_m=333300000000ffff00000000 }; { vlanvid=1064 } ]          5992       25  6m26s890ms
 7 faucet   [ { vlanvid=1064 } ]                                                  340        5  6m26s890ms
 8 faucet   []                                                                      0        0  6m26s890ms
 9 faucet   []                                                                  20391      106  6m26s890ms
10 faucet   [ { ethtype=9000 } ]                                                    0        0  6m26s890ms
11 faucet   [ { vlanvid=1064 } ]                                                  530        8  6m26s890ms
12 faucet   []                                                                      0        0  6m26s890ms
13 faucet   [ { inport=00000001 }; { vlanvid=0000 } ]                           39135      463  6m26s890ms
14 faucet   [ { inport=00000002 }; { vlanvid=0000 } ]                           37936      459  6m26s890ms
15 faucet   []                                                                  17941      100  6m26s890ms
16 faucet   [ { inport=00000001 } ]                                             48664      515  6m26s890ms
17 faucet   [ { inport=00000002 } ]                                             46348      507  6m26s890ms
18 faucet   []                                                                      0        0  6m26s890ms
19 faucet   [ { ethdst=dc2c6ec5a7ff }; { vlanvid=1064 } ]                       28340      408  6m26s780ms
20 faucet   [ { ethdst=dc2c6e46f893 }; { vlanvid=1064 } ]                       28340      408  6m26s780ms
21 faucet   [ { inport=00000001 }; { ethsrc=dc2c6ec5a7ff }; { vlanvid=1064 } ]  12020      142  2m660ms
22 faucet   [ { inport=00000002 }; { ethsrc=dc2c6e46f893 }; { vlanvid=1064 } ]  10769      133  1m55s660ms
```
