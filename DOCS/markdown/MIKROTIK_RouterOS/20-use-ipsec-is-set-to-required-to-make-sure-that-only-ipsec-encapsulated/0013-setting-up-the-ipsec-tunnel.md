## Setting up the IPsec tunnel 

It is advised to create a separate Phase 1 profile and Phase 2 proposal configurations to not interfere with any existing or future IPsec configuration. 

```
/ip ipsec profile
add name=NordVPN
/ip ipsec proposal
add name=NordVPN pfs-group=none
```

While it is possible to use the default policy template for policy generation, it is better to create a new policy group and template to separate this configuration from any other IPsec configuration. 

```
/ip ipsec policy group
add name=NordVPN
/ip ipsec policy
```

```
add dst-address=0.0.0.0/0 group=NordVPN proposal=NordVPN src-address=0.0.0.0/0 template=yes
```

Create a new mode config entry with responder=no that will request configuration parameters from the server. 

```
/ip ipsec mode-config
```

```
add name=NordVPN responder=no
```

Lastly, create peer and identity configurations. Specify your NordVPN credentials in username and password parameters. 

```
/ip ipsec peer
```

```
add address=lv20.nordvpn.com exchange-mode=ike2 name=NordVPN profile=NordVPN
/ip ipsec identity
```

```
add auth-method=eap certificate="" eap-methods=eap-mschapv2 generate-policy=port-strict mode-config=NordVPN
peer=NordVPN policy-template-group=NordVPN username=support@mikrotik.com password=secret
```

Verify that the connection is successfully established. 

```
/ip ipsec
active-peers print
installed-sa print
```
