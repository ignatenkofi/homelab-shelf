## Radius authentication with one server 

1. Create CAPsMAN security configuration 

2. Configure Radius server client 

3. Assign the configuration to your master profile (or directly to CAP itself) 

```
/caps-man security add authentication-types=wpa2-eap eap-methods=passthrough encryption=aes-ccm group-
encryption=aes-ccm name=radius
```

```
/radius add address=x.x.x.x secret=SecretUserPass service=wireless
```

```
/caps-man configuration set security=radius
```
