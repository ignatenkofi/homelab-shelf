## Manual upgrade process 

First step - visit www.mikrotik.com and head to the Software page, then choose the architecture of the system you have the RouterOS installed on (system architecture can be found in System → Resource section); Download the routeros (main) and extra packages that are installed on a device; 

Upload packages to a device using one of the previously mentioned methods: 

Menu: /system/package/update install ignore-missing command allows upgrading only the RouterOS main package, while omitting packages that are either missing or not uploaded during a manual upgrade process.
