## Configuring RADIUS client 

For the router to use RADIUS server for user authentication, it is required to add a new RADIUS client that has the same shared secret that we already configured on User Manager. 

```
/radius
```

```
add address=127.0.0.1 secret=test service=ipsec
```
