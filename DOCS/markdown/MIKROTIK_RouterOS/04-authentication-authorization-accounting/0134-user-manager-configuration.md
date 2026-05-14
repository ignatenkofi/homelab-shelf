## User Manager configuration 

Start off by enabling User Manager functionality. 

```
/user-manager
set enabled=yes
```

Allow receiving RADIUS requests from the localhost (the router itself). 

```
/user-manager router
```

```
add address=127.0.0.1 comment=localhost name=local shared-secret=test
```

Next, add users and their credentials that clients will use to authenticate to the server. 

```
/user-manager user
add name=user1 password=password
```
