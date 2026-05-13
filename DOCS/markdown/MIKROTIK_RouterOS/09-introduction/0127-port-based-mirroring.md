## Port-Based Mirroring 

The first configuration sets the ether5 port as a mirror0 analyzer port for both ingress and egress mirroring, mirrored traffic will be sent to this port. Portbased ingress and egress mirroring are enabled from the ether6 port. 

```
/interface ethernet switch
set ingress-mirror0=ether5 egress-mirror0=ether5
/interface ethernet switch port
set ether6 ingress-mirror-to=mirror0 egress-mirror-to=mirror0
```
