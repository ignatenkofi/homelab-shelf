## http-header syntax: 

- `$(if http-header == HTTP_HEADER_NAME)HTTP_HEADER_VALUE$(endif)` 

HTTP_HEADER_NAME - name of the HTTP header to be sent in the response 

HTTP_HEADER_VALUE - the value of the HTTP header with the name HTTP_HEADER_NAME to be sent in the response 

The HTTP response will appear as: 

```
HTTP_HEADER_NAME: HTTP_HEADER_VALUE
```

All variables and conditional expressions within HTTP_HEADER_VALUE and HTTP_STATUS_MESSAGE are processed as usual. 

In case multiple headers with the same name are added, then only the last one will be used (previous ones will be discarded). It allows the system to override regular HTTP headers (for example, Content-Type and Cache-Control).
