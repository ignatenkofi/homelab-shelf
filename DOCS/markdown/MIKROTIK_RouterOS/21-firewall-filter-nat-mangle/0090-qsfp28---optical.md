## `# QSFP28 - Optical` 

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseSR-LR
/interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseSR-LR
/interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25G-baseSR-LR
/interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25G-baseSR-LR
```

It is also possible to use QSFP28 to 2x50G QSFP28 Breakout Cables: 

1325 

```
# 2x50G - DAC
```

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=50G-baseCR2
/interface ethernet set qsfp28-1-3 auto-negotiation=no speed=50G-baseCR2
```

```
# 2x50G - Optical
```

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=50G-baseSR2-LR2
/interface ethernet set qsfp28-1-3 auto-negotiation=no speed=50G-baseSR2-LR2
```
