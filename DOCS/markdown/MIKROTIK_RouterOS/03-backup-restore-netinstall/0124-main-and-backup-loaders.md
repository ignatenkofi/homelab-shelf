## Main and Backup loaders 

By default, the main (regular) loader is used, but RouterBOARD devices also have a secondary (backup) bootloader, which can be used in case the main doesn't work. It is possible to call the backup loader with a configuration setting in RouterOS: 

```
system/routerboard/settings/set force-backup-booter=yes
```

It is also possible to use the backup booter by turning on the device, with the RESET button pushed. It is only possible to upgrade the main RouterBOOT, so in case of failure, you can use the backup booter to start the device and downgrade the main loader. For upgrade instructions, follow the separate instructions in RouterBOARD#UpgradingRouterBOOT
