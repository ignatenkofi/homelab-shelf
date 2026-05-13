## Application example 

With the following example we will restrict access for Peter's mobile phone: 

Disabled internet access on Monday, Wednesday and Friday Allowed unlimited internet access on: 

Tuesday Thursday from 11:00-22:00 Sunday 15:00-22:00 Limited bandwidth to 3Mbps for Peter's mobile phone on Saturday from 18:30-21:00 

748 

```
[admin@MikroTik] > /ip kid-control add name=Peter mon="" tur-tue="00:00-24h" wed="" tur-thu="11:00-22:00"
fri="" sat="18:30-22:00" tur-sun="15h-21h" rate-limit=3M
```

```
[admin@MikroTik] > /ip kid-control device add name=Mobile-phone user=Peter mac-address=FF:FF:FF:ED:83:63
```

Internet access limitation is implemented by adding dynamic firewall filter rules or simple queue rules. Here are example firewall filter rules: 

```
[admin@MikroTik] > /ip firewall filter print
```
