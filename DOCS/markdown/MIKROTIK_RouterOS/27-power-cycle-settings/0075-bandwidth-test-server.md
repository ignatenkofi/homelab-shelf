## Bandwidth Test Server 

```
Sub-menu: /tool bandwidth-server
```

**==> picture [390 x 99] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>allocate-udp-ports-from  (integer 1000..64000; Default: 2000 ) Beginning of UDP port range<br>authenticate  (yes | no; Default: yes ) Communicate only with authenticated clients<br>enabled  (yes | no; Default: yes ) Defines whether bandwidth server is enabled or not<br>max-sessions  (integer 1..1000; Default: 100 ) Maximal simultaneous test count<br>**----- End of picture text -----**<br>


Example 

Bandwidth Server: 

1755 

```
[admin@MikroTik] /tool bandwidth-server> print
                  enabled: yes
             authenticate: yes
  allocate-udp-ports-from: 2000
             max-sessions: 100
```

```
[admin@MikroTik] /tool bandwidth-server>
```
