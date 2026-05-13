## Linux (strongSwan) client configuration 

Download the PKCS12 certificate bundle and move it to /etc/ipsec.d/private directory. 

Add exported passphrase for the private key to /etc/ipsec.secrets file where "strongSwan_client.p12" is the file name and "1234567890" is the passphrase. 

```
: P12 strongSwan_client.p12 "1234567890"
```

Add a new connection to /etc/ipsec.conf file 

```
conn "ikev2"
keyexchange=ikev2
ike=aes128-sha1-modp2048
esp=aes128-sha1
leftsourceip=%modeconfig
leftcert=strongSwan_client.p12
leftfirewall=yes
right=2.2.2.2
rightid="CN=2.2.2.2"
rightsubnet=0.0.0.0/0
auto=add
```

You can now restart (or start) the ipsec daemon and initialize the connection 

1223 

```
$ ipsec restart
```

```
$ ipsec up ikev2
```
