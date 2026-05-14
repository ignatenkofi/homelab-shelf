## Upgrade license level using the command-line interface 

```
[admin@MikroTik] > /system license print
  system-id: 6lR1ZP/utuJ
      level: free
[admin@MikroTik] > /system/license/renew
account: mymikrotikcomaccount
password: *********************
level: p1
  status: done
[admin@MikroTik] > /system/license/print
         system-id: 6lR1ZP/utuJ
             level: p1
  limited-upgrades: no
   next-renewal-at: 2024-08-25 13:18:06
       deadline-at: 2024-09-24 13:18:06
```
