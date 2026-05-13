## Enabling PKI authentication 

Example of importing public key for user admin 

Get SSH key pair on the client device (the device you will connect from). Upload the public SSH key to the router and import it. 

More information about supported SSH keys find here. 

```
/user ssh-keys import public-key-file=id_rsa.pub user=admin
```
