## Upgrading RouterBOOT 

1744 

RouterBOOT upgrades usually include minor improvements to overall RouterBOARD operation. It is recommended to keep this version upgraded. If you see that the upgrade-firmware value is bigger than current firmware , you simply need to perform the upgrade command, accept it with  and then reboot y with /system reboot 

```
 [admin@mikrotik] /system routerboard> upgrade
Do you really want to upgrade firmware? [y/n]
y
```

```
echo: system,info,critical Firmware upgraded successfully, please reboot for changes to take effect!
```

After rebooting, the current-firmware value should become identical with upgrade-firmware
