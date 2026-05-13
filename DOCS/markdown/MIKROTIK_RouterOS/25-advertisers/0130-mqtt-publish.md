## MQTT Publish 

a) A quick MQTT publish test with a static value: 

```
/iot/mqtt/publish broker="tb" topic="v1/devices/me/telemetry" message="{\"cpu\":\"7\"}"
```

b) In order to publish relevant data from the RouterOS to the Thingsboard, you can use the script shown below as a reference. The script collects the data from the RouterOS device (model name, serial number, RouterOS version, current CPU, used memory, free memory, and uptime) and publishes the message (the data) to the broker in the JSON format: 

# Required packages: iot 

################################ Configuration ################################ # Name of an existing MQTT broker that should be used for publishing :local broker "tb" # MQTT topic where the message should be published :local topic "v1/devices/me/telemetry" #################################### System ################################### :put ("[*] Gathering system info...") :local cpuLoad [/system resource get cpu-load] :local freeMemory [/system resource get free-memory] :local usedMemory ([/system resource get total-memory] - $freeMemory) :local rosVersion [/system package get value-name=version \ [/system package find where name ~ "^routeros"]] :local model [/system routerboard get value-name=model] :local serialNumber [/system routerboard get value-name=serial-number] :local upTime [/system resource get uptime] #################################### MQTT ##################################### :local message \ "{\"model\":\"$model\",\ \"sn\":\"$serialNumber\",\ \"ros\":\"$rosVersion\",\ \"cpu\":$cpuLoad,\ \"umem\":$usedMemory,\ \"fmem\":$freeMemory,\ \"uptime\":\"$upTime\"}" :log info "$message"; :put ("[*] Total message size: $[:len $message] bytes") :put ("[*] Sending message to MQTT broker...") /iot mqtt publish broker=$broker topic=$topic message=$message :put ("[*] Done") 

2 script lines should be taken into account. 

1657 

:local broker "tb" 

line, where you should specify the broker's name within the quotation marks "". 

:local topic "v1/devices/me/telemetry" 

line, where you should specify the correct topic within the quotation marks "" (check Thingsboard's documentation for the exact topic that needs to be used). 

The rest of the script configuration depends on the overall requirements. 

Copy and paste the above script into a notepad, and re-copy it again. Navigate to System>Scripts menu, add a new script there, and paste the script that is shown above. Name it, for example, script1. 

To run the script, you can use the command line: 

```
/system script run script1
```
