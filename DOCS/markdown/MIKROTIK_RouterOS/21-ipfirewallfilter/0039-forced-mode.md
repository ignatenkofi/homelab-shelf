## Forced Mode 

In the situation when a warning message appears in the log records after connecting the DAC cable or optical module, as example: 

1297 

```
10:20:47 interface,warning sfp-sfpplus1 module auto-initialization failed, try forced-mode
```

This may indicate that the connected cable or module has a corrupted or bad EEPROM checksum, which causes the automatic connection configuration to fail. This functionality was introduced in RouterOS version 7.12 and may affect some links that worked in the past by mistake with wrongly assumed module /cable attributes, which could lead to various problems related to link connection and device functionality. 

In such cases, you can attempt to set the link mode manually, and this might help establish a working link. The following forced port setting examples are provided: 

For DAC cables and connection speeds of 1G/10G/25G: 

```
/interface ethernet
```

```
set [ find default-name=sfp-sfpplus1 ] auto-negotiation=no speed=1G-baseT-full
set [ find default-name=sfp-sfpplus1 ] auto-negotiation=no speed=10G-baseCR
set [ find default-name=sfp-sfpplus1 ] auto-negotiation=no speed=25G-baseCR
```

**==> picture [13 x 13] intentionally omitted <==**

Note: When selecting the interface speed setting, pay attention to what rates your DAC cable supports (check cable specification data) 

For optical modules and connection speeds of 1G/10G/25G: 

```
/interface ethernet
```

```
set [ find default-name=sfp-sfpplus1 ] auto-negotiation=no speed=1G-baseX
set [ find default-name=sfp-sfpplus1 ] auto-negotiation=no speed=10G-baseSR-LR
set [ find default-name=sfp-sfpplus1 ] auto-negotiation=no speed=25G-baseSR-LR
```

**==> picture [13 x 13] intentionally omitted <==**

Note: When selecting the interface speed setting, pay attention to what rates your optical module supports (check module specification data) 

**==> picture [13 x 13] intentionally omitted <==**

Note : Modules with bad EEPROM checksum do not output any EEPROM information to the ethernet monitor, which will also mean that the sfp DDM monitor does not work for such modules.
