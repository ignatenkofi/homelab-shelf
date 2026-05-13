## Simple L7 usage example 

First, add Regexp strings to the protocols menu, to define the strings you will be looking for. In this example, we will use a pattern to match RDP packets. 

664 

```
/ip firewall layer7-protocol
```

```
add name=rdp regexp="rdpdr.*cliprdr.*rdpsnd"
```

Then, use the defined protocols in the firewall. 

```
/ip firewall filter
```

```
# add few known protocols to reduce mem usage
```

```
add action=accept chain=forward comment="" disabled=no port=80 protocol=tcp
add action=accept chain=forward comment="" disabled=no port=443 protocol=tcp
```

```
# add l7 matcher
```

```
add action=accept chain=forward comment="" disabled=no layer7-protocol=\
    rdp protocol=tcp
```

As you can see before the l7 rule we added several regular rules that will match known traffic thus reducing memory usage.
