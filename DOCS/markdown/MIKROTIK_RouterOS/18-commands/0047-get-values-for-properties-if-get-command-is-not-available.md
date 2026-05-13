## Get values for properties if 'get' command is not available 

For example, how do you get usable output for scripting from `/interface wireless info hw-info` command? Use as-value: 

```
[admin@1p_DUT_wAP ac] /interface wireless info> :put [hw-info wlan1 as-value ]
ranges=2312-2732/5/b;g;gn20;gn40;2484-2484/5/b;g;gn20;gn40;rx-chains=0;1;tx-chains=0;1
```

Output is 1D array so you can easily get interested property value 

```
[admin@1p_DUT_wAP ac] /interface wireless info> :put ([hw-info wlan1 as-value ]->"tx-chains")
0;1
```

1124
