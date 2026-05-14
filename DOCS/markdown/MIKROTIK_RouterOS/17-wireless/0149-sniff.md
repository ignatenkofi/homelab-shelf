## Sniff 

Sniff mode allows to capture nearby 802.11ad frames. To use sniff mode same frequency needs to be used and interface operational mode needs to be set to sniff: 

```
/interface w60g set wlan60-1 mode=sniff
```

Now this interface can be used in Tools/Packet Sniffer for packet capture. Sniffer mode can't be used together with regular interface working modes.
