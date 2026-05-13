## Simply run the command: 

```
/iot mqtt publish broker=kaaiot message="{\"test\":\"data\"}" topic="kp1/<app-version>/epmx/<token>/update/keys
/88"
```

, where you should change `<app-version>` (that you can check under the " Home>Devices management>Devices>Specific device " tab) and `<token>` (that you've generated after creating a device on the platform) to your respective values. 

You should be able to see that a new "Metadata" value appeared under " Home>Device management>Devices>Specific device>Overview " tab or check logs under " Home>Device management>Devices>Specific device>Data logs" tab. 

To collect `/system resource print` information and post it, we can use scripting. Copy and paste the content of the script show below into the command line: 

1649 

```
/system script
```

```
add dont-require-permissions=no name=systeminfo owner=admin policy=ftp,reboot,read,write,policy,test,password,
sniff,sensitive,romon source="#####\
    ############################### System ###################################\r\
    \n:put (\"[*] Gathering system info...\")\r\
    \n:local cpuLoad [/system resource get cpu-load];\r\
    \n:local freeMemory [/system resource get free-memory];\r\
    \n:local usedMemory ([/system resource get total-memory] - \$freeMemory);\r\
    \n:local rosVersion [/system package get value-name=version \\\r\
    \n[/system package find where name ~ \"^routeros\"]];\r\
    \n:local model [/system routerboard get value-name=model];\r\
    \n:local serialNumber [/system routerboard get value-name=serial-number];\r\
    \n:local upTime [/system resource get uptime];\r\
    \n\r\
    \n#################################### message #####################################\r\
    \n:local message \\\r\
    \n\"{\\\"model\\\":\\\"\$model\\\",\\\r\
    \n\\\"sn\\\":\\\"\$serialNumber\\\",\\\r\
    \n\\\"ros\\\":\\\"\$rosVersion\\\",\\\r\
    \n\\\"cpu\\\":\\\"\$cpuLoad\\\",\\\r\
    \n\\\"umem\\\":\\\"\$usedMemory\\\",\\\r\
    \n\\\"fmem\\\":\\\"\$freeMemory\\\",\\\r\
    \n\\\"uptime\\\":\\\"\$upTime\\\"}\"\r\
    \n\r\
    \n:log info \"\$message\";\r\
    \n:put (\"[*] Total message size: \$[:len \$message] bytes\")\r\
    \n:put (\"[*] Sending message...\")\r\
    \n/iot mqtt publish broker=kaaiot message=\$message topic=\"kp1/<app-version>/epmx/<token>/update/keys/88\"
\r\
    \n:put (\"[*] Done\")"
```

Change the topic's `<app-version>` and `<token>` values. Then, run the script using: 

```
/system script run systeminfo
```

The JSON message will look like this: 

```
{
  "model": "RB924iR-2nD-BT5&BG77",
  "sn": "XXXXXXX",
  "ros": "7.99",
  "cpu": "7",
  "umem": "45113344",
  "fmem": "21995520",
  "uptime": "4d22:16:08"
}
```
