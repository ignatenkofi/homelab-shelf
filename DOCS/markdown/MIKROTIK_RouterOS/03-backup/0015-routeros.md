## RouterOS 

If your device is able to boot up and you are able to log in, then you can easily put the device into Etherboot mode. To do so, just connect to your device and execute the following command: 

```
/system routerboard settings set boot-device=try-ethernet-once-then-nand
```

After that either reboot the device or do a power cycle on the device. Next time the device will boot up, then it will first try going into Etherboot mode. Note that after the first boot up, the device will not try going into Etherboot mode and will boot directly from NAND or from the storage type the device is using.
