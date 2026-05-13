## `/routing/filter/rule` 

```
add chain=bgp_in rule="set bgp-large-communities 200001:200001:10 "
```

If there are a lot of community sets, that need to be applied in multiple rules, then it is possible to define community sets and use them to match or set: 

```
/routing/filter/large-community-set
```

```
add set=myLargeComSet communities=200001:200001:10
```
