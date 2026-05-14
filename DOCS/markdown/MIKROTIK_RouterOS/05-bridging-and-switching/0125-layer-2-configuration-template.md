## Layer 2 Configuration Template 

```
/interface/ethernet/switch set 0 l3-hw-offloading=no
```

```
/interface/bridge
# put bridge configuration changes here
/interface/vlan
# define/change VLAN interfaces
/interface/ethernet/switch set 0 l3-hw-offloading=yes
```
