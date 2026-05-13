## User Password Access 

For MikroTik routers, it's essential to set up passwords. We recommend using a password generator tool to create robust passwords that meet the following criteria: 

At least 12 characters long; 

Consist of numbers, symbols, uppercase, and lowercase letters; Avoid using dictionary words or combinations thereof. 

```
/user set 0 password="!={Ba3N!40TX+GvKBzjTLIUcx/,"
```

Another method to set a password for the current user: 

24 

```
/password
```

We highly recommend using a secondary method or the Winbox interface to update your router's password, as an added measure to safeguard against unauthorized access. 

```
[admin@MikroTik] > /password
old-password: ********
new-password: ****************************
confirm-new-password: ****************************
```

Ensure you remember the password! If it's forgotten, there's no way to recover it. You'll have to reset the configuration or reinstall the router system! 

You can also add additional users with full or limited router access in the /user menu 

**==> picture [13 x 12] intentionally omitted <==**

The best practice is to create a new user with a strong password and disable or remove the default admin user. 

```
/user add name=myname password=mypassword group=full
/user remove admin
```

**==> picture [13 x 12] intentionally omitted <==**

Note: Log in to the router using the new credentials to verify that the username and password are functioning correctly, before deleting the admin user.
