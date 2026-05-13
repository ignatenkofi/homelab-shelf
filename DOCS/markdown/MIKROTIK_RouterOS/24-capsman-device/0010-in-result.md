## In Result 

Now CAP should be able to connect to CAPsMAN, see in CAPsMAN interfaces if it connects. In CAPsMAN device Certificate menu three certificates can be seen: CA, CAPsMAN, and the one which is issued to CAP: 

```
[admin@CAPsMAN] /certificate print
Flags: K - private-key, D - dsa, L - crl, C - smart-card-key, A - authority, I - issued, R - revoked,
E - expired, T - trusted
#          NAME        COMMON-NAME      SUBJECT-ALT-NAME                                   FINGERPRINT
0 K L A  T CA          CA                                                                  752775b457a37...
1 K   A    CAPsMAN     CAPsMAN                                                             12911ba445b3b...
2      I   issued_1    CAP1                                                                5b9a52b6ce3fb...
```

In CAP devices Certificate menu two acquired certificates can be seen: 

```
[admin@CAP1] /interface wireless> /certificate print
```

```
Flags: K - private-key, D - dsa, L - crl, C - smart-card-key, A - authority, I - issued, R - revoked,
E - expired, T - trusted
#          NAME        COMMON-NAME      SUBJECT-ALT-NAME                                   FINGERPRINT
0   L A  T cert_exp... CA                                                                  752775b457a37...
1 K      T CAP1        CAP1                                                                5b9a52b6ce3fb...
```

1490 

1491
