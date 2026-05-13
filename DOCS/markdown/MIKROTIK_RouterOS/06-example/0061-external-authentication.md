## External authentication 

Another example is making HotSpot to authenticate on a remote server (which may, for example, perform credit card charging): 

Allow direct access to the external server in walled-garden (either HTTP-based or IP-based) 

Modify the login page of the HotSpot servlet to redirect to the external authentication server. The external server should modify the RADIUS database as needed 

Here is an example of such a login page to put on the HotSpot router (it is redirecting to https://auth.example.com/login.php, replace with the actual address of an external authentication server): 

```
<html>
```

```
<title>...</title>
```

```
<body>
```

```
<form name="redirect" action="https://auth.example.com/login.php" method="post">
<input type="hidden" name="mac" value="$(mac)">
<input type="hidden" name="ip" value="$(ip)">
<input type="hidden" name="username" value="$(username)">
<input type="hidden" name="link-login" value="$(link-login)">
<input type="hidden" name="link-orig" value="$(link-orig)">
<input type="hidden" name="error" value="$(error)">
</form>
<script language="JavaScript">
<!--
        document.redirect.submit();
//-->
</script>
</body>
</html>
```

The external server can log in a HotSpot client by redirecting it back to the original HotSpot servlet login page, specifying the correct username and password 

Here is an example of such a page (it is redirecting to https://hotspot.example.com/login, replace with the actual address of a HotSpot router; also, it is displaying www.mikrotik.com after successful login, replace with what is needed): 

302 

```
<html>
```

```
<title>Hotspot login page</title>
<body>
```

```
<form name="login" action="https://hotspot.example.com/login" method="post">
```

```
<input type="text" name="username" value="demo">
```

```
<input type="password" name="password" value="none">
<input type="hidden" name="domain" value="">
<input type="hidden" name="dst" value="http://www.mikrotik.com/">
<input type="submit" name="login" value="log in">
</form>
</body>
</html>
```

Hotspot will ask the RADIUS server whether to allow the login or not. If allowed, alogin.html page will be displayed (it can be modified to do anything). If not allowed, the flogin.html (or login.html) page will be displayed, which will redirect the client back to the external authentication server. 

Note: as shown in these examples, HTTPS protocol and POST method can be used to secure communications.
