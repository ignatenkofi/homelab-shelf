## Blacklists 

Unless you are using a lot of knocks, a simple port scan could accidentally trigger the correct ports in the correct order, so it is advisable to add a blacklist as well. 

At the very top of your firewall stack add a drop rule for the blacklist. 

```
/ip/firewall/filter add action=drop chain=input disabled=yes in-interface-list=WAN src-address-list=blacklist
```

Then add suspicious IPs to the blacklist. 

Bad ports - ones that will never be used by a trusted user and hence have a high timeout penalty. 

```
/ip/firewall/filter add action=add-src-to-address-list address-list=blacklist address-list-timeout=1000m
chain=input disabled=yes dst-port=666 in-interface-list=WAN protocol=tcp
```

Ports that slow down the port scanning process significantly to the point where it is pointless, but will never lock out a real user for too long. This could include every single port apart from the 'knock' ports, the key is that the source IP is not already in the secure list and hence those ports can be used after a successful knock. 

740 

```
/ip/firewall/filter add action=add-src-to-address-list address-list=blacklist address-list-timeout=1m
chain=input disabled=yes dst-port=21,22,23,8291,10000-60000 in-interface-list=WAN protocol=tcp src-address-
list=!secured
```

**==> picture [13 x 13] intentionally omitted <==**

Blacklist rules from this section are added disabled=yes in order to avoid locking out the user. Enable the filter rules, once the alternative access available or use <Safe Mode>
