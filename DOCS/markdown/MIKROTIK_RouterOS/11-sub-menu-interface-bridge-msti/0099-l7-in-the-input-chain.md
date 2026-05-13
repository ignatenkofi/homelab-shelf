## L7 in the input chain 

In this example, we will try to match the telnet protocol connecting to our router. 

```
/ip firewall layer7-protocol add comment="" name=telnet regexp="^\\xff[\\xfb-\\xfe].\\xff[\\xfb-\\xfe].\\xff
[\\xfb-\\xfe]"
```

Note that we need both directions which is why we need also the l7 rule in the output chain that sees outgoing packets. 

```
/ip firewall filter
```

```
add action=accept chain=input comment="" disabled=no layer7-protocol=telnet \
    protocol=tcp
```

```
add action=passthrough chain=output comment="" disabled=no layer7-protocol=telnet \
    protocol=tcp
```
