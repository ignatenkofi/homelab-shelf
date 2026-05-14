## LNS scenario RouterOS settings 

Make sure that the correct TTN server is selected, that the correct port is configured (TTN expects LNS over 8887), that LNS protocol is chosen, that the LNS key (from the " LoRa Basics Station LNS authentication Key " field) is input and that " SSL " checkbox is enabled: 

1632 

**==> picture [505 x 325] intentionally omitted <==**

The last step is to download and import Root Certificates. The page has links to the required file. 

After the certificate file was downloaded, drag and drop it into the RouterOS file menu and import the certificate list: 

1633 

**==> picture [505 x 345] intentionally omitted <==**

This should make the certificate list trusted: 

**==> picture [505 x 171] intentionally omitted <==**
