## RouterOS Supplicant configuration 

CA certificates are required for `eap-tls, eap-ttls` and `eap-peap` authentication methods. Additionally a client certificate is required for `eap-tls` method. For this example we have already imported a P12 certificate bundle with self signed client and CA certificates. For more information how to import certificates in RouterOS, please visit System/Certificates. 

```
/certificate print
```

```
Flags: K - private-key, L - crl, C - smart-card-key, A - authority, I - issued, R - revoked, E - expired, T
- trusted
 #         NAME                                            COMMON-
NAME                                         SUBJECT-ALT-NAME
FINGERPRINT
 0 K  A  T dot1x-client                                    ez_dot1x-
client                                     IP:10.1.2.34
 1  L A  T dot1x CA                                        ca
```

Simply add a new dot1x client instance that will initiate authentication process. 

```
/interface dot1x client
```

```
add anon-identity=anonymous client-certificate=dot1x-client eap-methods=eap-tls identity=dot1x-user
interface=ether1 password=dot1xtest
```

If authentication was successful, the interface should have status authenticated. 

```
/interface dot1x client print
Flags: I - inactive, X - disabled
```

```
 0   interface=ether1 eap-methods=eap-peap identity="dot1x-user" password="dot1xtest" anon-identity="
anonymous" client-certificate=dot1x-client status="authenticated"
```

290
