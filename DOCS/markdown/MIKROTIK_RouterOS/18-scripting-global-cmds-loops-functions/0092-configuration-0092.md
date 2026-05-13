## Configuration 

To set system identity in RouterOS: 

```
[admin@MikroTik] > /system identity set name=New_Identity
[admin@New_Identity] >
```

The current System Identity is always displayed after the logged-in account name and with the print command: 

```
[admin@New_Identity] /system identity>print
name: New_Identity
[admin@New_Identity] /system identity>
```
