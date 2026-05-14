## Requirements 

The Windows computer must be equipped with the following ports and contain the following files: 

- A working Ethernet port; 

- Valid .rsc file(s) with MikroTik RouterOS configuration similar to an export/import file. In addition to regular configuration commands, it is also possible to re-apply the factory passwords by using the read-only variables $defconfPassword and $defconfWifiPassword (starting from RouterOS 7.10beta8); Always use the latest FlashFig program available from the downloads page; The RouterBOARD has to be in flash-boot mode, if this is the very first boot, nothing needs to be done 

273 

**==> picture [13 x 13] intentionally omitted <==**

Be aware of the text editor's treatment of CR/LF characters and test that the config has no errors when normally applied onto an identical version of RouterOS before applying via FlashFig as run-time errors will not be visible!
