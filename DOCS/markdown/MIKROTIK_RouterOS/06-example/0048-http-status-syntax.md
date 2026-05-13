## http-status syntax : 

- `$(if http-status == XYZ)HTTP_STATUS_MESSAGE$(endif)` 

XYZ - The status code you wish to return. Should be 3 decimal digits, the first one must not be 0 

HTTP_STATUS_MESSAGE - any text you wish to return to the client that will follow the above status code in the HTTP reply 

In any HTTP response it will be on the first line and will be as follows: 

```
HTTP/1.0 XYZ HTTP_STATUS_MESSAGE
```
