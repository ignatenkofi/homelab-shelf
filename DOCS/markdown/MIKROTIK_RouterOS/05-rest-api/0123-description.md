## Description 

FlashFig is an application for mass router configuration. It can be used by MikroTik distributors, ISPs, or any other companies who need to apply RouterOS configuration to many routers in the shortest possible time. 

FlashFig applies MikroTik RouterOS configuration to any RouterBOARD within 3 seconds . You can perform FlashFig on a batch of routers, the only thing you need is to connect RouterBOARD to a Layer 2 network running FlashFig and to power a FlashFig-enabled RouterBOARD up. 

FlashFig only runs on a Windows computer and is available from the downloads page. 

All RouterBOARDs support FlashFig mode. It works between a Windows computer running FlashFig and a RouterBOARD in the same broadcast domain (direct Layer 2 Ethernet network connection is required). 

FlashFig support is enabled on every new RouterBOARD manufactured since March 2010 by default from the factory. For older models, FlashFig can be enabled via RouterBOOT or from MikroTik RouterOS console - /system routerboard settings set boot-device=flash-boot-once-then-nand or /system 

routerboard settings set boot-device=flash-boot 

. 

**==> picture [13 x 13] intentionally omitted <==**

Starting from RouterOS/RouterBOOT v7.16 , flash boot mode will be enabled in the same way as from the factory, after every system reset initiated from the software. The same mode will be initiated when you reset router with the reset button, (bootloader version  v7.16 or higher is required). 

Please note that if you press and hold reset button before powering on the router, then the backup booter is used. The backup booter firmware (installed in the factory) must also then be v7.16 or higher. 

FlashFig mode on a brand new RouterBOARD is disabled on further boots only after the first successful user login or successful FlashFig attempt to avoid unwanted reconfiguration at a later time. To use FlashFig a second time on the same router, you need to enable flash-boot in Bootloader settings (this setting will revert to NAND after a successful configuration change OR once any user logs into the board). 

If RouterOS reset-configuration command is used later (or configuration reset using the Reset button), FlashFig configuration is loaded. To permanently overwrite, use the Netinstall process and check Apply default configuration or use  flag in Linux-based command line.-r 

You view FlashFig video tutorial on MikroTik YouTube channel.
