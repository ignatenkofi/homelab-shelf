## `LTE firmware update:` 

```
curl -k -u <username>:<password> -X POST 'http://<ip-address>/rest/interface/lte/firmware-upgrade'   --data
'{"number":"lte2"}' -H "content-type: application/json"
```
