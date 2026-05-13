## Protected bootloader 

The feature allows the protection of RouterOS configuration and files from a physical attacker by disabling etherboot. It is called "Protected RouterBOOT". This feature can be enabled and disabled only from within RouterOS after login, i.e., there is no RouterBOOT setting to enable/disable this feature. These extra options appear only under certain conditions. When this setting is enabled - both the reset button and the reset pin-hole are disabled. RouterBOOT menu is also disabled. The only ability to change boot mode or enable the RouterBOOT settings menu is through RouterOS. If you do not know the RouterOS password - your device can not be recovered! 

**==> picture [13 x 13] intentionally omitted <==**

Starting from the v7 version, when enabling or making any changes to the protected-routerboard feature the reset or mode button must be pressed for confirmation. 

For example, when setting protected-routeboard enabled, you will be given 60 seconds to confirm by pressing the reset button, otherwise, this setting won't be enabled. 

```
[admin@450] > system/routerboard/settings/set protected-routerboot=enabled
[admin@450] > system/routerboard/settings/print
                        ;;; press button within 60 seconds to confirm
                            protected routerboot enable
              auto-upgrade: no
                 baud-rate: 115200
                boot-delay: 2s
            enter-setup-on: any-key
               boot-device: nand-if-fail-then-ethernet
             cpu-frequency: auto
             boot-protocol: bootp
       enable-jumper-reset: yes
       force-backup-booter: no
               silent-boot: yes
      protected-routerboot: enabled
      reformat-hold-button: 20s
  reformat-hold-button-max: 10m
```

Property Description protectedThis setting disables any access to the RouterBOOT configuration settings over a console cable and disables the operation of the routerboot (e reset button to change the boot mode ( Netinstall will be disabled ). Access to RouterOS will only be possible with a known RouterOS nabled | admin password. Unsetting of this option is only possible from RouterOS. If you forget the RouterOS password, the only option is to disabled; perform a complete reformat of both NAND and RAM with the following method, but you have to know the reset button hold time in Default: disa seconds. bled ) enabled - secure mode, only RouterOS can be accessed with a RouterOS admin password. Any user input from the serial port is ignored. Etherboot is not available, RouterBOOT setting change is not possible. 

disabled - regular operation, RouterBOOT settings available with serial console and reset button can be used to launch Netinstall 

1748 

reformatAs an emergency recovery option, it is possible to reset everything by pressing the button at power-on for longer than reformat-holdhold-button ( button time, but less than reformat-hold-button-max (new in RouterBOOT 3.38.3). 5s .. 300s; When you use the button for a complete reset, the following actions are taken: Default: 20s ) **`EXTREMELY DANGEROUS`** `. Use this only if you have lost all access to the device.` 1.  RouterOS, all of its files and configuration is completely and irreversibly erased by nand re-format; 2.  All RouterBOOT settings are reset to defaults; 3.  Board is rebooted; 4.  As boot from NAND fails, it goes to etherboot automatically; 5.  Netinstall is required to reinstall RouterOS. 

Please note! Reformat on some RouterBOARDS can take more than 5 minutes. After formatting the board will be ready for Netinstall. reformatIncrease the security even further by setting the max hold time, this means that you must release the reset button within a specified hold-buttontime interval. If you set the "reformat-hold-button" to 60s and "reformat-hold-button-max" to 65s, it will mean that you must hold the max (15s .. button 60 to 65 seconds, not less and not more, making guesses impossible. Introduced in RouterBOOT 3.38.3 600s; Default: 10m ) 

**==> picture [13 x 13] intentionally omitted <==**

RouterBOARD that has the protected RouterBOOT setting enabled will blink the LED every second, to make counting easier. The LED will turn off for one second, and turn on for the next second.
