## MAC telnet 

There is a limitation for MAC telnet when L3HW offloading is enabled on 98DX8xxx , 98DX4xxx, or 98DX325x switch chips. Packets from MAC Telnet are dropped and do not reach the CPU, thus access to the device will fail. 

440 

If MAC telnet is desired in combination with L3HW, certain ACL rule can be created to force these packets to the CPU. 

For example, if MAC telnet access on sfp-sfpplus1 and sfp-sfpplus2 is needed, you will need to add this ACL rule. It is possible to select even more interfaces with the `ports` setting. 

```
/interface ethernet switch rule
```

```
add dst-port=20561 ports=sfp-sfpplus1,sfp-sfpplus2 protocol=udp redirect-to-cpu=yes switch=switch1
```
