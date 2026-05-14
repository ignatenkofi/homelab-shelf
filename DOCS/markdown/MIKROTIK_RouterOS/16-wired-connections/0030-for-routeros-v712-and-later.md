## For RouterOS v7.12 and later: 

```
# 1x100G - DAC
```

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=100G-baseCR4
```

```
# 1x100G - Optical
```

```
/interface ethernet set qsfp28-2-1 auto-negotiation=no speed=100G-baseSR4-LR4
```

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

```
# 4x25G - DAC
```

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseCR
/interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseCR
/interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25G-baseCR
/interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25G-baseCR
```

```
# 4x25G - Optical
```

```
/interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseSR-LR
/interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseSR-LR
/interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25G-baseSR-LR
/interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25G-baseSR-LR
```

**==> picture [13 x 13] intentionally omitted <==**

In single-link mode, only the first QSFP28 sub-interface needs to be configured, while the remaining sub-interfaces should remain enabled. Similarly, for 2x50G link mode, only the master interfaces (e.g., qsfp28-1-1 and qsfp28-1-3) need to be configured, but the other sub-interfaces must remain enabled.
