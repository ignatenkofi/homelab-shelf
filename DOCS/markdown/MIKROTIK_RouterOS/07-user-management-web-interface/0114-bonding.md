## Bonding 

CRS3xx, CRS5xx series switches and CCR2116, CCR2216 routers support hardware offloading with bonding interfaces. Only `802.3ad` (LACP), `balance -xor` (static LAG) and `active-backup` bonding modes are hardware offloaded, other bonding modes will use the CPU's resources. You can find more information about the bonding interfaces in the Bonding Interface section. 

To create a hardware offloaded bonding interface, you must create a bonding interface with a supported bonding mode: 

```
/interface bonding
add mode=802.3ad name=bond1 slaves=ether1,ether2
```

This interface can be added to a bridge alongside other interfaces: 

```
/interface bridge
add name=bridge
/interface bridge port
add bridge=bridge interface=bond1 hw=yes
add bridge=bridge interface=ether3 hw=yes
add bridge=bridge interface=ether4 hw=yes
```

400 

**==> picture [13 x 13] intentionally omitted <==**

Do not add interfaces to a bridge that are already in a bond, RouterOS will not allow you to add an interface to bridge that is already a slave port for bonding. 

Make sure that the bonding interface is hardware offloaded by checking the "H" flag: 

```
/interface bridge port print
Flags: X - disabled, I - inactive, D - dynamic, H - hw-offload
 #     INTERFACE                                 BRIDGE                                 HW
 0   H bond1                                     bridge                                 yes
 1   H ether3                                    bridge                                 yes
 2   H ether4                                    bridge                                 yes
```

**==> picture [13 x 13] intentionally omitted <==**

With HW-offloaded bonding interfaces, the built-in switch chip will always use Layer2+Layer3+Layer4 for a transmit hash policy, changing the transmit hash policy manually will have no effect.
