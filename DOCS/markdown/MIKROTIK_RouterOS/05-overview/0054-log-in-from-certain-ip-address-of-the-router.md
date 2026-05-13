## Log-in from certain IP address of the router 

For testing or security reasons it may be required to log in to other host using certain source address of the connection. In this case src-address=<ip address> argument has to be used. Note that IP address in this case supports both, IPv4 and IPv6. 

```
/system ssh 192.168.88.1 src-address=192.168.89.2
```

```
/system ssh 2001:db8:add:1337::beef src-address=2001:db8:bad:1000::2
```

in this case, ssh client will try to bind to address specified and then initiate ssh connection to remote host.
