## 5.1 Certificates 

QKD requires: 

CA certificate (to validate the server). 

SAE client certificate (for authentication to the QKD server). 

- `/certificate import file-name=ca.crt.pem` 

- `/certificate import file-name=sae-server.crt.pem /certificate import file-name=sae-server.key.pem`
