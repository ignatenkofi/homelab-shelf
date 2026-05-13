## Import Certificate 

To import certificates, certificates must be uploaded to a device using one of the file upload methods. 

Certificates must be imported as a file. 

Supported are PEM, DER, CRT, PKCS12 formats. 

**==> picture [359 x 99] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name  (string Default: file-name_number) A certificate name that will be shown in the certificate manager<br>file-name  (string) A file name that will be imported<br>passphrase  (string Default: none) File passphrase if there is such<br>trusted  (yes | no Default: yes) Adds trusted flag for imported certificate<br>**----- End of picture text -----**<br>


```
[admin@MikroTik] > /certificate/import file-name=certificate_file_name name=name_example
passphrase=file_passphrase
     certificates-imported: 2
     private-keys-imported: 1
            files-imported: 1
       decryption-failures: 0
  keys-with-no-certificate: 0
[admin@MikroTik] > /certificate/print
Flags: K - PRIVATE-KEY; T - TRUSTED
Columns: NAME, COMMON-NAME
#    NAME            COMMON-NAME
0 KT name_example    cert
1  T name_example_1  ca
```
