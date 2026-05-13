## Administrative Services 

Although the firewall protects the router from the public interface, you may still want to disable RouterOS services. 

Most of RouterOS administrative tools are configured at  the /ip service menu 

Keep only the ones, you plan to actively use 

```
/ip service disable telnet,ftp,www,api
```

29 

Change default service ports, this will immediately stop most of the random SSH brute force login attempts: 

```
/ip service set ssh port=2200
```

Additionally, each service can be secured by allowed IP address or address range(the address service will reply to), although more preferred method is to block unwanted access in firewall because the firewall will not even allow to open socket 

```
/ip service set winbox address=192.168.88.0/24
```
