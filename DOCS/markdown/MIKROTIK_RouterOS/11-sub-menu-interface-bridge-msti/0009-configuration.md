## Configuration 

Start by creating a new bridge on AP and ST and add ether1 and wlan1 ports to it: 

```
/interface bridge
add name=bridge protocol-mode=none
/interface bridge port
add bridge=bridge interface=ether1
add bridge=bridge interface=wlan1
```

**==> picture [13 x 13] intentionally omitted <==**

You can enable RSTP if it is required, but generally, RSTP is not required for PtP links since there should not be any way for a loop to occur. 

For security reasons you should enable ingress-filtering since you are expecting only tagged traffic, then you can set the bridge to filter out all untagged traffic. Do the following on AP and ST :
