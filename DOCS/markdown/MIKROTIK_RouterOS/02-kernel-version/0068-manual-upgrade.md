## Manual upgrade 

You can upgrade RouterOS in the following ways: 

WinBox – drag and drop files to the Files menu WebFig - upload files from the Files menu 

FTP - upload files to the root directory 

**==> picture [13 x 13] intentionally omitted <==**

It is strongly recommended to upgrade the bootloader after upgrading RouterOS. To upgrade the bootloader, execute command "/system routerboard upgrade" in CLI, followed by a reboot. Alternatively, navigate to the GUI System → RouterBOARD menu and click the "Upgrade" button, then reboot the device. 

**==> picture [13 x 13] intentionally omitted <==**

RouterOS cannot be upgraded through a serial cable. Only RouterBOOT is upgradeable using this method.
