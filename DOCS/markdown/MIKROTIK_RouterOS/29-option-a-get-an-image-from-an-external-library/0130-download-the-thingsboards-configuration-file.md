## Download the ThingsBoard's configuration file 

Open your command terminal ("CMD", as Administrator, for Windows users, or "Linux Shell or Command Terminal" for Linux users) and navigate it to the directory where the certificates are: 

```
C:\Windows\System32>cd c:\Users\Admin\Desktop\ThingsBoard
C:\Users\Admin\Desktop\ThingsBoard>dir
Directory of C:\Users\Admin\Desktop\ThingsBoard
27.01.2023  15:36    <DIR>          .
27.01.2023  15:36    <DIR>          ..
27.01.2023  15:09             2 448 keystore.p12
27.01.2023  15:36             2 434 mqttserver.p12
               2 File(s)          4 882 bytes
               2 Dir(s)  51 380 154 368 bytes free
```

From this directory, you will need to connect to the router's IP via the SFTP (which allows you to file transfer using SSH protocol, so you need to make sure that SSH service is enabled beforehand): 

```
c:\Users\Admin\Desktop\ThingsBoard>sftp admin@192.168.88.1
The authenticity of host '192.168.88.1 (192.168.88.1)' can't be established.
RSA key fingerprint is SHA256:/WmmZErqWL51SOlS4EaGvSQ0i4HPnSIHCEjnc8AmP2c.
Are you sure you want to continue connecting (yes/no/[fingerprint])?yes
admin@192.168.88.1's password:
Connected to 192.168.88.1.
sftp>
```

While the container is running, go to the ThingsBoard configuration file folder (use `dir` or `ls` command to see the content of the folder you are in and `cd` command to go to the folder of our choice). By default, it should be the folder with the " thingsboard.yml " configuration file in it. In our example, we could locate it under: 

```
sftp> cd ThingsBoard\usr\share\thingsboard\conf
```

```
sftp> dir
```

```
banner.txt          i18n                logback.xml         templates           thingsboard.conf    thingsboard.
yml
```

Download the " thingsboard.yml " configuration using `get` command. This will download the default ThingsBoard configuration file to your machine (to the directory from where you initiated SFTP): 

1891 

```
sftp> get thingsboard.yml
Fetching /ThingsBoard/usr/share/thingsboard/conf/thingsboard.yml to thingsboard.yml
/ThingsBoard/usr/share/thingsboard/conf/thingsboard.yml                               100%   67KB   2.0MB/s
00:00
sftp> quit
```

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
```
