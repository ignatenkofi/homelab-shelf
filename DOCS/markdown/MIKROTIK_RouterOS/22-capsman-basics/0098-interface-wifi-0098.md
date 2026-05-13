## `/interface wifi` 

```
set [ find default-name=wifi1 ] configuration.country=Latvia .mode=ap .ssid=Orion disabled=no
interworking=interworking security=orion_password_profile
```

Make sure the correct country profile is configured. In this example, we are using “wifi1”, but the same command would work with other interfaces. 

**==> picture [13 x 13] intentionally omitted <==**

NAS-id that's used by Orion to differentiate networks is equal to system identity. To adjust the nas-id, you can do "/system identity set name=exampleName". 

1386
