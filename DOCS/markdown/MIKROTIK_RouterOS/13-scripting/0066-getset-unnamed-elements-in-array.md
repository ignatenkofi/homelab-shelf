## Get/Set unnamed elements in array 

Lets say we have an array of elements { "el1"; "el2"; "el3" }. It is possible to pick elements of an array with pick command, but is not so neat as syntax below: 

```
[admin@1p_DUT_wAP ac] /> :global test { "el1"; "el2"; "el3" }
```

```
[admin@1p_DUT_wAP ac] /> :put ($test->1)
el2
```

The same syntax can be used to set values: 

```
[admin@1p_DUT_wAP ac] /> :set ($test->2) "el3_changed"
[admin@1p_DUT_wAP ac] /> :environment print
test={"el1"; "el2"; "el3_changed"}
```
