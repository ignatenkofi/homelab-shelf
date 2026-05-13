## For RouterOS versions earlier than v7.12: 

```
# 1x40G - DAC/Optical
/interface ethernet set qsfpplus1-1 auto-negotiation=no speed=40Gbps full-duplex=yes
```

```
# 4x10G - DAC/Optical
/interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10Gbps full-duplex=yes
/interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10Gbps full-duplex=yes
/interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10Gbps full-duplex=yes
/interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10Gbps full-duplex=yes
```
