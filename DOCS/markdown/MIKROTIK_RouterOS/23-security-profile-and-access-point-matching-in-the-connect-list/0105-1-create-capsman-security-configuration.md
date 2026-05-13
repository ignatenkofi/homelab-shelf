## 1. Create CAPsMAN security configuration 

2. Configure AAA settings 

3. Configure Radius server clients 

4. Assign the configuration to your master profile (or directly to CAP itself) 

```
/caps-man security add authentication-types=wpa2-eap eap-methods=passthrough encryption=aes-ccm group-
encryption=aes-ccm name=radius
```

```
/caps-man aaa set called-format=ssid
```

```
/radius add address=x.x.x.x secret=SecretUserPass service=wireless called-id=SSID1
```

```
/radius add address=y.y.y.y secret=SecretUserPass service=wireless called-id=SSID2
```

```
/caps-man configuration set security=radius
```

1462 

Now everyone connecting to CAP's with ssid= SSID1 will have their radius authentication requests sent to x.x.x.x and everyone connecting to CAP's with ssid= SSID2 will have their radius authentication requests sent to y.y.y.y
