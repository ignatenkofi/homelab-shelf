## Or use string directly: 

```
[admin@rack1_b34_CCR1036] /ip address> print where address="111.111.1.1/24"
```

```
Flags: X - disabled, I - invalid, D - dynamic
#   ADDRESS            NETWORK         INTERFACE
0   111.111.1.1/24     111.111.1.0     ether2
```

Obviously second method is not suitable if you are getting ip prefix from a variable, then conversion should be done as in first example or by writing variable to string with "$myVar".
