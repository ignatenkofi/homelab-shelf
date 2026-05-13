## `/routing/filter/rule` 

```
add chain=ospf_in rule="if (dst==0.0.0.0/0 && protocol static) { accept }"
```

For example, ROSv6 rule "/routing filter add chain=ospf_in prefix=172.16.0.0/16 prefix-length=24 protocol=static action=accept" converted to ROSv7 would be:
