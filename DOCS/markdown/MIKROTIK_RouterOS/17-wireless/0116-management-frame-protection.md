## Management frame protection 

Used for : Deauthentication attack prevention, MAC address cloning issue. 

RouterOS implements proprietary management frame protection algorithm based on shared secret. Management frame protection means that RouterOS wireless device is able to verify source of management frame and confirm that particular frame is not malicious. This feature allows to withstand deauthentication and disassociation attacks on RouterOS based wireless devices. 

Management protection mode is configured in security-profile with management-protection setting. Possible values are: disabled - management protection is disabled (default), allowed - use management protection if supported by remote party (for AP - allow both, non-management protection and management protection clients, for client - connect both to APs with and without management protection), required - establish association only with remote devices that support management protection (for AP - accept only clients that support management protection, for client - connect only to APs that support management protection). 

Management protection shared secret is configured with security-profile management-protection-key setting. 

When interface is in AP mode, default management protection key (configured in security-profile) can be overridden by key specified in access-list or RADIUS attribute. 

```
[admin@mikrotik] /interface wireless security-profiles> print
```

```
 0 name="default" mode=none authentication-types="" unicast-ciphers=""
  group-ciphers="" wpa-pre-shared-key="" wpa2-pre-shared-key=""
  supplicant-identity="n-str-p46" eap-methods=passthrough
  tls-mode=no-certificates tls-certificate=none static-algo-0=none
  static-key-0="" static-algo-1=none static-key-1="" static-algo-2=none
  static-key-2="" static-algo-3=none static-key-3=""
  static-transmit-key=key-0 static-sta-private-algo=none
  static-sta-private-key="" radius-mac-authentication=no
  radius-mac-accounting=no radius-eap-accounting=no interim-update=0s
  radius-mac-format=XX:XX:XX:XX:XX:XX radius-mac-mode=as-username
  radius-mac-caching=disabled group-key-update=5m
```

```
management-protection=disabled management-protection-key=""
```

```
[admin@mikrotik] /interface wireless security-profiles> set default management-protection=
                                                        allowed  disabled  required
```

1417 

**==> picture [494 x 472] intentionally omitted <==**
