## Configuration Examples 

The following example shows how to copy the file with filename "conf.rsc" from a device with ip address 192.168.88.2 by FTP protocol and save it as file with filename "123.rsc". User and password are needed to login into the device. 

```
[admin@MikroTik] /tool> fetch address=192.168.88.2 src-path=conf.rsc \
user=admin mode=ftp password=123 dst-path=123.rsc port=21 \
host="" keep-result=yes
```

Example to upload file to another router: 

```
[admin@MikroTik] /tool> fetch address=192.168.88.2 src-path=conf.rsc \
user=admin mode=ftp password=123 dst-path=123.rsc upload=yes
```

Another file download example that demonstrates the usage of url property. 

```
[admin@MikroTik] /> /tool fetch url="https://www.mikrotik.com/img/netaddresses2.pdf" mode=http
  status: finished
```

```
[admin@test_host] /> /file print
 # NAME                     TYPE                  SIZE                 CREATION-TIME
 ...
 5 netaddresses2.pdf        .pdf file             11547                jun/01/2010 11:59:51
```

1140 

It is also possible to transfer files over some specific VRF. You can specify VRF at the end of the URL address part (url="http://192.168.88.2@vrf1/..." - will not work for SFTP), address property combined with address and separated with "@" (address=192.168.88.2@vrf1) or simply as address parameter with "@" symbol before the VRF name as in the example (uses address from URL and combines it with VRF name from address parameter): 

```
[admin@MikroTik] /> /tool/fetch url="sftp://192.168.88.2" address=@test src-path=test.txt user=admin
password="" upload=yes
```

```
  status: finished
```
