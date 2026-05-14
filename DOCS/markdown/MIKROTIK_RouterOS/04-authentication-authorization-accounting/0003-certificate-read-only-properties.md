## Certificate read-only properties 

After a certificate is signed, most of a certificate template properties are converted to read-only (except name and trusted) 

**==> picture [356 x 212] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>serial-number Certificate serial number<br>fingerprint Certificate fingerprint<br>akid Certificate authority ID<br>skid Certificate subject ID<br>issuer Certificate Authority<br>invalid-before Date and time before which a certificate expired<br>invalid-after Date and time after which a certificate expired<br>expires-after  Time left before expiration<br>key-type  (RSA: | EC ) Private key ype<br>ca CA certificate name (shown only for certificates that are signed in specific device)<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

If the CA certificate is removed, all issued certificates in the chain are also removed.
