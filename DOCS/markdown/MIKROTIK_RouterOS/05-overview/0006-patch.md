## PATCH 

This method is used to update a single record. Set PATCH call body as a JSON object which contains fields and values of the properties to be updated. For example, add a comment: 

- `$ curl -k -u admin: -X PATCH https://10.155.101.214/rest/ip/address/*3 \` 

- `--data '{"comment": "test"}' -H "content-type: application/json"` 

```
{".id":"*3","actual-interface":"dummy","address":"192.168.99.2/24","comment":"test",
```

- `"disabled":"false","dynamic":"false","interface":"dummy","invalid":"false","network":"192.168.99.0"}` 

In case of a successful update, the server returns the updated object with all its parameters.
