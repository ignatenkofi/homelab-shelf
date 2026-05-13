## Basic Example 

Lets look at very basic example where on the label switching router (P) along the LSP we want to mark packets with exp bit 0, limit the bandwidth and change exp bit to 3: 

840 

```
/mpls mangle
```

```
add chain=forward exp=0 set-exp=3 set-mark=m0
```

```
/queue tree
```

```
add limit-at=10M max-limit=10M name=mpls_queue packet-mark=m0 parent=sfp-sfpplus2
```

Keep in mind that MPLS packets cannot be queued with queues that are using IMQ interfaces (simple queue, queue tree global), so we need to use queue tree with "real" interface as a parent. 

MPLS Mangle table also shows matched packet count that is useful for setup debugging: 

```
[admin@CCR2004_2XS_111] /mpls/mangle> print
Flags: X - DISABLED
Columns: CHAIN, EXP, SET-EXP, SET-MARK, PACKETS
#   CHAIN    EXP  SET-EXP  SET-MARK  PACKETS
0   forward    0        3  m0        221 654
```

Another important thing is that MPLS mangle rules are not executed line by line like regular firewall mangle rules, MPLS Mangle is a set of actions that are applied in one go. 

For example, lets look at the set of rules 

```
/mpls mangle
add chain=forward exp=0 set-mark=m0
add chain=forward exp=0 set-exp=3
add chain=forward exp=3 set-mark=m3
```

In this example, if incoming packet has exp bit 0, third rule will have no effect. 

And once the action is set for specific exp bit it cannot be modified by another rules: 

```
[admin@CCR2004_2XS_111] /mpls/mangle> add chain=forward exp=0 set-mark=m4
failure: conflicting forward set-mark rule
```

841
