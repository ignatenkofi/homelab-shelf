## Remote Switch Port Analyzer 

This example will mirror incomming and outgoing traffic from the ether2 interface, copies will be encapsulated in 802.1Q VLAN using the 999 as VLAN ID, and packets will be sent to the ether3 interface. If the original traffic is already VLAN tagged, RSPAN will add another layer of VLAN tagging as an outer tag. This results in the mirrored traffic being tagged twice. If the `mirror-target` port is included in vlan-filtering bridge, it is not required to make the interface as tagged VLAN member under the `/interface/bridge/vlan` menu for the RSPAN. 

```
/interface ethernet switch port
set ether2 mirror-egress=yes mirror-ingress=yes
/interface ethernet switch
```

```
set switch1 mirror-target=ether3 rspan=yes rspan-egress-vlan-id=999 rspan-ingress-vlan-id=999
```
