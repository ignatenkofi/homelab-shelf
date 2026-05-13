## How to define empty array 

RouterOS does not allow to define empty array in a way that you think it should work: 

```
[admin@1p_DUT_wAP ac] /interface> :global array {}
syntax error (line 1 column 17)
```

Insted a work around is to convert empty string to an array: 

```
[admin@rack1_b36_CCR1009] > :global array [:toarray ""]
[admin@rack1_b36_CCR1009] > :environment print
array={}
```

From here we can use this array to set elements: 

```
[admin@rack1_b36_CCR1009] > :set ($array->"el0") "el0_val"
[admin@rack1_b36_CCR1009] > :environment print
array={el0="el0_val"}
```
