## Configuration Examples 

In order for a device to participate in the RoMON network, the RoMON feature must be enabled and ports that participate in the RoMON network must be specified. 

234 

```
/tool romon set enabled=yes secrets=testing
```

Ports that participate in the RoMON network are configured in the RoMON port menu. Port list is a list of entries that match either specific port or all ports and specifies if matching port(s) is forbidden to participate in the RoMON network and in case port is allowed to participate in RoMON network entry also specifies the port cost. Note that all specific port entries have higher priority than the wildcard entry with interface=all . 

For example, the following list specifies that all ports participate in RoMON network with cost 100 and ether7 interface with cost 200: 

```
[admin@MikroTik] > /tool/romon/port/print
Flags: * - default
Columns: INTERFACE, FORBID, COST
#     INTERF  FO  COS
0  *  all     no  100
1     ether7  no  200
```

By default, one wildcard entry with forbid=no and cost=100 is created.
