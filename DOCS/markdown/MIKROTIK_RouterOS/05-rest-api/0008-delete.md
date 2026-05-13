## DELETE 

This method is used to delete the record with a specified ID from the menu encoded in the URL. If the deletion has been succeeded, the server responds with an empty response. For example, call to delete the record twice, on second call router will return 404 error: 

- `$ curl -k -u admin: -X DELETE https://10.155.101.214/rest/ip/address/*9` 

```
$ curl -k -u admin: -X DELETE https://10.155.101.214/rest/ip/address/*9
{"error":404,"message":"Not Found"}
```
