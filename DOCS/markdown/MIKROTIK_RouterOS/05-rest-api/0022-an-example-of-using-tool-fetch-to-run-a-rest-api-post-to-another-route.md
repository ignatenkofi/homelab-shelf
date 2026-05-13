## An example of using `/tool fetch` to run a REST API POST to another RouterOS device: 

```
/tool fetch http-method=post url="http://<ip-address>/rest/execute" http-data="{\"script\":\"/log info
fetchtest\"}" http-header-field="Content-Type:application/json" output=user user=<username>
password=<password>
```

232
