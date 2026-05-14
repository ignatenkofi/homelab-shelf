## Netinstall 

NetInstall is a widely-used installation tool for RouterOS. It runs on Windows systems or via a command-line tool, netinstall-cli, on Linux, or through Wine (with superuser permissions required). 

The NetInstall utilities can be downloaded from the MikroTik download section 

. 

NetInstall is also used to re-install RouterOS in cases where a previous installation has failed, been damaged, or where access passwords have been lost. 

To use NetInstall, your device must support booting from Ethernet, with a direct Ethernet connection between the NetInstall computer and the target device. All RouterBOARDs support PXE network booting, which can be enabled in the RouterOS "routerboard" menu (if RouterOS is accessible) or in the bootloader settings using a serial console cable. 

Note: For RouterBOARD devices without a serial port or RouterOS access, you can activate PXE booting using the Reset button. 

48 

NetInstall can also directly install RouterOS onto a disk (USB/CF/IDE/SATA) connected to the NetInstall Windows machine. Once installed, simply transfer the disk to the Router machine and boot from it. 

Attention! Do not try to install RouterOS on your system drive. Action will format your hard drive and wipe out your existing OS.
