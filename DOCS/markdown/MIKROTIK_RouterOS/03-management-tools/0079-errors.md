## Errors 

The success or failure of the API calls is indicated in the HTTP status code. In case of failure (status code 400 or larger), the body of the response contains a JSON object with the error code, a description of the error, and optional error details. For example, trying to delete an interface will return 

```
{"error":406,"message":"Not Acceptable","detail":"no such command or directory (remove)"}
```
