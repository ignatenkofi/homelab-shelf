## RAM proxy cache: 

Important commands: 

max-cache-size= 

max-cache-object-size= cache-on-disk= 

932 

```
[admin@MikroTik] /ip proxy> set max-cache-size=unlimited max-cache-object-size=50000KiB cache-on-disk=no
...
[admin@MikroTik] /ip proxy> print
                 enabled: yes
             src-address: ::
                    port: 8080
               anonymous: no
            parent-proxy: 0.0.0.0
       parent-proxy-port: 0
     cache-administrator: webmaster
          max-cache-size: unlimited  <-------
   max-cache-object-size: 500000KiB  <-------
           cache-on-disk: no  <-------
  max-client-connections: 600
  max-server-connections: 600
          max-fresh-time: 3d
   serialize-connections: no
       always-from-cache: no
          cache-hit-dscp: 4
              cache-path: proxy-cache
```
