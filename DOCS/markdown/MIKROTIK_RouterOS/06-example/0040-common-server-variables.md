## Common server variables: 

hostname - DNS name or IP address (if DNS name is not given) of the HotSpot Servlet ("hotspot.example.net") identity - RouterOS identity name ("MikroTik") 

login-by - authentication method used by user 

- plain-passwd - a "yes/no" representation of whether HTTP-PAP login method is allowed ("no") server-address - HotSpot server address ("10.5.50.1:80") 

- ssl-login - a "yes/no" representation of whether HTTPS method was used to access that servlet page ("no") server-name - HotSpot server name (set in the /ip hotspot menu, as the name property) 

Links: 

298 

link-login - link to login page including original URL requested ("http://10.5.50.1/login?dst=http://www.example.com/") link-login-only - link to login page, not including original URL requested ("http://10.5.50.1/login") link-logout - link to logout page ("http://10.5.50.1/logout") link-status - link to status page ("http://10.5.50.1/status") link-orig - original URL requested ("http://www.example.com/")
