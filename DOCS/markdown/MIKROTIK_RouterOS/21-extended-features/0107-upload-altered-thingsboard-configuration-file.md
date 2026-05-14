## Upload altered ThingsBoard configuration file 

All that is left is to overwrite the current configuration file with an altered file and upload both certificates. 

Once again, make sure your terminal is pointing to the right folder (where 3 files are located → both certificates and an altered "thingsboard.yml" file), and, from there, SFTP into the container's configuration file directory: 

```
c:\Users\Admin\Desktop\ThingsBoard>dir
 Directory of c:\Users\Admin\Desktop\ThingsBoard
```

```
30.01.2023  10:59    <DIR>          .
30.01.2023  10:59    <DIR>          ..
27.01.2023  15:09             2 448 keystore.p12
27.01.2023  15:36             2 434 mqttserver.p12
30.01.2023  10:59            68 846 thingsboard.yml
               3 File(s)         73 728 bytes
               2 Dir(s)  50 901 626 880 bytes free
c:\Users\Admin\Desktop\ThingsBoard>sftp admin@192.168.88.1
admin@192.168.88.1's password:
Connected to 192.168.88.1.
sftp> cd ThingsBoard\usr\share\thingsboard\conf
sftp> dir
banner.txt          i18n                logback.xml         templates           thingsboard.conf    thingsboard.
yml
```

Upload these files with the help of `put` command: 

1893 

```
sftp> put thingsboard.yml
Uploading thingsboard.yml to /ThingsBoard/usr/share/thingsboard/conf/thingsboard.yml
thingsboard.yml                                                                       100%   67KB   2.2MB/s
00:00
sftp> put keystore.p12
Uploading keystore.p12 to /ThingsBoard/usr/share/thingsboard/conf/keystore.p12
keystore.p12                                                                          100% 2448     1.2MB/s
00:00
sftp> put mqttserver.p12
Uploading mqttserver.p12 to /ThingsBoard/usr/share/thingsboard/conf/mqttserver.p12
mqttserver.p12                                                                        100% 2434   608.5KB/s
00:00
sftp> dir
banner.txt          i18n                keystore.p12        logback.xml         mqttserver.p12
templates
thingsboard.conf    thingsboard.yml
```

Restart the container: 

```
[admin@MikroTik] > /container/stop 0
[admin@MikroTik] > /container/start 0
```

Make sure to wait for the container to stop ( `status=stopped` should be shown after using `/container/print` command) before initiating it again.
