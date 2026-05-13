## Configuration Reset 

RouterOS allows resetting configuration with `/system reset-configuration` command 

This command clears all configuration of the router and sets it to the factory defaults including the login name and password ('admin' with an empty password or, for some models, check user and wireless passwords on the sticker). For more details on the default configuration see the list. 

After executing the configuration reset command, the router will reboot and load the default configuration. Starting from version 7.13, following the reset, a license prompt will be displayed with the option to view the end-user license agreement. 

**==> picture [13 x 13] intentionally omitted <==**

The backup file of the existing configuration is stored before reset. That way you can easily restore any previous configuration if the reset is done by mistake. 

**==> picture [13 x 13] intentionally omitted <==**

If the router was installed using Netinstall and had a script specified as the initial configuration, the reset command executes this script after purging the configuration. To stop it from doing so, you will have to reinstall the router. 

It is possible to override the default reset behavior with the parameters below: 

**==> picture [516 x 212] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>keep- Do not remove existing users from the configuration<br>users<br>no- Do not load the default configuration, just clear the configuration<br>defaults<br>skip- Skip automatic backup file generation before reset<br>backup<br>run-after- Run specified .rsc file after reset. That way you can load your custom configuration.<br>reset<br>If a specific .rsc file execution takes more than 2 minutes, a script will fail, and LOG will contain  "runtime limit exceeded" or in<br>rare cases "std failure: timeout" error.<br>caps- Run caps-mode script after configuration reset.<br>mode<br>**----- End of picture text -----**<br>


For example hard reset configuration without loading default config and skipping backup file: 

```
[admin@MikroTik] > /system reset-configuration no-defaults=yes skip-backup=yes
Dangerous! Reset anyway? [y/N]: y
```

And the same using Winbox: 

62 

**==> picture [369 x 145] intentionally omitted <==**

63
