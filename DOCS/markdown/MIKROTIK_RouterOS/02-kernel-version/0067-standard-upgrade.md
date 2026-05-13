## Standard upgrade 

The package upgrade feature connects to the MikroTik download servers and checks if there is another RouterOS version for your device under the selected release channel. Can also be used for downgrading, if you, for example, are using stable release at the moment, but changed the release channel to the long-term. 

After clicking the Check For Updates button in QuickSet (or in the System → Packages menu) the Check For Updates window will open with the current or the latest changelog (if a newer version exists). If newer version exists, buttons Download and Download&Install will appear. By cicking the Download button a newest version will be downloaded (manual device reboot is required), by clicking Download&Install, download will start, and after a successful download will reboot a device to install the downloaded packages. 

The versions offered will depend on the selected release channel. Not all versions migh be available. It will not be possible to upgrade from an older version to the latest version in one go, when using check-for-updates approach. For example, if running RouterOS v6.x, even selecting the major release upgrade channel, called "Upgrade", you will only see v7.12.1 as the available version. You must first upgrade to that intermediate version and only then newer releases will be available in the channels. This intermediate step can be done using check for updates too, but you will simply have to repeat check for updates after the first update to the intermediate version. 

If custom packages are installed, the downloader will take that into account and download all necessary packages. 

**==> picture [13 x 13] intentionally omitted <==**

It is strongly recommended to upgrade the bootloader after RouterOS update. To upgrade the bootloader, execute command "/system routerboard upgrade" in CLI, followed by a reboot. Alternatively, navigate to the GUI System → RouterBOARD menu and click the "Upgrade" button, then reboot the device. 

40 

**==> picture [505 x 286] intentionally omitted <==**

41 

**==> picture [505 x 413] intentionally omitted <==**

42 

**==> picture [505 x 421] intentionally omitted <==**

43 

**==> picture [505 x 12] intentionally omitted <==**

You can automate the upgrade process by running a script in the system scheduler. This script queries the MikroTik upgrade servers for new versions, if the response received says "New version is available", the script then issues the upgrade command below. Important note, this will not work, if you are running it for the first time on a release that is older. It might not see latest versions as available, if you are running v6.x, you would first have to manually select the "Upgrade" channel to do a major release upgrade to v7.12.1 intermediate version, and only afterwards newer v7 releases will be visible in the upgrade channels. 

```
[admin@MikroTik] >/system package update
check-for-updates once
:delay 3s;
```

```
:if ( [get status] = "New version is available") do={ install }
```
