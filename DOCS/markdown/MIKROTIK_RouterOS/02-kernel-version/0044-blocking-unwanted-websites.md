## Blocking Unwanted Websites 

Sometimes you may want to block certain websites, for example, deny access to entertainment sites for employees, deny access to porn, and so on. This can be achieved by redirecting HTTP traffic to a proxy server and use an access-list to allow or deny certain websites. 

First, we need to add a NAT rule to redirect HTTP to our proxy. We will use RouterOS built-in proxy server running on port 8080. 

```
/ip firewall nat
```

```
  add chain=dst-nat protocol=tcp dst-port=80 src-address=192.168.88.0/24 \
    action=redirect to-ports=8080
```

Enable web proxy and drop some websites: 

```
/ip proxy set enabled=yes
```

```
/ip proxy access add dst-host=www.facebook.com action=deny
```

```
/ip proxy access add dst-host=*.youtube.* action=deny
/ip proxy access add dst-host=:vimeo action=deny
```

Using Winbox: 

On the left menu navigate to IP -> Web Proxy 

Web proxy settings dialog will appear. 

Check the "Enable" checkbox and click on the "Apply" button Then click on the "Access" button to open the "Web Proxy Access" dialog 

33 

**==> picture [504 x 423] intentionally omitted <==**

In the "Web Proxy Access" dialog click on "+" to add a new Web-proxy rule Enter Dst hostname that you want to block, in this case, "www.facebook.com", choose the action "deny" Then click on the "Ok" button to apply changes. Repeat the same to add other rules. 

34 

**==> picture [504 x 247] intentionally omitted <==**
