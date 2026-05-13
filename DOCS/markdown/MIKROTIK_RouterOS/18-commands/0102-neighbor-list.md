## Neighbor list 

The neighbor list shows all discovered neighbors in the Layer2 broadcast domain. It shows to which interface neighbor is connected, its IP/MAC addresses, and other related parameters. The list is read-only, an example of a neighbor list is provided below: 

```
[admin@MikroTik] /ip neighbor print
 # INTERFACE ADDRESS         MAC-ADDRESS       IDENTITY   VERSION    BOARD
 0 ether13   192.168.33.2    00:0C:42:00:38:9F MikroTik   5.99       RB1100AHx2
 1 ether11   1.1.1.4         00:0C:42:40:94:25 test-host  5.8        RB1000
 2 Local     10.0.11.203     00:02:B9:3E:AD:E0 c2611-r1   Cisco I...
 3 Local     10.0.11.47      00:0C:42:84:25:BA 11.47-750  5.7        RB750
 4 Local     10.0.11.254     00:0C:42:70:04:83 tsys-sw1   5.8        RB750G
 5 Local     10.0.11.202     00:17:5A:90:66:08 c7200      Cisco I...
```
