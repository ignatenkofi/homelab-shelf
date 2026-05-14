## Always check what value and type command returns 

Lets say we want to get gateway of specific route using as-value, if we execute following command it will return nothing 

```
[admin@rack1_b36_CCR1009] /ip address> :put ([/ip route print as-value where gateway="ether1"]->"gateway")
```

Command assumes that output will be 1D array from which we could extract element gateway. 

At first lets check if print is actually find anything: 

```
[admin@rack1_b36_CCR1009] /ip address> :put ([/ip route print as-value where gateway="ether1"])
.id=*400ae12f;distance=255;dst-address=111.111.111.1/32;gateway=ether1;pref-src=111.111.111.1
```

So obviously there is something wrong with variable itself or variable type returned. Lets check it more closely: 

```
[admin@rack1_b36_CCR1009] /ip address> :global aa ([/ip route print as-value where gateway="ether1"
])
```

```
[admin@rack1_b36_CCR1009] /ip address> :environment print
aa={{.id=*400ae12f; distance=255; dst-address=111.111.111.1/32; gateway={"ether1"}; pref-src=111.11
1.111.1}}
```

Now it is clear that returned value is 2D array with one element. So the right sequence to extract gateway will be: 

get 2d array get first element 

get "gateway" from picked element 

```
[admin@rack1_b36_CCR1009] /ip address> :put ([:pick [/ip route print as-value where gateway="ether1"] 0]->"
gateway")
ether1
```
