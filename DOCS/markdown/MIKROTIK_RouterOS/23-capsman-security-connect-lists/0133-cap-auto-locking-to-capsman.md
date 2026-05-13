## CAP Auto Locking to CAPsMAN 

CAP can be configured to automatically lock to a particular CAPsMAN server. Locking is implemented by recording certificate CommonName of CAPsMAN that CAP is locked to and checking this CommonName for all subsequent connections. As this feature is implemented using certificate CommonName, use of certificates is mandatory for locking to work. 

Locking is enabled by the following command: 

```
[admin@CAP] > /interface wireless cap set lock-to-caps-man=yes
```

Once CAP connects to suitable CAPsMAN and locks to it, it is reflected like this: 

```
[admin@wtp] > /interface wireless cap print
```

```
...
```

```
       locked-caps-man-common-name: CAPsMAN-000C424C30F3
```

From now on CAP will only connect to CAPsMAN with this CommonName, until locking requirement is cleared, by setting lock-to-caps-man=no . This approach needs to be used if it is necessary to force CAP to lock to another CAPsMAN - by at first setting lock-to-caps-man=no followed by lock-to-capsman=yes . 

Note that CAP can be manually "locked" to CAPsMAN by setting caps-man-certificate-common-names .
