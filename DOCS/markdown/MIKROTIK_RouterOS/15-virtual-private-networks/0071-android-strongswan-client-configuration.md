## Android (strongSwan) client configuration 

Currently, there is no IKEv2 native support in Android, however, it is possible to use strongSwan from Google Play Store which brings IKEv2 to Android. StrongSwan accepts PKCS12 format certificates, so before setting up the VPN connection in strongSwan, make sure you download the PKCS12 bundle to your Android device. When it is done, create a new VPN profile in strongSwan, type in the server IP, and choose "IKEv2 Certificate" as VPN Type. When selecting a User certificate, press Install and follow the certificate extract procedure by specifying the PKCS12 bundle. Save the profile and test the connection by pressing on the VPN profile. 

**==> picture [504 x 129] intentionally omitted <==**

It is possible to specify custom encryption settings in strongSwan by ticking the "Show advanced settings" checkbox. Currently, strongSwan by default is compatible with the following Phase 1 ( profiles) and Phase 2 ( proposals) proposal sets: 

**==> picture [227 x 215] intentionally omitted <==**

**----- Start of picture text -----**<br>
Phase 1<br>Hash Algorithm Encryption Algorithm DH Group<br>SHA* AES-*-CBC modp2048<br>SHA* AES-*-CBC ecp256<br>SHA* AES-*-CBC ecp384<br>SHA* AES-*-CBC ecp521<br>SHA* AES-*-CBC modp3072<br>SHA* AES-*-CBC modp4096<br>SHA* AES-*-CBC modp6144<br>SHA* AES-*-CBC modp8192<br>SHA* AES-*-GCM modp2048<br>**----- End of picture text -----**<br>

1222 

**==> picture [227 x 133] intentionally omitted <==**

**----- Start of picture text -----**<br>
SHA* AES-*-GCM ecp256<br>SHA* AES-*-GCM ecp384<br>SHA* AES-*-GCM ecp521<br>SHA* AES-*-GCM modp3072<br>SHA* AES-*-GCM modp4096<br>SHA* AES-*-GCM modp6144<br>SHA* AES-*-GCM modp8192<br>**----- End of picture text -----**<br>

**==> picture [244 x 252] intentionally omitted <==**

**----- Start of picture text -----**<br>
Phase 2<br>Hash Algorithm Encryption Algorithm PFS Group<br>none AES-256-GCM none<br>none AES-128-GCM none<br>SHA256 AES-256-CBC none<br>SHA512 AES-256-CBC none<br>SHA1 AES-256-CBC none<br>SHA256 AES-192-CBC none<br>SHA512 AES-192-CBC none<br>SHA1 AES-192-CBC none<br>SHA256 AES-128-CBC none<br>SHA512 AES-128-CBC none<br>SHA1 AES-128-CBC none<br>**----- End of picture text -----**<br>
