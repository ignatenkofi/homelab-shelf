## `/interface bridge mdb` 

```
add bridge=bridge1 group=ff02::2 interface=bridge1,ether2,ether3,ether4,ether5
```

```
[admin@MikroTik] > /interface bridge mdb print where group=ff02::2
Flags: D - DYNAMIC
Columns: GROUP, VID, ON-PORTS, BRIDGE
 #   GROUP    VID  ON-PORTS  BRIDGE
 0   ff02::2                 bridge1
15 D ff02::2    1  bridge1   bridge1
16 D ff02::2   10  bridge1   bridge1
                   ether2
                   ether3
                   ether4
                   ether5
17 D ff02::2   20  bridge1   bridge1
                   ether2
                   ether3
18 D ff02::2   30  bridge1   bridge1
                   ether2
                   ether3
```
