## Static IP address for a user 

To assign the end user a static IP address, Framed-IP-Address attribute can be used. When using static IP address allocation, shared-sessions must be set to 1 to prevent cases when a user has multiple simultaneous sessions, but there is only one IP address. For example: 

340 

```
/user-manager user
```

```
set [find name=username] shared-users=1 attributes=Framed-IP-Address:192.168.1.4
```
