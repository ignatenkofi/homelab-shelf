## Youtube Matcher 

**==> picture [13 x 13] intentionally omitted <==**

When a user is logged in YouTube will use HTTPS, meaning that L7 will not be able to match this traffic. Only unencrypted HTTP can be matched. 

```
/ip firewall layer7-protocol
```

```
add name=youtube regexp="(GET \\/videoplayback\\\?|GET \\/crossdomain\\.xml)"
```

665
