## macOS client configuration 

Open the PKCS12 format certificate file on the macOS computer and install the certificate in the "System" keychain. It is necessary to mark the CA certificate as trusted manually since it is self-signed. Locate the certificate macOS Keychain Access app under the System tab and mark it as Always Trust. 

1218 

**==> picture [504 x 216] intentionally omitted <==**

You can now proceed to System Preferences -> Network and add a new configuration by clicking the + button. Select Interface: VPN, VPN Type: IKEv2 and name your connection. Remote ID must be set equal to common-name or subjAltName of server's certificate. Local ID can be left blank. Under Authentication Settings select None and choose the client certificate. You can now test the connectivity. 

**==> picture [504 x 219] intentionally omitted <==**

Currently, macOS is compatible with the following Phase 1 ( profiles) and Phase 2 ( proposals) proposal sets: 

**==> picture [232 x 140] intentionally omitted <==**

**----- Start of picture text -----**<br>
Phase 1<br>Hash Algorithm Encryption Algorithm DH Group<br>SHA256 AES-256-CBC modp2048<br>SHA256 AES-256-CBC ecp256<br>SHA256 AES-256-CBC modp1536<br>SHA1 AES-128-CBC modp1024<br>SHA1 3DES modp1024<br>**----- End of picture text -----**<br>

1219 

**==> picture [232 x 101] intentionally omitted <==**

**----- Start of picture text -----**<br>
Phase 2<br>Hash Algorithm Encryption Algorithm PFS Group<br>SHA256 AES-256-CBC none<br>SHA1 AES-128-CBC none<br>SHA1 3DES none<br>**----- End of picture text -----**<br>
