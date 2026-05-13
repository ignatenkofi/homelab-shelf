## Windows client configuration 

Open PKCS12 format certificate file on the Windows computer. Install the certificate by following the instructions. Make sure you select the Local Machine store location. 

**==> picture [504 x 97] intentionally omitted <==**

You can now proceed to Network and Internet settings -> VPN and add a new configuration. Fill in the Connection name, Server name, or address parameters. Select IKEv2 under VPN type. When it is done, it is necessary to select "Use machine certificates". This can be done in Network and Sharing Center by clicking the Properties menu for the VPN connection. The setting is located under the Security tab. 

1217 

**==> picture [504 x 146] intentionally omitted <==**

Currently, Windows 10 is compatible with the following Phase 1 ( profiles) and Phase 2 ( proposals) proposal sets: 

**==> picture [226 x 272] intentionally omitted <==**

**----- Start of picture text -----**<br>
Phase 1<br>Hash Algorithm Encryption Algorithm DH Group<br>SHA1 3DES modp1024<br>SHA256 3DES modp1024<br>SHA1 AES-128-CBC modp1024<br>SHA256 AES-128-CBC modp1024<br>SHA1 AES-192-CBC modp1024<br>SHA256 AES-192-CBC modp1024<br>SHA1 AES-256-CBC modp1024<br>SHA256 AES-256-CBC modp1024<br>SHA1 AES-128-GCM modp1024<br>SHA256 AES-128-GCM modp1024<br>SHA1 AES-256-GCM modp1024<br>SHA256 AES-256-GCM modp1024<br>**----- End of picture text -----**<br>


**==> picture [307 x 140] intentionally omitted <==**

**----- Start of picture text -----**<br>
Phase 2<br>Hash Algorithm Encryption Algorithm PFS Group<br>SHA1 AES-256-CBC none<br>SHA1 AES-128-CBC none<br>SHA1 3DES none<br>SHA1 DES none<br>SHA1 none none<br>**----- End of picture text -----**<br>
