## QSFP+/QSFP28 interface compatibility with breakout cables 

MikroTik devices can establish links between QSFP+/QSFP28 and SFP+/SFP28 ports using breakout cables. 

Configuration Examples: 

For RouterOS v7.12 and later: 

```
# QSFP+ - DAC
```

```
/interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10G-baseCR
/interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10G-baseCR
/interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10G-baseCR
/interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10G-baseCR
```

```
# QSFP+ - Optical
```

```
/interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10G-baseSR-LR
/interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10G-baseSR-LR
/interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10G-baseSR-LR
/interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10G-baseSR-LR
```
