## 5.3 QKD Key Manager 

RouterOS server can act as a QKD client: 

- `/ip ipsec key qkd set address=10.13.2.9:8020 \ cache-size=1 \ certificate=sae-server \ key-size=32 \ kme-id=server-kme-id \ peer-sae-id=client-sae-id` 

Parameter descriptions: 

**==> picture [325 x 117] intentionally omitted <==**

**----- Start of picture text -----**<br>
Parameter Description<br>cache-size Number of keys IPsec will prefetch from QKD server.<br>cache-state Current number of keys cached and available.<br>key-size Requested size of each key in bytes (e.g., 32 bytes = 256 bits).<br>kme-id Used for certificate validation. If not specified, KME identity will not be validated.<br>peer-sae-id Identifier for the peer SAE.<br>**----- End of picture text -----**<br>


1233
