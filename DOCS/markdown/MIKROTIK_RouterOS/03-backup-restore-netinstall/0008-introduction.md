## Introduction 

Netinstall is a tool for installing and reinstalling MikroTik devices running RouterOS. Always try using Netinstall if you suspect that your device is not working properly. The tool is available for Windows (with a graphical interface) and for Linux (as a command line tool). 

In short, the Netinstall procedure goes like this: Connect your PC directly to the boot port (Usually Ether1, the port labeled BOOT or as otherwise indicated in the product manual) of the device you will be reinstalling. Turn on the device while holding the reset button until it shows up in the Netinstall tool. 

**==> picture [13 x 13] intentionally omitted <==**

Careful. Netinstall re-formats the system's drive, all configuration and saved files will be lost. Netinstall does not erase the RouterOS license key, nor does it reset RouterBOOT related settings, for example, CPU frequency is not changed after reinstalling the device.
