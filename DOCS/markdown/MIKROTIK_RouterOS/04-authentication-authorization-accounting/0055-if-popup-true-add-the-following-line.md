## $(if popup == 'true') add the following line: 

```
open('http://www.example.com/your-banner-page.html', 'my-banner-name','');
```

(you should correct the link to point to the page you want to show) 

To choose a different page shown after login, in login.html change: 

```
<input type="hidden" name="dst" value="$(link-orig)">
```
