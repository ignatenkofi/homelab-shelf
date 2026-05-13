## to this line: 

```
<input type="hidden" name="dst" value="http://www.example.com">
```

(you should correct the link to point to your server) 

To erase the cookie on logoff, in the page containing a link to the logout (for example, in status.html) change: 

```
open('$(link-logout)', 'hotspot_logout', ...
```
