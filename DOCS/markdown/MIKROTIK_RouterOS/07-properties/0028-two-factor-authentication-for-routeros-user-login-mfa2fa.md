## Two factor authentication for RouterOS user login (MFA/2FA) 

As User-Manager supports TOTP (time-based-one-time password), it is possible to setup so called MFA authentication for different services. Here will will look into RouterOS user authentication over User Manager (radius) with time based password, that is changed every 30 seconds. 

Here are the necessary configuration options on your MikroTik router, 

Enable to use RADIUS for /user menu, and set default-grop from /user group menu. Keep in mind that local /user database is checked first, and then RADIUS is contacted. 

```
/user/aaa/set use-radius=yes default-group=full
```

Enable radius client for login service. As we run User Manager on the same router, 127.0.0.1 is used, 

```
/radius/add address=127.0.0.1 service=login secret=mystrongsecret
```

Here are the configuration steps for User Manager , 

Make sure you have added your managed devices to "Routers" menu, 

```
/user-manager/router/add name=myrouter address=127.0.0.1 shared-secret=mystrongsecret
```

Add user to User-Manager user table with OTP secret parameter. Few more steps are required for proper OTP configuration. 

Pick OTP-secret name and convert it to base32 format (there are plenty of online converters from utf-8 to base32 format). For my configuration I use "mysupersecret", that in base32 would be NV4XG5LQMVZHGZLDOJSXI=== 

```
/user-manager/user/add name=mikrotik password=mysuperpassword otp-secret="NV4XG5LQMVZHGZLDOJSXI==="
```

Note, than in your favorite authenticator app, you will need to set user this key manually "NV4XG5LQMVZHGZLDOJSXI===", when adding new time password instance. 

To login to your MikroTik device, open Winbox/Console and connect to your router address, use login:mikrotik and password:mysuperpasswordxxxxxx, where xxxxxx is 6 digit code from your favorite authentication app. 

Password is changed every 30 seconds and it is available from your favorite app. 

**==> picture [207 x 188] intentionally omitted <==**

348
