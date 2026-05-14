## Sub-menu: **`/snmp community`** 

This sub-menu allows to set up access rights for the SNMP data. 

There is little security in v1 and v2c, just Clear text community string („username“) and the ability for Limiting access by IP address. 

In the production environment, SNMP v3 should be used as that provides security - Authorization (User + Pass) with MD5/SHA1, Encryption with DES and AES). 

```
[admin@MikroTik] /snmp community> print value-list
name: public
address: 0.0.0.0/0
security: none
read-access: yes
write-access: no
authentication-protocol: MD5
encryption-protocol: DES
authentication-password: *****
encryption-password: *****
```

**==> picture [13 x 13] intentionally omitted <==**

Default settings only have one community named public without any additional security settings. These settings should be considered insecure and should be adjusted according to the required security profile.
