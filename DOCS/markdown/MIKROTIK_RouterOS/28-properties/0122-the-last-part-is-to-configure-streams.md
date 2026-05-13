## The last part is to configure streams 

```
/tool traffic-generator stream
add disabled=no mbps=500 name=str1 id=3 packet-size=1450 port=port0 pps=0 \
    tx-template=routing-1
add disabled=no mbps=500 name=str3 id=4 packet-size=1450 port=port1 pps=0 \
    tx-template=routing-2
```

Notice that each stream has a unique  value. This value identifies stream packets, otherwise, the traffic generator will not work. id
