## MAC Based Mirroring 

The third configuration also requires ports to be switched in a group. Mirroring configuration sets the ether5 port as a mirror0 analyzer port and sets the mirror0 port to be used when mirroring from the Unicast Forwarding database occurs. The entry from the Unicast Forwarding database enables mirroring for packets with source or destination MAC address E7:16:34:A1:CD:18 from ether8 port. 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```

```
/interface ethernet switch
set ingress-mirror0=ether5 fdb-uses=mirror0
```

```
/interface ethernet switch unicast-fdb
add port=ether8 mirror=yes svl=yes mac-address=E7:16:34:A1:CD:18
```
