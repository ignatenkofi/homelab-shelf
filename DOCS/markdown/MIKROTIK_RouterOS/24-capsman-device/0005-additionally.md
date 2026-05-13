## Additionally 

If you want to allow only CAPs with a valid certificate to connect to this CAPsMAN you can set Require Peer Certificate to yes on CAPsMAN device: 

```
/caps-man manager
set require-peer-certificate=yes
```

However, when you will want to add new CAP devices to your CAPsMAN network you will have to set this option to no and then back to yes after CAP has gained certificates. Every time you change this option CAPsMAN will drop all dynamic interfaces and CAPs will try to connect again. 

If you want to lock CAP to specific CAPsMAN and be sure it won't connect to other CAPsMANs you should set option Lock To CAPsMAN to yes. Additionally, you can specify CAPsMAN to lock to by setting CAPsMAN Certificate Common Names on CAP device: 

```
/interface wireless cap
set lock-to-caps-man=yes
set caps-man-certificate-common-names=CAPsMAN-D4CA6D987C26
```
