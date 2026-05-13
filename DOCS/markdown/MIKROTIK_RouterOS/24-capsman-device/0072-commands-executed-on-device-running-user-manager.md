## Commands executed on device running User Manager 

```
# Enabling User Manager and specifying, which certificate to use
/user-manager
set enabled=yes certificate=userman-cert
# Enabling CRL checking to avoid accepting revoked user certificates
/certificate settings
set crl-download=yes crl-use=yes
# Adding access points
/user-manager router
add name=ap1 address=10.0.0.11 shared-secret="Use a secure password generator for this"
add name=ap2 address=10.0.0.12 shared-secret="Use a secure password generator for this too"
# Limiting allowed authentication methods
/user-manager user group
set [find where name=default] outer-auths=eap-tls,eap-peap
add name=certificate-authenticated outer-auths=eap-tls
# Adding users
/user-manager user
add name=maija@mikrotik.test group=certificate-authenticated
add name=paija@mikrotik.test group=default password="right mule accumulator nail"
```
