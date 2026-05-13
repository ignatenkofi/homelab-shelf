## To enable bandwidth-test server without client authentication: 

```
[admin@MikroTik] /tool bandwidth-server> set enabled=yes authenticate=no
[admin@MikroTik] /tool bandwidth-server> print
                  enabled: yes
             authenticate: no
  allocate-udp-ports-from: 2000
             max-sessions: 100
```

```
[admin@MikroTik] /tool bandwidth-server>
```
