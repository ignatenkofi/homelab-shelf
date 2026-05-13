## Run the tool: 

```
sudo ./netinstall-cli [-parameters] [address/interface] routeros-arm64-[package VERSION].npk
```

**==> picture [13 x 13] intentionally omitted <==**

The tool requires privileged access and must be run as root, use sudo. 

96 

The available parameters are as follows: 

**==> picture [516 x 602] intentionally omitted <==**

**----- Start of picture text -----**<br>
Parameter Meaning<br>-r When the reinstallation process is performed, the current configuration will be reset, and for devices that have it, the default configuration<br>will be applied (optional).<br>-e Performing the reinstallation process will reset the device to an empty configuration.<br>-b Option to discard the currently installed branding package from the device, otherwise it will be reinstalled together with RouterOS.<br>-m Enables multiple device reinstallation.<br>Available options:<br>No "-m", no "-o" chosen  – Only one successful installation will proceed, and Netinstall will close afterward.<br>"-m" only  – Enables multiple device reinstallation. The same device will be reinstalled as many times as BOOTP requests are sent.<br>"-o" only  – Functions the same as when neither "-m" nor "-o" is chosen: only one successful installation will proceed, and Netinstall will<br>close afterward.<br>Both "-m" and "-o"  – Enables multiple device reinstallation. The same device will be reinstalled only once per Netinstall run.<br>-o When using the netinstall tool with the "-o" option, devices can only be installed once per netinstall run. This means that during the<br>netinstall process, the tool will keep track of the MAC addresses of devices that were successfully installed. If a device with the same<br>MAC address tries to reinstall during the same run, the tool will ignore it and not<br> respond to its BOOTP requests.<br>-f Ignore size constraints. Netinstall-cli checks the storage size on the router. If the total size of the selected packages exceeds the device's<br>available storage, an error will be displayed:  "Ignoring XX:XX:XX:XX:XX:XX, not enough space (override with -f)"<br>-c Allow to run multiple Netinstall instances on the same computer.<br>-v Verbose mode<br>-k <keyfile> Provides the device with a license key in .KEY format (optional).<br>-s  Pre-configures the device with the provided configuration (text file in .RSC format), removing the existing configuration before applying<br><userscript> the new one. This configuration also replaces the default configuration. The script can access factory passwords with read-only variables<br>$defconfPassword and $defconfWifiPassword (starting from RouterOS 7.10beta8) (optional).<br>--mac <mac  Specifies MAC address which will be allowed to be installed. When a MAC address is provided, all other BOOTP requests are<br>address> disregarded.<br>-i  Allows you to specify an interface (optional).<br><interface><br>-a <IP  Uses a specific IP address that the Netinstall server will assign to the device. Mandatory, but can be auto-assigned if interface parameter<br>address> used.<br>PACKAGE Specify a list of RouterOS.NPK format packages that Netinstall will try to install on the device (mandatory).  The system package must be<br>listed first.<br>If the "-r" or "e-" parameter is not specified, netinstall-cli will reinstall RouterOS  and will keep the current configuration by downloading current<br>configuration database from the router, reinstalling the router (including disk formatting), and uploading the configuration back to it, the same<br>as  Netinstall  "Keep old configuration"  option. However, it's important to note that this process solely applies to the configuration itself and does<br>not impact the files, including databases like the User Manager database, Dude database, and others.<br>**----- End of picture text -----**<br>


First make sure you have set the IP on your computer's interface: 

```
admin@ubuntu:~$ sudo ifconfig <interface> 192.168.88.2/24
```

97 

Then run the Netinstall version 6 (an example that resets the configuration upon reinstallation procedure): 

```
admin@ubuntu:~$ sudo ./netinstall -r -a 192.168.88.3 routeros-mipsbe-6.48.1.npk
Using server IP: 192.168.88.2
Starting PXE server
Waiting for RouterBOARD...
PXE client: 01:23:45:67:89:10
Sending image: mips
Discovered RouterBOARD...
Formatting...
Sending package routeros-mipsbe-6.48.1.npk ...
Ready for reboot...
Sent reboot command
```

Or run the Netinstall version 7 (an example that applies an empty configuration and discards the branding during the reinstallation procedure): 

```
admin@ubuntu:~$ sudo ./netinstall-cli -e -b -i enx1234567ee890 -a 192.168.88.3 routeros-7.14.2-arm.npk wireless-
7.14.2-arm.npk
Version: 7.15beta9(2024-03-27 20:41:15)
Will apply empty config
Will remove branding
Using Interface: enx1234567ee890
Wait for Link-UP on 'enx1234567ee890'. OK
Using Client IP: 192.168.88.3
Using Server IP: 192.168.88.10
Starting PXE server
Waiting for RouterBOARD...
client: 74:4D:28:8E:86:74
Detected client architecture: arm
Sending and starting Netinstall boot image ...
Installed branding package detected
Discovered RouterBOARD... 74:4D:28:8E:86:74
Formatting...
Sending package routeros-7.14.2-arm.npk ...
Sending package wireless-7.14.2-arm.npk ...
Sending empty config ...
Ready for reboot...
Sent reboot command
```
