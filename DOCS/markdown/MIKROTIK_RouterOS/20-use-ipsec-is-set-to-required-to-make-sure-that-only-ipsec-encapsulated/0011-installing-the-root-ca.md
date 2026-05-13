## Installing the root CA 

Start off by downloading and importing the NordVPN root CA certificate. 

```
/tool fetch url="https://downloads.nordvpn.com/certificates/root.der"
```

```
/certificate import file-name=root.der
```

There should now be the trusted NordVPN Root CA certificate in System/Certificates menu. 

```
[admin@MikroTik] > /certificate print where name~"root.der"
```

```
Flags: K - private-key, L - crl, C - smart-card-key, A - authority, I - issued, R - revoked, E - expired, T -
trusted
#         NAME            COMMON-NAME            SUBJECT-ALT-NAME
FINGERPRINT
```

```
0       T root.der_0      NordVPN Root CA
8b5a495db498a6c2c8c...
```
