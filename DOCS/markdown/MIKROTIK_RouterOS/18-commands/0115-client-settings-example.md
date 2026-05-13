## Client settings example: 

To check the status of the NTP client in CLI, use the "print" command 

```
[admin@ntp-example_v6] > /system ntp client print
           enabled: no
       primary-ntp: 0.0.0.0
     secondary-ntp: 0.0.0.0
  server-dns-names:
              mode: unicast
```

To enable the NTP client and set IP addresses or FQDN of the NTP servers: 

```
[admin@ntp-example_v6] > /system ntp client set enabled=yes
[admin@ntp-example_v6] > /system ntp client print
             enabled: yes
         primary-ntp: 0.0.0.0
       secondary-ntp: 0.0.0.0
    server-dns-names:
                mode: unicast
     dynamic-servers: x.x.x.x, x.x.x.x
       poll-interval: 15s
       active-server: x.x.x.x
    last-update-from: x.x.x.x
  last-update-before: 6s570ms
     last-adjustment: -1ms786us
[admin@ntp-example_v6] > /system ntp client set primary-ntp=162.159.200.123
[admin@ntp-example_v6] > /system ntp client print
           enabled: yes
       primary-ntp: 162.159.200.123
     secondary-ntp: 0.0.0.0
  server-dns-names:
              mode: unicast
   dynamic-servers: x.x.x.x, x.x.x.x
     poll-interval: 16s
     active-server: x.x.x.x
```
