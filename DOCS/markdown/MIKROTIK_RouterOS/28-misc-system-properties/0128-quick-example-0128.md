## Quick Example 

To make system generate a support output file and sent it automatically to support@example.com through the 192.0.2.1in case of a software crash: 

1842 

```
[admin@MikroTik] system/watchdog/ set auto-send-supout=yes \
\... send-to-email=support@example.com send-smtp-server=192.0.2.1
[admin@MikroTik] system watchdog> print
      watch-address: none
     watchdog-timer: yes
      no-ping-delay: 5m
   automatic-supout: yes
   auto-send-supout: yes
   send-smtp-server: 192.0.2.1
      send-email-to: support@example.com
```

1843
