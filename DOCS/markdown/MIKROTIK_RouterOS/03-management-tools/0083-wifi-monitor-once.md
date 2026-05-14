## `WiFi monitor once:` 

```
curl -k -u <username>:<password> -X POST "http://<ip-address>/rest/interface/wifi/monitor" -H "Content-Type:
application/json" -d '{ "numbers": "wifi1", "once":"" }'
```

```
Export device configuration:
```

231 

```
curl -k -u <username>:<password> https://<ip-address>/rest/export --data '{"compact":"","file":"test.rsc"}' -H
"content-type: application/json"
```
