## 6.  Start HAProxy Container: 

```
/container start [find where name=haproxy]
```

7.  Setup a schedule, for example, each day at 06:30 to check for a new certificate: 

```
/system scheduler
add interval=1d name=SCHEDULE_RenewCertbot on-event=SCRIPT_RenewCertbot policy=ftp,reboot,read,write,
policy,test,password,sniff,sensitive,romon start-date=\
    2025-03-10 start-time=06:30:00
/system script
add dont-require-permissions=no name=SCRIPT_RenewCertbot owner=admin policy=ftp,reboot,read,write,policy,
test,password,sniff,sensitive,romon source=\
    "/container/start [find where name=\"certbot\"]"
```
