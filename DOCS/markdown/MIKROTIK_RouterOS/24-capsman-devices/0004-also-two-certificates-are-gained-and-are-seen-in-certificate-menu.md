## Also, two certificates are gained and are seen in Certificate menu: 

```
[admin@CAP] > /certificate print
Flags: K - private-key, D - dsa, L - crl, C - smart-card-key, A - authority, I - issued, R - revoked, E -
expired, T - trusted
#          NAME              COMMON-NAME              SUBJECT-ALT-NAME
FINGERPRINT
0     A  T _0                CAPsMAN-CA-D4CA6D987C26
383e63d7b...
1 K        CAP-D4CA6D7F45BA  CAP-D4CA6D7F45BA
d495d1a94...
```

On CAPsMAN device in Certificate menu three certificates are created. CAPsMAN and CAPsMAN-CA certificates, as well as a certificate which is issued to CAP: 

```
[admin@CAPsMAN] > /certificate print
Flags: K - private-key, D - dsa, L - crl, C - smart-card-key, A - authority, I - issued, R - revoked, E -
expired, T - trusted
#          NAME                     COMMON-NAME              SUBJECT-ALT-NAME
FINGERPRINT
0 K   A  T CAPsMAN-CA-D4CA6D987C26  CAPsMAN-CA-D4CA6D987C26
383e63d7b...
1 K    I   CAPsMAN-D4CA6D987C26     CAPsMAN-D4CA6D987C26
02b0f7ff4...
2      I   issued_1                 CAP-D4CA6D7F45BA
d495d1a94...
```
