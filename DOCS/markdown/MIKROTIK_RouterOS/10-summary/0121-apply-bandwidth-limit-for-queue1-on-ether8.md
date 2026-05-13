## Apply bandwidth limit for queue1 on ether8: 

```
/interface ethernet switch shaper
add port=ether8 rate=10M target=queue1
```

If the CRS switch supports Access Control List, this configuration is simpler: 

```
/interface ethernet switch acl policer
add name=policer1 yellow-burst=100k yellow-rate=10M
```

```
/interface ethernet switch acl
```

```
add mac-dst-address=E7:16:34:A1:CD:18 policer=policer1
```
