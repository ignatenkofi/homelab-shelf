## Create certificates 

Create a certificate for HTTPS: 

```
/certificate add name=TBhttps common-name=172.18.0.2
/certificate sign TBhttps
```

Create a certificate for MQTT: 

```
/certificate add name=TBmqtt common-name=172.18.0.2
```

```
/certificate sign TBmqtt
```

Confirm that they were added with the help of `/certificate/print` command: 

```
[admin@MikroTik] > /certificate/print
Flags: K - PRIVATE-KEY; A - AUTHORITY; T - TRUSTED
Columns: NAME, COMMON-NAME, FINGERPRINT
#     NAME     COMMON-NAME  FINGERPRINT
0 KAT TBhttps  172.18.0.2   863f4547c74ce3ec70c3e82172502711517b52bbc055d18c24ba4aafec46152c
1 KAT TBmqtt   172.18.0.2   ebf3ff5d03ed4cc73546e058da9bc414cdaf24ce45da29b203348045fbbd21ae
```

Export the certificates using PKCS12 format and set up a password/passphrase for them: 

```
/certificate/export-certificate file-name=keystore export-passphrase=thingsboard_cert_password type=pkcs12
numbers=0
```

```
/certificate/export-certificate file-name=mqttserver export-passphrase=thingsboard_mqttcert_password
type=pkcs12 numbers=1
```

Use your own `export-passphrase` and remember them. 

1890 

The output from the command above will create certificate keystore.p12 and mqttserver.p12 files that you can download from the "File List" menu: 

```
[admin@MikroTik] > /file/print
Columns: NAME, TYPE, SIZE, CREATION-TIME
 #  NAME                 TYPE             SIZE       CREATION-TIME
 0  tb/mytb-data         container store             jan/19/2023 13:43:16
 1  container-log.0.txt  .txt file        2240.5KiB  jan/27/2023 15:37:41
 2  skins                directory                   jan/18/2023 15:12:22
 3  tb/mytb-logs         container store             jan/27/2023 12:24:30
 4  pull                 directory                   jan/19/2023 13:41:01
 5  pub                  directory                   jan/18/2023 16:15:29
 6  tb                   directory                   jan/23/2023 15:46:39
 7  tb/data              container store             jan/18/2023 16:50:08
 8  tb/logs              container store             jan/18/2023 16:50:08
 9  mqttserver.p12       .p12 file        2438       jan/27/2023 15:36:26
10  keystore.p12         .p12 file        2448       jan/27/2023 15:08:07
11  ThingsBoard          container store             jan/19/2023 13:40:50
```

Download both files from the router into any directory on your PC. For example, we've downloaded it into `C:\Users\Admin\Desktop\ThingsBoard` folder.
