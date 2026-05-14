## Port Based Mirroring 

Starting from RouterOS version 7.15, it is possible to configure multiple source ports and selectively choose whether to mirror incoming traffic, outgoing traffic, or both. In this example, both incoming and outgoing traffic from the ether2 interface will be copied and sent to the ether3 interface for monitoring or analysis. 

```
# Since RouterOS v7.15
/interface ethernet switch port
set ether2 mirror-egress=yes mirror-ingress=yes
/interface ethernet switch
set switch1 mirror-target=ether3
```

```
# Older RouterOS:
/interface ethernet switch
set switch1 mirror-source=ether2 mirror-target=ether3
```
