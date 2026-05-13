## `/routing/filter/rule` 

```
add chain=BGP_OUT rule="if (dst-len==24 && dst in 172.16.0.0/16) { \n
    set bgp-med 20; set bgp-path-prepend 2; accept }"
```

It is also possible to match prefix length range like this
