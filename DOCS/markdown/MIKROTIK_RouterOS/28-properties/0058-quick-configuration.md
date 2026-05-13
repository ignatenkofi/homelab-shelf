## Quick Configuration 

To enable SNMP in RouterOS: 

1812 

```
[admin@MikroTik] /snmp> print
enabled: no
contact:
location:
engine-id:
trap-community: (unknown)
trap-version: 1
[admin@MikroTik] /snmp> set enabled yes
```

You can also specify administrative contact information in the above settings. All SNMP data will be available to communities configured in the community menu.
