## Using TOTP (time-based one-time password) for user authentication 

User Manager supports time-based authentication token addition to the user's password field that is regenerated every 30 seconds. 

**==> picture [13 x 13] intentionally omitted <==**

OTP depends on the clock, so make sure time settings are configured correctly. 

TOTP works by having a shared secret on the supplicant (client) and the authentication server (User Manager). To configure TOTP on RouterOS, simply set the otp-secret for the user. For example: 

```
/user-manager user
```

```
set [find name=username] password=mypass otp-secret=mysecret
```

To calculate the TOTP token on the supplicant side, many widely available applications can be used, for example, Google Authenticator or https://totp.app/. Adding mysecret to the TOTP token generator will provide a new unique 6-digit code that must be added to the user password. 

**==> picture [341 x 153] intentionally omitted <==**

The following example will accept the user's authentication with a calculated TOTP token added to the common password until a new TOTP token is generated, for example, 

```
User-Name=username
User-Password=mypass620872
```
