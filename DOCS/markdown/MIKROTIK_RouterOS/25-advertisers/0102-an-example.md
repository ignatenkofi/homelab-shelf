## An example: 

```
/iot mqtt subscriptions print
```

```
 0 broker=broker topic="some/sort/of/topic" qos=0 on-message="/system script run script1"
```

```
 1 broker=broker topic="some/#" qos=0 on-message="/system script run script2"
```

```
 2 broker=broker topic="some/sort/of/+" qos=0 on-message="/system script run script3"
```

```
 3 broker=broker topic="some/thing/#" qos=0 on-message="/system script run script4"
```

When you publish the data to `some/sort/of/topic` , script1 will be initiated → because the topic is an exact match. 

When you publish the data to `some/sort/of/thing` , scrtip3 will be initiated → because it falls under the single 1v1 wildcard topic name. 

When you publish the data to `some/name` , script2 will be initiated →  because it falls under the multi-level wildcard topic name. 

When you publish the data to `some/thing/else` , script 4 will be initiated → because it falls under the multi-level wildcard topic name (even though it is also matched by `some/#` wildcard, it is a level closer to `some/thing/#` entry).
