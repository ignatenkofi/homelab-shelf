## Using MQTT to post the data 

In order to use a one-way SSL MQTT scenario, get the root certificate from " Home>Device management>Credentials " by clicking on the " Get root certificate " button. More info can be found here. 

Upload ca.pem certificate file to the RouterOS and import it using: 

```
/certificate/import file-name=ca.pem passphrase=""
```
