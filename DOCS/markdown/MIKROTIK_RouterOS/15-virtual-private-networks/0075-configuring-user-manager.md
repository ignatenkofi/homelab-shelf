## Configuring User Manager 

1224 

First of all, allow receiving RADIUS requests from the localhost (the router itself): 

```
/user-manager router
```

```
add address=127.0.0.1 comment=localhost name=local shared-secret=test
```

Enable the User Manager and specify the Let's Encrypt certificate (replace the name of the certificate to the one installed on your device) that will be used to authenticate the users. 

```
/user-manager
```

```
set certificate="letsencrypt_2021-04-09T07:10:55Z" enabled=yes
```

Lastly add users and their credentials that clients will use to authenticate to the server. 

```
/user-manager user
add name=user1 password=password
```
