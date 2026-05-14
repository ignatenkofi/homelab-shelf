## Example to lock to LTE band 7: 

```
[admin@MikroTik] /interface lte set lte1 modem-init="AT^SYSCFGEX=\"03\",3FFFFFFF,2,4,40,,"
```

Change last part 40 to desired band specified hexadecimal value where: 

```
4 LTE BC3
40 LTE BC7
80000 LTE BC20
7FFFFFFFFFFFFFFF  All bands
etc
```

All band HEX values and AT commands can be found in Huawei AT Command Interface Specification guide 

Check if the band is locked: 

```
[admin@MikroTik] /interface lte at-chat lte1 input="AT^SYSCFGEX\?"
```

```
output: ^SYSCFGEX: "03",3FFFFFFF,0,2,40
OK
```

For more information check modem manufacturers AT command reference manuals.
