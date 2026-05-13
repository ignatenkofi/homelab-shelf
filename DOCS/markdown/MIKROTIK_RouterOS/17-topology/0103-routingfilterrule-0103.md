## `/routing/filter/rule` 

```
add chain=bgp_in rule="append bgp-large-communities myLargeComSet "
```

Since route-target is encoded in extended community attribute to change or match RT you need to operate on extended community attribute, for example: 

1079 

```
/routing/filter/rule
```

```
add chain=bgp_in rule="set bgp-ext-communities rt:327824:20 "
```
