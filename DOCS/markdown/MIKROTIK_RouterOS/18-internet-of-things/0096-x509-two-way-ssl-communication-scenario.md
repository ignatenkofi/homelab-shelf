## X.509 (two-way SSL communication) scenario 

**==> picture [13 x 13] intentionally omitted <==**

This type of authentication requires you to use a server certificate and a client certificate for SSL communication. A server certificate must be generated and uploaded to the ThingsBoard instance. 

To generate a server certificate, use this guide as a reference → generate the certificate (for example, using OPENSSL tool), install/upload it into the correct folder, and enable MQTT SSL in the ThingsBoard configuration file. 

To generate a client certificate, use this guide as a reference. 

You can change the credentials type in the " Device Credentials " section for the specific device: 

1654 

**==> picture [505 x 188] intentionally omitted <==**

X.509 scenario uses a client certificate for authentication. 

Once the certificate is generated (for example, using OPEN SSL), copy the RSA public key into the field and click on the "Save" button.
