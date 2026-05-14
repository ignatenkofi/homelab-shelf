## Setup example 

We are assuming you have already set up a firewall that drops all connection attempts from the WAN port, so you will need to add additional rules before that. 

First, create a firewall rule that listens on a given port and adds the connected source IP to an address list - this is the first knock. 

```
/ip/firewall/filter add action=add-src-to-address-list address-list=888 address-list-timeout=30s chain=input
dst-port=888 in-interface-list=WAN protocol=tcp
```

Then add a rule that does the same on another port, but only approves IPs that are already in the first list. You can repeat this step as many times as you like. 

```
/ip/firewall/filter add action=add-src-to-address-list address-list=555 address-list-timeout=30s chain=input
dst-port=555 in-interface-list=WAN protocol=tcp src-address-list=888
```

Finally, the last knock will be added to an IP list that is trusted and any input is accepted. 

```
/ip/firewall/filter add action=add-src-to-address-list address-list=secured address-list-timeout=30m
chain=input dst-port=222 in-interface-list=WAN protocol=tcp src-address-list=555
```

```
/ip/firewall/filter add action=accept chain=input in-interface-list=WAN src-address-list=secured
```
