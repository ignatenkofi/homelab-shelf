## Do not use console numbers to get parameter values 

Lets start with very basics. When you work with console to access parameters, you are used to following syntax: 

```
[admin@rack1_b34_CCR1036] /interface> print
Flags: D - dynamic, X - disabled, R - running, S - slave
```

```
#     NAME                                TYPE       ACTUAL-MTU L2MTU  MAX-L2MTU
```

```
0  R  ether1                              ether            1500  1580      1022
```

```
[admin@rack1_b34_CCR1036] /interface> set 0 name=LAN
```

What print command does is temporary saves buffer with id numbers referencing to internal ID numbers, so obviously if you are trying to use non-existent buffer values script will fail, like, for example this script: 

```
/system script add name=script1 source={
 /ip route set 0 gateway=3.3.3.3
}
```

Script does not know what you assume by "1" and will throw an error. Proper way is to use internal ID numbers, those numbers can be seen if you are doing `print as-value` or returned by find command, for example: 

```
[admin@rack1_b34_CCR1036] /ip route> :put [find where dst-address="10.0.0.0/8"]
```

```
*1
```

So in this case proper script would be: 

```
/system script add name=script1 source={
 /ip route set *1 gateway=3.3.3.3
}
```

Note that it is not recommended to use internal numbers directly, since items can be removed and re-added in which case internal id number will change and script will fail again, so instead use find command directly in your code: 

```
/system script add name=script1 source={
```

```
 /ip route set [find dst-address="0.0.0.0/0"] gateway=3.3.3.3
}
```
