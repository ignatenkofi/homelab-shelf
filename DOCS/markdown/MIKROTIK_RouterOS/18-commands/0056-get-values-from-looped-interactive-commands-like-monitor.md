## Get values from looped interactive commands like "monitor" 

Frequently asked question s how to get values in script returned by, for example, monitor command? First problem with such commands is that they are running infinitely until user action is applied, obviously you cannot do that from script. Instead you can run with additional parameter once, it will allow to execute command only once and stop. Another problem is getting variable value sin script, there is no as-value, there is no get, but they have do. What it does is allows to access variables returned by the command as in example below: 

```
[admin@1p_DUT_wAP ac] /interface> monitor-traffic ether1 once do={:global myBps $"rx-bits-per-second" }
...
```

```
[admin@1p_DUT_wAP ac] /interface> :environment print
myBps=71464
```
