## Regex Testing Tool 

RouterOS now has a built-in regex checking tool to simplify the hard life of the administrators. This tool supports also num-list so now exact regex can be tested against any as-path before applying it to the routing filters. 

```
/routing/filter/num-list add list=test range=100-1500
```

```
/routing/filter/test-as-path-regexp regexp="[[:test:]]5678\$" as-path="1234,5678"
```
