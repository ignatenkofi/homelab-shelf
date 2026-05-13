## For RouterOS v7.12 and later: 

```
# 1x40G - DAC
/interface ethernet set qsfpplus1-1 auto-negotiation=no speed=40G-baseCR4
```

```
# 1x40G - Optical
/interface ethernet set qsfpplus1-1 auto-negotiation=no speed=40G-baseSR4-LR4
```

```
# 4x10G - DAC
```

```
/interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10G-baseCR
/interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10G-baseCR
/interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10G-baseCR
/interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10G-baseCR
```

```
# 4x10G - Optical
/interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10G-baseSR-LR
/interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10G-baseSR-LR
/interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10G-baseSR-LR
/interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10G-baseSR-LR
```

**==> picture [13 x 13] intentionally omitted <==**

In single-link mode, only the first QSFP+ sub-interface needs to be configured, while the remaining sub-interfaces should remain enabled.
