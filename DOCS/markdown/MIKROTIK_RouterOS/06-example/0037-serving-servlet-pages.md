## Serving Servlet Pages 

The HotSpot servlet recognizes 5 different request types: 

1. request for a remote host 

   - if user is logged in and advertisement is due to be displayed, radvert.html is displayed. This page redirects to the scheduled advertisement page if user is logged in and advertisement is not scheduled for this user, the requested page is served 

   - if user is not logged in, but the destination host is allowed by the walled garden, then the request is also served 

297 

if user is not logged in, and the destination host is disallowed by the walled garden, rlogin.html is displayed; if rlogin.html is not found, redirect.html is used to redirect to the login page 

2. request for "/" on the HotSpot host 

if user is logged in, rstatus.html is displayed; if rstatus.html is not found, redirect.html is used to redirect to the status page if user is not logged in, rlogin.html is displayed; if rlogin.html is not found, redirect.html is used to redirect to the login page 

3. request for "/login" page 

if user has successfully logged in (or is already logged in), alogin.html is displayed; if alogin.html is not found, redirect.html is used to redirect to the originally requested page or the status page (in case, the original destination page was not given) if user is not logged in (username was not supplied, no error message appeared), login.html is showed 

if login procedure has failed (an error message is supplied), flogin.html is displayed; if flogin.html is not found, login.html is used in case of fatal errors, error.html is showed 

4. request for "/status" page 

if user is logged in, status.html is displayed 

if user is not logged in, fstatus.html is displayed; if fstatus.html is not found, redirect.html is used to redirect to the login page 

5. request for '/logout' page 

if user is logged in, logout.html is displayed 

if user is not logged in, flogout.html is displayed; if flogout.html is not found, redirect.html is used to redirect to the login page 

Note: If it is not possible to meet a request using the pages stored on the router's FTP server, Error 404 is displayed 

There are many ways to customize what the HotSpot authentication pages look like: 

The pages are easily modifiable. They are stored on the router's FTP server in the directory you choose for the respective HotSpot server profile. By changing the variables, which client sends to the HotSpot servlet, it is possible to reduce the keyword count to one (username or password; for example, the client's MAC address may be used as the other value) or even to zero (License Agreement; some predefined values general for all users or client's MAC address may be used as username and password) 

Registration may occur on a different server (for example, on a server that is able to charge Credit Cards). Client's MAC address may be passed to it, so that this information doesn't have to be entered manually. After the registration, the server should change RADIUS database enabling client to log in for some amount of time. 

To insert a variable in some place in the HTML file, the $(var_name) syntax is used, where the "var_name" is the name of the variable (without quotes). This construction may be used in any HotSpot HTML file accessed as '/', '/login', '/status' or '/logout', as well as any text or HTML (.txt, .htm or .html) file stored on the HotSpot server (with the exception of traffic counters, which are available in status page only, and error , error-orig , chap-id , chap-challenge and popup variables, which are available in login page only). For example, to show a link to the login page, following construction can be used: 

```
<a href="$(link-login)">login</a>
```
