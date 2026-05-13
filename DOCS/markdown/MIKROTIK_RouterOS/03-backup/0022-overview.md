## Overview 

MikroTik hardware routers that run RouterOS come preinstalled with a RouterOS license, if you have purchased a RouterOS based device, nothing must be done regarding the license. 

For X86 systems (i.e. PC devices), you need to obtain a license key. Each x86 system has a unique identifier called Software ID , which is used for licensing. 

The license key is a block of symbols that needs to be copied from your mikrotik.com account, or from the email you received in, and then it can be pasted into the router. You can paste the key anywhere in the terminal, or by clicking "Paste key" in WinBox License menu. A reboot is required for the key to take effect. 

**==> picture [13 x 13] intentionally omitted <==**

RouterOS licensing scheme is based on Software ID / System ID where: 

RouterBOARD Software ID is bound to storage media (HDD, NAND). x86 Software ID is bound to MBR CHR System ID is bound to MBR and UUID 

Before the license purchase it is recommended to check if the Software ID does not change on reboot. (Software ID may change on defective HDD, on HDD where RAID controllers are used but not properly configured etc.) 

Licensing information can be read from CLI system console: 

```
[admin@RB1100] > /system license print
    software-id: "43NU-NLT9"
         nlevel: 6
       features:
[admin@RB1100] >
```

or from equivalent WinBox,  WebFig menu. 

104
