## Operations with Arrays 

Warning: Key name in the array contains any character other than a lowercase character, it should be put in quotes 

For example: 

```
[admin@ce0] > {:local a { "aX"=1; ay=2 }; :put ($a->"aX")}
1
```

Loop through keys and values 

"foreach" command can be used to loop through keys and elements: 

```
[admin@ce0] > :foreach k,v in={2; "aX"=1; y=2; 5} do={:put ("$k=$v")}
0=2
1=5
aX=1
y=2
```

If the "foreach" command is used with one argument, then the element value will be returned: 

```
[admin@ce0] > :foreach v in={2; "aX"=1; y=2; 5} do={:put ("$v")}
2
5
1
2
```

Note: If the array element has a key then these elements are sorted in alphabetical order, elements without keys are moved before elements with keys and their order is not changed (see example above). 

1109 

Change the value of a single array element 

```
[admin@MikroTik] > :global a {x=1; y=2}
[admin@MikroTik] > :set ($a->"x") 5
[admin@MikroTik] > :environment print
a={x=5; y=2}
```
