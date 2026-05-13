## Checking RouterBOOT version 

This command shows the current RouterBOOT version of your device and the available upgrade which is included in routeros-x.yy.npk package, or if you uploaded a *.FWF file corresponding to the device model: 

```
[admin@admin] >  system/routerboard/print
                ;;; Firmware upgraded successfully, please reboot for changes
                    to take effect!
       routerboard: yes
        board-name: hAP ac
             model: RouterBOARD 962UiGS-5HacT2HnT
     serial-number: 6737057562DD
     firmware-type: qca9550L
  factory-firmware: 3.29
  current-firmware: 6.49.5
  upgrade-firmware: 7.4beta5
```

In this case, you see, there is a newer version of the Bootloader firmware available already inside your current RouterOS version and it has been updated and requires a reboot. 

**==> picture [13 x 13] intentionally omitted <==**

A downgrade is also possible by uploading *.FWF file with an older version may be required for troubleshooting purposes when contacting MikroTik support. 

149
