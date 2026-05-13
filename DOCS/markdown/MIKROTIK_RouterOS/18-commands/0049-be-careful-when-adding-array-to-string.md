## Be careful when adding array to string 

If you want to print an array or add an array to existing string, be very careful as it may lead to unexpected results. For example ,we have array with two elements and we want to print the array value on screen: 

```
[admin@1p_DUT_wAP ac] /> :global array {"cccc", "ddddd"}
```

```
[admin@1p_DUT_wAP ac] /> :put ("array value is: " . $array )
array value is: cccc;array value is: ddddd
```

Obviously this is not what we expected, because what . does is adds string to each array element and then prints the output. Instead you need to convert to string first: 

```
[admin@1p_DUT_wAP ac] /> :put ("array value is: " . [:tostr  $array] )
array value is: cccc;ddddd
```
