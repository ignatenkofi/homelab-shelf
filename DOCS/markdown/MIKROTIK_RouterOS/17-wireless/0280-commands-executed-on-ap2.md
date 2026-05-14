## Commands executed on ap2 

```
# Configuring radius client
/radius
```

```
add address=10.0.0.10 secret="Use a secure password generator for this too" service=wireless timeout=1s
/radius incoming
set accept=yes
# Configuring enabled authentication types. Can also be done via a security profile, but note that interface
properties, if specified, override profile properties
/interface/wifiwave2 set [find] security.authentication-types=wpa2-eap,wpa3-eap
```

A wifiwave2 AP can  also be configured to use the extra secure wpa3-eap-192 mode, but note that it requires that all client devices support the GCMP-256 cipher and use EAP-TLS authentication.
