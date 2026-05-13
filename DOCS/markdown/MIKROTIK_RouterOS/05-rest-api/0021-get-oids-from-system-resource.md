## `Get OIDs from /system resource:` 

```
curl -k -u <username>:<password> -X POST http://<ip-address>/rest/system/resource/print --data '{"oid":""}' -H
"content-type: application/json"
```

**==> picture [13 x 12] intentionally omitted <==**

There is no option to run a "continuous" command, like "monitor" via REST API. Use "monitor once" parameter instead to print the result once.
