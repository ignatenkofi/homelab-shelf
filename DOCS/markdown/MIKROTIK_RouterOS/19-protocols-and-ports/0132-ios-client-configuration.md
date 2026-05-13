## iOS client configuration 

Typically PKCS12 bundle contains also a CA certificate, but iOS does not install this CA, so a self-signed CA certificate must be installed separately using PEM format. Open these files on the iOS device and install both certificates by following the instructions. It is necessary to mark the self-signed CA certificate as trusted on the iOS device. This can be done in Settings -> General -> About -> Certificate Trust Settings menu. When it is done, check whether both certificates are marked as "verified" under the Settings -> General -> Profiles menu. 

**==> picture [504 x 274] intentionally omitted <==**

You can now proceed to Settings -> General -> VPN menu and add a new configuration. Remote ID must be set equal to common-name or subjAltName of server's certificate. Local ID can be left blank. 

1220 

**==> picture [504 x 546] intentionally omitted <==**

Currently, iOS is compatible with the following Phase 1 ( profiles) and Phase 2 ( proposals) proposal sets: 

**==> picture [218 x 101] intentionally omitted <==**

**----- Start of picture text -----**<br>
Phase 1<br>Hash Algorithm Encryption Algorithm DH Group<br>SHA256 AES-256-CBC modp2048<br>SHA256 AES-256-CBC ecp256<br>SHA256 AES-256-CBC modp1536<br>**----- End of picture text -----**<br>


1221 

**==> picture [218 x 39] intentionally omitted <==**

**----- Start of picture text -----**<br>
SHA1 AES-128-CBC modp1024<br>SHA1 3DES modp1024<br>**----- End of picture text -----**<br>


**==> picture [234 x 101] intentionally omitted <==**

**----- Start of picture text -----**<br>
Phase 2<br>Hash Algorithm Encryption Algorithm PFS Group<br>SHA256 AES-256-CBC none<br>SHA1 AES-128-CBC none<br>SHA1 3DES none<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

If you are connected to the VPN over WiFi, the iOS device can go into sleep mode and disconnect from the network.
