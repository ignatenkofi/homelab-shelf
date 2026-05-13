## Testing the connection 

Upload CA certificate ( ca.crt ) into RouterOS, into the device's "File List": 

```
/file print
Columns: NAME, TYPE, SIZE, CREATION-TIME
#  NAME                TYPE             SIZE  CREATION-TIME
0  skins               directory              1970-01-01 03:00:02
1  pub                 directory              2023-01-04 11:05:04
2  disk7               disk                   2023-07-12 09:52:07
3  mosquitto           container store        2023-07-12 09:52:09
4  mosquitto_mounted   container store        2023-07-25 16:38:37
5  pull                directory              2023-07-12 09:52:09
6  ca.crt              .crt file        1322  2023-07-12 11:28:23
```

1880 

Import the certificate: 

```
/certificate/import file-name=ca.crt passphrase=""
```
