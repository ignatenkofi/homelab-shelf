## Uploading and importing certificates 

Before we proceed with the setup, you need to download Amazon Root CA and upload it, together with the gateway certificate file and its key, into the RouerOS file list menu: 

1610 

**==> picture [376 x 248] intentionally omitted <==**

After the files were uploaded, import the certificates, one by one (under System>Certificates ): 

**==> picture [376 x 258] intentionally omitted <==**

Make sure to upload the gateway certificate first and then its key (so that the gateway certificate has both K-key and T-trusted flags present). In the end, you should have all 3 file imported, like so: 

1611 

**==> picture [376 x 124] intentionally omitted <==**
