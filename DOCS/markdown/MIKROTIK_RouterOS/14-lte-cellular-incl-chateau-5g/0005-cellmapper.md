## CellMapper 

By using those acquired variables it's possible to send the AT command to modem for locking to tower in the current format: 

for R11e-LTE and R11e-LTE6 

819 

```
AT*Cell=<mode>,<NetworkMode>,<band>,<EARFCN>,<PCI>
```

```
where
```

```
<mode> :
0 – Cell/Frequency disabled
1 – Frequency lock enabled
2 – Cell lock enabled
```

```
<NetworkMode>
0 – GSM
1 – UMTS_TD
2 – UMTS_WB
3 – LTE
```

```
<band>
Not in use, leave this blank
```

```
<EARFCN>
earfcn from lte info
```

```
<PCI>
phy-cellid from lte info
```

To lock modem at previously used tower at-chat can be used: 

```
/interface lte at-chat lte1 input="AT*Cell=2,3,,1300,384"
```

For R11e-LTE all set on locks are lost after reboot or modem reset. Cell data can be also gathered from "cell-monitor". 

For R11e-LTE6 cell lock works only for the primary band, this can be useful if you have multiple channels on the same band and you want to lock it to a specific earfcn. Note, that cell lock is not band-specific and for ca-band it can also use other frequency bands, unless you use band lock. 

Use cell lock to set the primary band to the 1300 earfcn and use the second channel for the ca-band: 

```
/interface lte at-chat lte1 input="AT*Cell=2,3,,1300,138"
```

Now it uses the earfcn: 1300 for the primary channel: 

```
        primary-band: B3@20Mhz earfcn: 1300 phy-cellid: 138
             ca-band: B3@5Mhz earfcn: 1417 phy-cellid: 138
```

You can also set it the other way around: 

```
/interface lte at-chat lte1 input="AT*Cell=2,3,,1417,138"
```

Now it uses the earfcn: 1417 for the primary channel: 

```
        primary-band: B3@5Mhz earfcn: 1417 phy-cellid: 138
             ca-band: B3@20Mhz earfcn: 1300 phy-cellid: 138
```

For R11e-LTE6 modem cell lock information will not be lost after reboot or modem reset. To remove cell lock use at-chat command: 

```
/interface lte at-chat lte1 input="AT*Cell=0"
```

for R11e-4G 

820 

```
AT%CLCMD=<mode>,<mode2>,<EARFCN>,<PCI>,<PLMN>
AT%CLCMD=1,1,3250,244,\"24705\"
```

```
where
```

```
<mode> :
0 – Cell/Frequency disabled
1 – Cell lock enabled
```

```
<mode2> :
0 - Save lock for first scan
```

```
1 - Always use lock
```

```
(after each reset modem will clear out previous settings no matter what is used here)
```

```
<EARFCN>
earfcn from lte info
```

```
<PCI>
phy-cellid from lte info
```

```
<PLMN>
Mobile operator code
```

All PLMN codes available here this variable can be also left blank 

To lock the modem to the cell - modem needs to be in non operating state, the easiest way for R11e-4G modem is to add CellLock line to "modem-init" string: 

```
/interface lte set lte1 modem-init="AT%CLCMD=1,1,3250,244,\"24705\""
```

Multiple cells can also be added by providing a list instead of one tower information in the following format: 

```
AT%CLCMD=<mode>,<mode2>,<EARFCN_1>,<PCI_1>,<PLMN_1>,<EARFCN_2>,<PCI_2>,<PLMN_2>
```

For example to lock to two different PCIs within the same band and operator: 

```
/interface lte set lte1 modem-init="AT%CLCMD=1,1,6300,384,\"24701\",6300,385,\"24701\""
```
