## For RouterOS versions earlier than v7.12: 

```
# QSFP+ - DAC/Optical
```

```
/interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10Gbps full-duplex=yes
/interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10Gbps full-duplex=yes
/interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10Gbps full-duplex=yes
/interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10Gbps full-duplex=yes
```

```
# QSFP28 - DAC/Optical
```

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25Gbps full-duplex=yes
/interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25Gbps full-duplex=yes
/interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25Gbps full-duplex=yes
/interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25Gbps full-duplex=yes
```

1326
