## Support on older MikroTik hardware 

This section only applies to older devices that display a particular error message! Do not change the bootloader without seeing a message instructing you to do it. 

The protected RouterBOOT feature is supported by all modern MikroTik devices, but if you have and old device, if your factory-firmware version is lower than 7.19.3 and your device displays the message → The "protected routerboot" feature requires a backup-routerboot upgrade ← when trying to enable the feature, do the following: 

- upgrade or downgrade the device specifically to the RouterOS 7.19.3 release (from our download page or archive); 

upgrade your current RouterBOOT version with "/system routerboard upgrade" then reboot the device, so that the RouterBOOT version ( currentfirmware version when checking "/system routerboard print") is the same as the firmware version ("/system resource print") installed, which should be 7.19.3 ; 

upload the the v7 universal package for all architectures to the device and reboot the device again. This will make your factory-firmware version 7. 19.3 , where you are allowed to enable the feature. After this step, you can upgrade the device to a newer release. 

If your RouterOS version is v6 and you get the same prompt, follow the same steps mentioned above, but only update/downgrade/compare your device version to specifically 6.49.7 instead and use v6 universal package for all architectures.
