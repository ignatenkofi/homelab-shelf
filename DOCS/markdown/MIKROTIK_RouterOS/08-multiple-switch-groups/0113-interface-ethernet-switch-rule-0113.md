## `/interface ethernet switch rule` 

```
add new-qos-profile=stream ports=ether1,ether2 src-mac-address=00:01:02:00:00:00/FF:FF:FF:00:00:00
switch=switch1
```

```
add new-qos-profile=voip ports=ether1,ether2 src-mac-address=04:05:06:00:00:00/FF:FF:FF:00:00:00 switch=switch1
```
