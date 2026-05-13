## Import RadSec certificates 

In this step, we will import RadSec certificates you should have downloaded from the Orion (from the Orion portal, in the "Manage" tab, under "RadSec Certificates" > "Download Orion Certificates" > "Generate Client Certificate Bundle"). 

1) Drag and drop certificates into WinBox or use FTP/SFTP to upload them into the router instead. 

Ensure that you have all 3 certificate files in the file system (with the `/file print` command): 

```
[admin@MikroTik] > /file/print
Columns: NAME, TYPE, SIZE, LAST-MODIFIED
# NAME                      TYPE       SIZE      LAST-MODIFIED
0 bw.radsec.cacert.pem      .pem file  716       2025-08-19 15:01:56
1 key.pem                   .pem file  227       2025-08-19 15:01:54
2 cert.pem                  .pem file  895       2025-08-19 15:01:54
```

2) Import certitficate files 1 by 1. 

Start with the RadSec CA certificate: 

```
/certificate import file-name=bw.radsec.cacert.pem passphrase=""
```

Then, import client certificate (witch the AP will use for RadSec connection): 

```
/certificate import file-name=cert.pem passphrase=""
```

Lastly, import client certificate's key: 

1385 

```
/certificate import file-name=key.pem passphrase=""
```

Once certificates are imported, they should look like this (CA RadSec certificate should be trusted, while client/AP certificate should be "Trusted" and "Private-Key" flagged): 

```
[admin@MikroTik] > /certificate/print
Flags: K - PRIVATE-KEY; T - TRUSTED
Columns: NAME, COMMON-NAME, SUBJECT-ALT-NAME, SKID
#    NAME                    COMMON-NAME                                      SUBJECT-ALT-
NAME                                     SKID
```

```
0  T bw.radsec.cacert.pem_0  Buttonwood Radsec
```

```
CA                                                                                  XXYYXXYYXXYYXXYYXXYYXXYYXXYY
XXYYXXYYXXY
```

```
1 KT cert.pem_0              xxxxx.yyyyyyyyyyyyyyyyyyy.orion.area120.com  DNS:xxxxx.yyyyyyyyyyyyyyyyyyy.orion.
area120.com
```
