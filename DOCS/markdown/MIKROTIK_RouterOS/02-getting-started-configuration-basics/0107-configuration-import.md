## Configuration Import 

Root menu command import allows running configuration script from the specified file. Script file (with extension ".rsc") can contain any console command including complex scripts. 

For example, load saved configuration file 

```
[admin@MikroTik] > import address.rsc
Opening script file address.rsc
Script file loaded and executed successfully
[admin@MikroTik] >
```

Import command allows to specify the following parameters: 

**==> picture [516 x 174] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>from-line Start executing the script from the specified line number. This option is only available in verbose mode.<br>file-name Name of the script (.rsc) file to be executed.<br>verbose Reads each line from the file and executes individually, allowing to debug syntax or other errors more easily.<br>dry-run Simulates the import without making any configuration changes. This helps in catching syntax errors. This option is only available in<br>verbose mode.<br>If the device has a default or existing configuration that requires replacement, it is necessary to initiate a configuration reset.<br>This involves applying a clean, empty configuration using the command /system/reset-configuration no-defaults=yes, followed by a device<br>reboot.<br>**----- End of picture text -----**<br>


60
