## RouterBOARD 

FlashFig mode is enabled on every RouterBOARD from the factory by default, which means no configuration is required on RouterBOARD. 

If FlashFig is not enabled on your router, access the RouterBOARD with WinBox/Console and change the boot-device to flash-boot or flash-bootonce-then-nand: 

```
system/routerboard/settings/set boot-device=flash-boot
```

Or use a more preferable option, for a single boot flash-boot: 

```
system/routerboard/settings/set boot-device=flash-boot-once-then-nand
```

Your router is now ready for FlashFig.
