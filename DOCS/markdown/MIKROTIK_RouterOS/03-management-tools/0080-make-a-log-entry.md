## `Make a log entry:` 

```
curl -k -u <username>:<password> -X POST http://<ip-address>/rest/execute --data '{"script":"/log/info test"}' -
H "content-type: application/json"
```
