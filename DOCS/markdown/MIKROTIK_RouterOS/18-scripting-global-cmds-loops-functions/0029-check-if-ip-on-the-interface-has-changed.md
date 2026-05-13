## Check if IP on the interface has changed 

Sometimes provider gives dynamic IP addresses. This script will compare if a dynamic IP address is changed. 

```
:global currentIP;
:local newIP [/ip address get [find interface="ether1"] address];
```

```
:if ($newIP != $currentIP) do={
    :put "ip address $currentIP changed to $newIP";
    :set currentIP $newIP;
}
```

1114
