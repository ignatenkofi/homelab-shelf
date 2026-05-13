## Simple log-in to remote host 

It is able to connect to remote host and initiate ssh session. IP address supports both IPv4 and IPv6. 

```
/system ssh 192.168.88.1
/system ssh 2001:db8:add:1337::beef
```

In this case user name provided to remote host is one that has logged into the router. If other value is required, then user=<username> has to be used. 

```
/system ssh 192.168.88.1 user=lala
/system ssh 2001:db8:add:1337::beef user=lala
```

244
