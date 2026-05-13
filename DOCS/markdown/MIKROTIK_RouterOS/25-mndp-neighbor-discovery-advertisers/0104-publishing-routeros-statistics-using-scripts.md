## Publishing RouterOS statistics using scripts 

You can also use scripts to structure MQTT messages that contain RouterOS statistics. Then, you can apply the scheduler to run the script whenever you like. 

For example, you can run a script like this (copy the content of the RouterOS code shown below into a new terminal and press "enter"): 

```
/system script add dont-require-permissions=no name=mqttpublish owner=admin policy=\
    ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon source="#\
    \_Required packages: iot\r\
    \n\r\
    \n################################ Configuration #########################\
    #######\r\
    \n# Name of an existing MQTT broker that should be used for publishing\r\
    \n:local broker \"broker\"\r\
    \n\r\
    \n# MQTT topic where the message should be published\r\
    \n:local topic \"my/test/topic\"\r\
    \n\r\
    \n#################################### System ############################\
    #######\r\
    \n:put (\"[*] Gathering system info...\")\r\
    \n:local cpuLoad [/system resource get cpu-load]\r\
    \n:local freeMemory [/system resource get free-memory]\r\
    \n:local usedMemory ([/system resource get total-memory] - \$freeMemory)\r\
    \n:local rosVersion [/system package get value-name=version \\\r\
    \n\A0 \A0 [/system package find where name ~ \"^routeros\"]]\r\
    \n:local model [/system routerboard get value-name=model]\r\
    \n:local serialNumber [/system routerboard get value-name=serial-number]\r\
    \n:local upTime [/system resource get uptime]\r\
    \n\r\
    \n#################################### MQTT ##############################\
    #######\r\
    \n:local message \\\r\
    \n\A0 \A0 \"{\\\"model\\\":\\\"\$model\\\",\\\r\
    \n\A0 \A0 \A0 \A0 \A0 \A0 \A0 \A0 \\\"sn\\\":\\\"\$serialNumber\\\",\\\r\
    \n\A0 \A0 \A0 \A0 \A0 \A0 \A0 \A0 \\\"ros\\\":\\\"\$rosVersion\\\",\\\r\
    \n\A0 \A0 \A0 \A0 \A0 \A0 \A0 \A0 \\\"cpu\\\":\$cpuLoad,\\\r\
    \n\A0 \A0 \A0 \A0 \A0 \A0 \A0 \A0 \\\"umem\\\":\$usedMemory,\\\r\
    \n\A0 \A0 \A0 \A0 \A0 \A0 \A0 \A0 \\\"fmem\\\":\$freeMemory,\\\r\
    \n\A0 \A0 \A0 \A0 \A0 \A0 \A0 \A0 \\\"uptime\\\":\\\"\$upTime\\\"}\"\r\
    \n\r\
    \n:log info \"\$message\";\r\
    \n:put (\"[*] Total message size: \$[:len \$message] bytes\")\r\
    \n:put (\"[*] Sending message to MQTT broker...\")\r\
    \n/iot mqtt publish broker=\$broker topic=\$topic message=\$message\r\
    \n:put (\"[*] Done\")"
```

The script collects the data from the RouterOS (model name, serial number, RouterOS version, current CPU, used memory, free memory, and uptime) and publishes the message (the data) to the broker in the JSON format: 

```
/system script run mqttpublish
[*] Gathering system info...
[*] Total message size: 125 bytes
[*] Sending message to MQTT broker...
```

```
[*] Done
```

You can subscribe to the topic to check the results: 

1644 

```
/iot mqtt subscriptions recv  print
```

```
 0 broker=broker topic="my/test/topic" data="{"model":"RB924i-2nD-BT5&BG77","sn":"E9C80EAEXXXX","ros":"7.9","
cpu":13,"umem":47476736,
     "fmem":19632128,"uptime":"02:21:18"}"
   time=2023-05-22 17:03:52
```

Do not forget to change the "Configuration" part of the script (topic and the broker) based on your settings. 

1645
