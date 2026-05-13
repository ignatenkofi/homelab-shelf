## Always use unique variable names 

One of the most common scripting mistakes that most users are doing is not using unique varible names, for example, variable defined in function has the same name as globally defined variable, which leads to unexpected result: 

```
:global my2 "123"
```

```
:global myFunc do={ :global my2; :put $my2; :set my2 "lala"; :put $my2 }
$myFunc my2=1234
:put "global value $my2"
```

Output will be: 

```
1234
lala
global value 123
```

Another common case is when user defined variable have the same name as RouterOS built in variable, for example, we want to print route with dst address defined in variable: 

```
[admin@1p_DUT_wAP ac] /ip route> :global "dst-address" "0.0.0.0/0"
[admin@1p_DUT_wAP ac] /ip route> print where dst-address=$"dst-address"
Flags: X - disabled, A - active, D - dynamic, C - connect, S - static, r - rip, b - bgp, o - ospf, m - mme,
B - blackhole, U - unreachable, P - prohibit
#      DST-ADDRESS        PREF-SRC        GATEWAY            DISTANCE
0 ADS  0.0.0.0/0                          10.155.136.1              1
1 ADC  10.155.136.0/24    10.155.136.41   ether1                    0
```

Obviously result is not as expected, simple solution, use unique variable name: 

```
[admin@1p_DUT_wAP ac] /ip route> :global myDst "0.0.0.0/0"
[admin@1p_DUT_wAP ac] /ip route> print where dst-address=$myDst
Flags: X - disabled, A - active, D - dynamic, C - connect, S - static, r - rip, b - bgp, o - ospf, m - mme,
B - blackhole, U - unreachable, P - prohibit
#      DST-ADDRESS        PREF-SRC        GATEWAY            DISTANCE
0 ADS  0.0.0.0/0                          10.155.136.1              1
```
