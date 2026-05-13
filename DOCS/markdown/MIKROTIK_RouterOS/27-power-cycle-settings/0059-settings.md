## Settings 

Sub-menu level: `/system routerboard settings` 

```
[admin@MikroTik] /system/routerboard/settings> print
              auto-upgrade: no
                 baud-rate: 115200
                boot-delay: 2s
            enter-setup-on: any-key
               boot-device: nand-if-fail-then-ethernet
         preboot-etherboot: disabled
             cpu-frequency: 1200MHz
          memory-frequency: 1066DDR
             boot-protocol: bootp
       enable-jumper-reset: yes
       force-backup-booter: no
               silent-boot: yes
      protected-routerboot: disabled
      reformat-hold-button: 20s
  reformat-hold-button-max: 10m
```

**==> picture [13 x 13] intentionally omitted <==**

Starting from RouterOS version 7.17 device-mode restricts SwOS/RouterOS transition for dual-boot; in order to enable: system/device-mode /update routerboard=yes 

**==> picture [506 x 111] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>auto-upgrade  (yes | no;  Whether to upgrade firmware automatically after RouterOS upgrade. The latest firmware will be applied after an additional<br>Default: no ) reboot<br>baud-rate  (integer;  Choose the onboard RS232 speed in bits per second if installed.  Off  option allows serial interface to be disabled.<br>Default: 115200 )<br>boot-delay  (time;  How much time does to wait for a keystroke while booting<br>Default: 2 s )<br>**----- End of picture text -----**<br>


1745 

**==> picture [506 x 658] intentionally omitted <==**

**----- Start of picture text -----**<br>
boot-device  (nand-if- Choose the way RouterBOOT loads the operating system:<br>fail-then-ethernet ...;<br>Default:  nand-if-fail- ethernet - boot the device in  Etherboot  mode;<br>then-ethernet ) flash-boot - Flashfig mode on startup is enabled. This setting will revert to NAND after a successful configuration<br>change OR once any user logs into the board.<br>flash-boot-once-then-nand - Flashfig mode on startup is enabled for a single boot only, resets to nand-if-fail-then-<br>ethernet after that.<br>nand-if-fail-then-ethernet - boot RouterOS from the NAND, if RouterOS is not booting - it goes to Etherboot<br>automatically. This is the default mode for devices straight out of the box;<br>nand-only - boot RouterOS from the NAND;<br>try-ethernet-once-then-nand - boot device in Etherboot mode once and if no server is available - it will boot directly<br>from the NAND or of the storage type the device is using.<br>Note<br>Etherboot mode is a special state for a MikroTik device that allows you to reinstall your device using Netinstall.<br>There are several ways to put your device into Etherboot mode depending on the device you are using:<br>1. Press the Reset button and power on your device (wait until "USR" led is blinking then stable "On" and when<br>the "USR" led is "Off" - release the Reset button) - the device is booting in  bootp  mode to reinstall RouterOS<br>using Netinstall.<br>2. Using the serial console, when the device is booting up, keep pressing  CTRL+E  on your keyboard until the<br>device shows that it is  trying bootp protocol<br>3. Using the serial console, press any key while the device is booting and choose "o" then "1" and "x"<br>boot-os  (router-os  Changes the booting operating system for CRS3xx series switches<br>|swos; Default: router-<br>os )<br>boot-protocol  (bootp  Boot protocol to use:<br>|dhcp ...; Default: bootp )<br>bootp - the default option for booting RouterOS<br>dhcp - used for OpenWRT and possibly other OS<br>cpu-frequency  (depend This option allows for changing the CPU frequency of the device. Values depend on the model, to see available options,<br>s on model; Default: de hit the [?] button in RouterOS version 6 or the [F1] button in RouterOS version 7 on the keyboard at this prompt<br>pends on model )<br>cpu-mode  (power-save  Whether to enter CPU suspend mode in HTL instruction. Most OSs use HLT instruction during the CPU idle cycle. When<br>| regular; Default: power the CPU is in suspend mode, it consumes less power, but in low-temperature conditions, it is recommended to choose a<br>-save ) regular mode, so that the overall system temperature would be higher<br>enable-jumper-reset  (ye Disable this to avoid accidental setting reset via the onboard jumper<br>s | no; Default: yes )<br>enter-setup-on  (any- Which key will cause the BIOS to enter configuration mode during boot delay. Useful when the serial console prints out<br>key | delete-key;  symbols during the boot process and goes into RouterBOOT menu by itself. Note that in some serial terminal programs, it<br>Default: delete-key ) is impossible to use the Delete key to enter the setup - in this case, it might be possible to do this with the Backspace key<br>force-backup-booter  (ye If to use the backup RouterBOOT. This is only useful if the main loader has become corrupted somehow and cannot be<br>s | no; Default: no ) fixed. So that you don't have to boot the device with a pushed reset button (which loads the backup loader), you can use<br>this setting to load it every time<br>yes - backup loader will be used always<br>no - main booter will be used<br>init-delay  (timeout  Used for mPCIe modems with RB9xx series devices only<br>interval 0s..9s; Default: )<br>In case your modem is not being recognized after a soft reboot, then you might need to add a delay before the USB port is<br>initialized<br>**----- End of picture text -----**<br>


1746 

**==> picture [506 x 358] intentionally omitted <==**

**----- Start of picture text -----**<br>
memory-frequency  (dep This option allows changing the memory frequency of the device. Values depend on the model, to see available options,<br>ends on model; Default: hit the [?] button in RouterOS version 6 or the [F1] button in RouterOS version 7 button on the keyboard at this prompt<br>depends on model )<br>memory-data-rate  (dep This option allows changing the memory data rate of the device. Values depend on the model, to see available options, hit<br>ends on the model;  the [?] button in RouterOS version 6 or the [F1] button in RouterOS version 7 button on the keyboard at this prompt<br>Default:  depends on<br>model )<br>preboot-etherboot  (time Enables  preboot etherboot , which runs before the regular boot device. It works the same as  boot-device=etherboot , but<br>out interval 1s..30s;  has an additional timeout value. If an IP address is not received from the Netinstall server before the timeout expires, the<br>Default: disabled ) regular booting process will start.<br>Note<br>The preboot-etherboot configuration is stored in the BIOS, downgrading RouterOS to older versions will not<br>disable it. This feature can be disabled from the RouterOS menu or by resetting the BIOS.<br>Since etherboot accepts IP addresses from any BOOTP/DHCP server, use preboot-etherboot-server to start<br>etherboot only when address is received from specified Netinstall server.<br>preboot-etherboot- Sets  preboot-etherboot  to accept IP address only from the specified Netinstall server IP address. By enabling this feature,<br>server  (IP address, any: unintentional etherboot from other BOOTP/DHCP servers can be prevented.<br>Default:  any )<br>regulatory-domain-ce  (y Enables extra-low TX power for high antenna gain devices (requires a reboot)<br>es | no; Default: no )<br>silent-boot  (yes | no;  This option disables beeping sounds during booting<br>Default: no )<br>yes - no booting beeps (does not disable the RouterOS: beep command)<br>no - regular booting sound<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

If the CPU or memory is overclocked and that is the reason why the router is not performing as suspected, then this is not considered a warranty case and you should return both frequencies to a nominal value.
