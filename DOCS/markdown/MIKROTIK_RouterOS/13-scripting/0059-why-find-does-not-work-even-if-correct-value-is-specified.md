## Why find does not work even if correct value is specified? 

Lets say we want to print specific address: 

```
[admin@rack1_b34_CCR1036] /ip address> print where address=111.111.1.1/24
Flags: X - disabled, I - invalid, D - dynamic
```

```
#   ADDRESS            NETWORK         INTERFACE
```

So why it does not work? 

Console tries to convert variable types as hard as it can, but it is not always possible to do it correctly, so lets look closely why this particular example does not work. First lets check what variable type "address" is: 

1123 

```
[admin@rack1_b34_CCR1036] /ip address> :put [:typeof ([print as-value]->0->"address")]
str
```

So obviously we are comparing string to ip-prefix. And conversion from ip-prefix to string does not happen, so what we can do to solve the problem? Convert variable to correct format: 

```
[admin@rack1_b34_CCR1036] /ip address> print where address=[:tostr 111.111.1.1/24]
```

```
Flags: X - disabled, I - invalid, D - dynamic
#   ADDRESS            NETWORK         INTERFACE
0   111.111.1.1/24     111.111.1.0     ether2
```
