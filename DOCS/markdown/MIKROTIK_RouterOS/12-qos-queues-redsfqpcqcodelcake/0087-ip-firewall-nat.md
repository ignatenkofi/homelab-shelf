## `/ip firewall nat` 

```
  add action=accept chain=srcnat comment="defconf: accept all that matches IPSec policy" ipsec-policy=out,ipsec
disabled=yes
```

```
  add action=masquerade chain=srcnat comment="defconf: masquerade" out-interface-list=WAN
```

Notice the disabled policy matcher rule, the same as in firewall filters IPSec traffic must be excluded from being NATed (except in specific scenarios where IPsec policy is configured to match NAT`ed address). So whenever IPsec tunnels are used on the router this rule must be enabled.
