## Decode-ad 

In this menu, you can decode static MikroTik, Eddystone TLM, Eddystone UID and iBeacon payloads. 

To decode a payload, just input it into the "data" field: 

1563 

```
/iot bluetooth decode-ad data=0201060303AAFE1116AAFE20000B6E158402353AF20238576B
             type: eddystone-tlm
          version: 0
  battery-voltage: 2.926V
      temperature: 21.515C
     packet-count: 37042930
           uptime: 3724682.7s
/iot bluetooth decode-ad data=15FF4F090100032E0100FFFF00004F17C1E80F000064
         type: mikrotik
      version: 1
    encrypted: no
        acc-x: 0.003G
        acc-y: -0.003G
        acc-z: 0G
  temperature: 23.308C
       uptime: 1042625s
        flags:
      battery: 100%
```

1564
