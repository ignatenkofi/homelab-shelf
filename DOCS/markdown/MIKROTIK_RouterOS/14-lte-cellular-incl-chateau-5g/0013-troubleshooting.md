## Troubleshooting 

Enable LTE logging: 

```
[admin@MikroTik] > /system logging add topics=lte
```

Check for errors in log: 

```
[admin@MikroTik] > /log print
```

```
11:08:59 lte,async lte1: sent AT+CPIN?
11:08:59 lte,async lte1: rcvd +CME ERROR: 10
```

search for CME error description online, 

in this case: CME error 10 - SIM not inserted
