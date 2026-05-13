## Get file content received by fetch tool 

Fetch tool allows for ease of use downloading file content into memory and allowing to access this data by script. To make it work use as-value parameter and output=user: 

```
[admin@rack1_b34_CCR1036] > :put ([/tool fetch ftp://admin:@10.155.136.41/test.txt
output=user as-value ]->"data")
my file content
```

1127
