## Example 

To save the router's configuration to file test and a password: 

```
[admin@MikroTik] > /system backup save name=test password=<YOUR_PASSWORD>
Configuration backup saved
[admin@MikroTik] > /system backup
```

To see the files stored on the router: 

```
[admin@MikroTik] > /file print
# NAME TYPE SIZE CREATION-TIME
0 test.backup backup 12567 sep/08/2018 21:07:50
[admin@MikroTik] >
```

To load the saved backup file test: 

```
[admin@MikroTik] > /system backup load name=test
password: <YOUR_PASSWORD>
Restore and reboot? [y/N]: y
Restoring system configuration
System configuration restored, rebooting now
```
