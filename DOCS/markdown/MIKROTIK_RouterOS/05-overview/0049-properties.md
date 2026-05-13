## Properties 

Sub-menu: `/ip ssh` 

**==> picture [516 x 366] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>always-allow-password-login  (yes | no; Default:  no ) Whether to allow password login at the same time when public key authorization is configured<br>for a user.<br>ciphers  (3des-cbc | aes-cbc | aes-ctr | aes-gcm | auto |  Allow to configure SSH ciphers.<br>null; Default:  auto )<br>forwarding-enabled  (both | local | no | remote; Default:  no Allows to control which SSH forwarding method to allow:<br>)<br>no - SSH forwarding is disabled;<br>local - Allow SSH clients to originate connections from the server(router), this setting<br>controls also dynamic forwarding;<br>remote - Allow SSH clients to listen on the server(router) and forward incoming<br>connections;<br>both - Allow both local and remote forwarding methods.<br>host-key-size  (1024 | 1536 | 2048 | 4096 | 8192;  RSA key size when host key is being regenerated.<br>Default:  2048 )<br>host-key-type  (ed25519 | rsa; Default:  rsa ) Select host key type<br>strong-crypto  (yes | no; Default:  no ) Use stronger encryption, HMAC algorithms, use bigger DH primes and disallow weaker ones:<br>use 256 and 192 bit encryption instead of 128 bits;<br>disable null encryption;<br>use sha256 for hashing instead of sha1;<br>disable md5;<br>use 2048bit prime for Diffie-Hellman exchange instead of 1024bit.<br>Commands<br>Property Description<br>**----- End of picture text -----**<br>


243 

**==> picture [516 x 222] intentionally omitted <==**

**----- Start of picture text -----**<br>
export-host-key  (key-file- Export public and private RSA/Ed25519 to files. Command takes two parameters:<br>prefix)<br>key-file-prefix  - used prefix for generated files, for example, prefix 'my' will generate files 'my_rsa', 'my_rsa.pub' etc.<br>passphrase  - private key passphrase<br>Host keys are exported in PKCS#8 format.<br>import-host-key  (private- Import and replace private RSA/Ed25519 key from specified file. Command takes two parameters:<br>key-file)<br>private-key-file  - name of the private RSA/Ed25519 key file<br>passphrase  - private key passphrase<br>Private key is supported in PEM or PKCS#8 format.<br>regenerate-host-key  () Generated new and replace current set of private keys (RSA/Ed25519) on the router. Be aware that previously imported<br>keys might stop working.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Exporting the SSH host key requires "sensitive" user policy.
