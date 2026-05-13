## Troubleshooting 

Ensure connection is established to the correct device by checking the device settings like serial number and model name by issuing a command: 

```
[admin@MikroTik] > /system routerboard print
```

If bridge wlan60-1 interface in bridge settings is inactive and configuration is done properly  to enable the interface on a device - issue a command: 

```
[admin@MikroTik] > /interface w60g enable wlan60-1
```

1456
