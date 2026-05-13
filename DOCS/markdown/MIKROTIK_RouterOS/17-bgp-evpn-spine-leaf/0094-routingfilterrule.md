## `/routing/filter/rule` 

```
add chain=bgp_in rule="if (dst in 192.168.0.0/16) {accept}"
```

```
add chain=bgp_in rule="set bgp-local-pref -1; set bgp-igp-metric ospf-ext-metric; accept"
```

**==> picture [13 x 13] intentionally omitted <==**

If the routing filter chain is not specified BGP will try to advertise every active route it can find in the routing table 

**==> picture [13 x 13] intentionally omitted <==**

The default action of the routing filter chain is "drop"
