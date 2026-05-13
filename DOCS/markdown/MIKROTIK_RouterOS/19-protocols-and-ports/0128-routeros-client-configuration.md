## RouterOS client configuration 

Import a PKCS12 format certificate in RouterOS. 

```
/certificate import file-name=cert_export_RouterOS_client.p12 passphrase=1234567890
```

There should now be the self-signed CA certificate and the client certificate in the Certificate menu. Find out the name of the client certificate. 

```
/certificate print
```

cert_export_RouterOS_client.p12_0 is the client certificate. 

It is advised to create a separate Phase 1 profile and Phase 2 proposal configurations to not interfere with any existing IPsec configuration. 

```
/ip ipsec profile
add name=ike2-rw
/ip ipsec proposal
add name=ike2-rw pfs-group=none
```

While it is possible to use the default policy template for policy generation, it is better to create a new policy group and template to separate this configuration from any other IPsec configuration. 

```
/ip ipsec policy group
add name=ike2-rw
/ip ipsec policy
add group=ike2-rw proposal=ike2-rw template=yes
```

Create a new mode config entry with responder=no that will request configuration parameters from the server. 

```
/ip ipsec mode-config
add name=ike2-rw responder=no
```

Lastly, create peer and identity configurations. 

```
/ip ipsec peer
```

```
add address=2.2.2.2/32 exchange-mode=ike2 name=ike2-rw-client
/ip ipsec identity
```

```
add auth-method=digital-signature certificate=cert_export_RouterOS_client.p12_0 generate-policy=port-strict
mode-config=ike2-rw peer=ike2-rw-client policy-template-group=ike2-rw
```

Verify that the connection is successfully established. 

```
/ip ipsec
active-peers print
installed-sa print
```
