## LTE settings 

LTE and router-specific LTE settings. The menu is available starting from RouterOS v7. 

```
Sub-menu: /interface lte settings
```

**==> picture [516 x 249] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>mode  (auto | mbim | serial  user/ ; Default:  Operation mode setting.<br>auto )<br>auto - automatically select the operation mode.<br>serial - provide only serial ports<br>mbim - switch modem into MBIM mode if possible<br>user - OS will not attempt to automatically switch the modem mode. (Available from RouterOS 7.16)<br>firmware-path  (string) Firmware path in host OS. Modem gobi firmware<br>external-antenna  (auto | both | div | main  This setting is only available for "Chateau" routers, except for Chateau 5G versions.<br>| none; Default:  auto )<br>auto - measures the signal levels on both internal and external antennas and selects the antennas with<br>the best signal(RSRP).<br>both - both antennas are set to external<br>div - diversity antenna set to external<br>main - main antenna set to external<br>none - no external antenna selected(using internal antennas)<br>external-antenna-selected  () This setting is only available for "Chateau" routers, except for Chateau 5G versions. Shows the currently<br>selected antenna if " external-antenna " is set to "auto"<br>**----- End of picture text -----**<br>

811 

sim-slot () 

This setting is available for routers that have switchable SIM slots (LtAP, SXT). Selection options differ between products.
