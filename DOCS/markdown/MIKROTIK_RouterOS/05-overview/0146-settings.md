## Settings 

/certificate settings allows configuring Certificate Revocation List (CRL) settings. 

By default, CRL is not utilized, and certificates are not verified for revocation status. 

**==> picture [516 x 166] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>builtin-trust-anchors  (trusted not-trusted|  Allows to trust built-in root certificate authorities<br>Default: see description)<br>Default builtin-trust-anchors after upgrade from older RouterOS version: not-trusted<br>Default builtin-trust-anchors after configuration reset: trusted<br>crl-download  (yes | no Default: no) Whether to automatically download/update CRL<br>crl-store  (ram | sytem Default: ram) Where to store downloaded CRL information<br>CRL will be automatically renewed every hour for certificates which have "trusted=yes" using http<br>protocol (ldap and ftp is currently unsupported)<br>crl-use  (yes | no Default: no) Whether to use CRL<br>**----- End of picture text -----**<br>


281 

**==> picture [13 x 13] intentionally omitted <==**

If /certificate/settings/set crl-use is set to yes, RouterOS will check CRL for each certificate in a certificate chain, therefore, an entire certificate chain should be installed into a device - starting from Root CA, intermediate CA (if there are such), and certificate that is used for specific service. 

An example on importing a root certificate.
