## Route Selection 

Route selection rules allow controlling how output routes are selected from available candidate routes. By default, (if no selection rules are set) output always picks the best route. 

For example, if we look at the routing table below, we can see that there are 2 candidate routes and one best route. By default when BGP selects which route to send out, it will pick the active route. 

```
[admin@4] /routing/route> print where dst-address=1.0.0.0/24
Flags: A - ACTIVE; b, y - COPY
Columns: DST-ADDRESS, GATEWAY, AFI, DISTANCE, SCOPE, TARGET-SCOPE, IMMEDIATE-GW
   DST-ADDRESS  GATEWAY         AFI  DISTANCE  SCOPE  TARGET-SCOPE  IMMEDIATE-GW
 b 1.0.0.0/24   10.155.101.217  ip4        19     40            30  10.155.109.254%ether1
Ab 1.0.0.0/24   10.155.101.232  ip4        20     40            30  10.155.109.254%ether1
 b 1.0.0.0/24   10.155.101.231  ip4        20     40            30  10.155.109.254%ether1
```

But there might be cases where you would want preference for other routes, not the active ones, and here come in-play selection rules. 

Selection rules in RouterOS are configured from `/routing/filter/select-rule` menu. 

Select rules can also call routing filters where routes get selected based on filter rules. For example, to mimic default output selection we can set up the following rule sets: 

```
/routing filter rule
add chain=get_active rule="if (active) {accept}"
```

```
/routing filter select-rule
add chain=my_select_chain do-where=get_active
```
