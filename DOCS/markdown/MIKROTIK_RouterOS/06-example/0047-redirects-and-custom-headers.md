## Redirects and custom Headers 

- `$(if http-status == 302)Hotspot login required$(endif)` 

- `$(if http-header == "Location")$(link-redirect)$(endif)` 

Note: Although the above appears to use the conditional expression 'if' it is in fact setting the 'http-status' to '302' not testing for it. Also the same for the variable 'http-header'. Once again, even though it uses an 'if' it is in fact setting the variable to 'Location' followed by the URL set from the variable 'linkredirect'. 

For example, in the case where $(link-redirect) evaluates to "http://192.168.88.1/login", then the HTTP response returned to the client will be changed to: 

```
HTTP/1.0 302 Hotspot login required
<regular HTTP headers>
Location: http://192.168.88.1/login
```
