## Configuration 

Bonding could be used only on OSI layer 2 (Ethernet level) connections. Thus we need to create EoIP interfaces on each of the wireless links. This is done as follows: 

on router R1: 

```
/interface eoip add remote-address=10.0.1.1/24 tunnel-id=1
```

```
/interface eoip add remote-address=10.2.2.1/24 tunnel-id=2
```

and on router R2: 

773 

```
/interface eoip add remote-address=10.0.1.2/24 tunnel-id=1
/interface eoip add remote-address=10.2.2.2/24 tunnel-id=2
```

The second step is to add a bonding interface and specify EoIP interfaces as slaves:
