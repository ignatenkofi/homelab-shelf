## `/routing/filter/rule` 

```
add chain=BGP_OUT rule="if (dst-len>13 && dst-len<31 && dst in 172.16.0.0/16) { accept }"
```

Filter rules now can be used to match or set communities,  large communities, and extended communities from the community list:
