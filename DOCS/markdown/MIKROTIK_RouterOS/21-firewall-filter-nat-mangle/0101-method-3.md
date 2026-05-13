## Method 3 

It is also possible to set a specified role for the PWR-Line device (master or slave) with the plc-cco-selection-mode parameter. 

Property Description 

1328 

plc-cco-selection-mode (auto | always | never; Sets PWR-Line device mode: Default: auto ) 

auto - PWR-Line will automatically decide what role to take depending on the situation upon joining a PWR-Line network. always - PWR-Line will always be forced to act as "central-coordinator" or master device. never - PWR-Line will always be forced to act as a slave device. 

Example: 

```
/interface pwr-line configure pwr-line1 plc-cco-selection-mode=auto
```

```
/interface pwr-line configure pwr-line1 plc-cco-selection-mode=always
```

```
/interface pwr-line configure pwr-line1 plc-cco-selection-mode=never
```
