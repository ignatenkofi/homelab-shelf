## Or to configure different speed rates for each QSFP+/QSFP28 sub-interfaces: 

```
# QSFP28 - DAC
```

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseCR
/interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseCR
/interface ethernet set qsfp28-1-3 auto-negotiation=no speed=10G-baseCR
/interface ethernet set qsfp28-1-4 auto-negotiation=no speed=10G-baseCR
```

```
# QSFP28 - Optical
```

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseSR-LR
/interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseSR-LR
/interface ethernet set qsfp28-1-3 auto-negotiation=no speed=10G-baseSR-LR
/interface ethernet set qsfp28-1-4 auto-negotiation=no speed=10G-baseSR-LR
```
