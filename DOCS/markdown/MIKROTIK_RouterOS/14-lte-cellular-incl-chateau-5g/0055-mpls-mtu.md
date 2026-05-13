## MPLS MTU 

Configuration of MPLS MTU (path MTU + MPLS tag size) is useful in cases when there is a large variety of possible MTUs along the path. Configuring MPLS MTU to a minimum value that can pass all the hops will ensure that the MPLS packet will not be silently dropped on the devices that do not support big enough MTU. 

MPLS MTUs are configured from the `/mpls interface` menu. 

```
[admin@rack1_b35_CCR1036] /mpls/interface> print
Flags: X - disabled; * - builtin
 0    ;;; router-test
      interface=ether1 mpls-mtu=1580 input=yes
```

```
 1    ;;; router-test
      interface=ether2 mpls-mtu=1580 input=yes
```

```
 2    interface=all mpls-mtu=1500
```
