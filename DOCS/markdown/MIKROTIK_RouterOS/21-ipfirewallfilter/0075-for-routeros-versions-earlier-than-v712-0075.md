## For RouterOS versions earlier than v7.12: 

```
# 1x100G - DAC/Optical
```

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=100Gbps full-duplex=yes
```

```
# 4x25G - DAC/Optical
```

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25Gbps full-duplex=yes
/interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25Gbps full-duplex=yes
/interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25Gbps full-duplex=yes
/interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25Gbps full-duplex=yes
```
