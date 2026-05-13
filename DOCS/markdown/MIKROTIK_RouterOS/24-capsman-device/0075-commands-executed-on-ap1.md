## Commands executed on ap1 

```
# Configuring radius client
/radius
```

```
add address=10.0.0.10 secret="Use a secure password generator for this" service=wireless timeout=1s
/radius incoming
set accept=yes
# Adding a security profile and applying it to wireless interfaces
/interface/wireless/security-profile
add name=radius mode=dynamic-keys authentication-types=wpa2-eap
/interface/wireless
set [find] security-profile=radius
```
