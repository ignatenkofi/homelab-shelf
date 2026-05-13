## HTTP header detection 

The Hotspot login pages have access to HTTP headers by using $(http-header-name); 

For example, there exists an ability to check the user agent (or browser), and will return any other content instead of the regular login page, if so desired. This can be used to disable automatic popups in phones, for example. 

For example, to output "SUCCESS" for users of a specific Firefox mobile version, instead of the login page, you can these lines on the top of the rlogin.html page in your hotspot directory: 

- `$(if user-agent == "Mozilla/5.0 (Android; Mobile; rv:40.0) Gecko/40.0 Firefox/40.0" ) <HTML><HEAD><TITLE>Success</TITLE></HEAD><BODY>Success</BODY></HTML> $(else)` 

```
---- regular content of rlogin.html page  ----
```

```
$(endif)
```

This will DISABLE the login popup for Android Firefox 40 users.
