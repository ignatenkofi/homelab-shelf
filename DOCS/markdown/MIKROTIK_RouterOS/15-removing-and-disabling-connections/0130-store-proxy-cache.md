## Store proxy cache: 

Important commands: 

max-cache-size= max-cache-object-size= cache-on-disk= cache-path= 

```
[admin@MikroTik] > ip proxy set cache-on-disk=yes cache-path=/usb1/proxy/cache
```

```
[admin@MikroTik] > ip proxy print
                 enabled: yes
             src-address: ::
                    port: 8080
               anonymous: no
            parent-proxy: 0.0.0.0
       parent-proxy-port: 0
     cache-administrator: webmaster
          max-cache-size: unlimited  <-------
   max-cache-object-size: 50000KiB  <-------
           cache-on-disk: yes  <-------
  max-client-connections: 600
  max-server-connections: 600
          max-fresh-time: 3d
   serialize-connections: no
       always-from-cache: no
          cache-hit-dscp: 4
              cache-path: usb1/proxy/cache  <-------
[admin@MikroTik] > file print
 # NAME                                                           TYPE
 0 skins                                                          directory
 5 usb1/proxy                                                     directory
 6 usb1/proxy/cache                                               web-proxy store   <-------
 7 usb1/lost+found                                                directory
```

Check if a cache is working: 

933 

```
[admin@MikroTik] > ip proxy monitor
                 status: running
                 uptime: 2w20h28m25s
     client-connections: 15
     server-connections: 7
               requests: 79772
                   hits: 30513
             cache-used: 481KiB
         total-ram-used: 1207KiB
  received-from-servers: 4042536KiB
        sent-to-clients: 4399757KiB
   hits-sent-to-clients: 176934KiB
```
