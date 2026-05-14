## Menu: /system package 

Commands executed in this menu will take place only on restart of the router. Until then, the user can freely schedule or revert set actions. 

**==> picture [516 x 129] intentionally omitted <==**

**----- Start of picture text -----**<br>
Command Description<br>disable schedule the package to be disabled after the next reboot. No features provided by the package will be accessible<br>downgrade will prompt for the reboot. During the reboot process will try to downgrade the RouterOS to the oldest version possible by checking the<br>packages that are uploaded to the router.<br>enable schedule package to be enabled after the next reboot<br>uninstall schedule package to be removed from the router. That will take place during the reboot.<br>unschedule remove scheduled task for the package.<br>**----- End of picture text -----**<br>

52 

print outputs information about the packages, like: version, package state, planned state changes, etc. update manages the "check-for-updates" channel and performs RouterOS upgrades applyapply scheduled changes and reboot device changes 

Menu: /system/check-installation 

The "Check installation" function ensures the integrity of the RouterOS system by verifying the readability and correct placement of files. Its primary purpose is to confirm the health and status of your NAND/Flash storage. 

Menu: /system/package/update install ignore-missing command allows upgrading only the RouterOS main package, while omitting packages that are either missing or not uploaded during a manual upgrade process.
