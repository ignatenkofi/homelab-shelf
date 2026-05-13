## Configuration examples 

Creating a DLNA server 

```
/ip media add friendly-name=Mikrotik interface=bridge1 path=usb1
```

Creating multiple DLNA servers with limitations. Usage example - Limit children's TV access only to child-friendly media, located in folder "usb1/kids" 

```
/ip media add friendly-name=adults interface=bridge1 path=usb1/adults allowed-hostname=ADULTS_TV
/ip media add friendly-name=kids interface=bridge1 path=usb1/kids allowed-hostname=KIDS_TV
```

1897
