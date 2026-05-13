## Routing Filter Wizard 

Cmd : `/routing/filter/filter-wizard` 

Due to incresed complexity of writing filters in script like manner, v7.20 introduces new routing filter wizard that allows to generate filter rules with ROSv6like syntax. 

Quick demonstration: 

1063 

```
[admin@CCR2004_2XS_111] /routing/filter> filter-wizard <tab>
```

```
action        dst                   ospf-type         scope-target      set-gw-check                use-te-
nexthop
```

```
afi           dst-len               protocol          set-bgp-...       set-scope
bgp-...       gateway               routing-table     set-blackhole     set-scope-target
blackhole     jump-target-chain     rpki              set-comment       set-suppress-hw-offload
chain         match-chain           rpki-verify       set-distance      set-use-te-nexthop
distance      ospf-metric           scope             set-gateway       suppress-hw-offload
```

```
[admin@CCR2004_2XS_111] /routing/filter> filter-wizard action=accept chain=vpn-in afi=vpnv4 set-bgp-ext-
communities=rt:2:2
```

```
  result: Filter rule 'if (afi vpnv4) { set bgp-ext-communities rt:2:2; accept; }' added
```

```
[admin@CCR2004_2XS_111] /routing/filter> /routing/filter/rule/print
Flags: X - disabled, I - inactive
```

```
 0   ;;; added by filter-wizard
```

```
     chain=vpn-in rule="if (afi vpnv4) { set bgp-ext-communities rt:2:2; accept; }"
```

Filter wizard adds rules at the end of the list and will have a comment "added by filter-wizard". 

Returned errors when trying to add filter with unacceptable values will be printed in CLI and logged in system log with "route,error" topics. 

```
[admin@CCR2004_2XS_111] /routing/filter> filter-wizard action=accept chain=vpn-in afi=vpnv4 match-chain=vpn-in
  result: Error adding 'if (chain vpn-in && afi vpnv4) { accept; }'match with 'vpn-in' creates chain loop (6)
```

```
[admin@CCR2004_2XS_111] /routing/filter> /log/print
```

```
 2025-05-19 13:05:15 route,error Error adding 'if (chain vpn-in && afi vpnv4) { accept; }'match with 'vpn-in'
creates chain loop (6)
```

1064
