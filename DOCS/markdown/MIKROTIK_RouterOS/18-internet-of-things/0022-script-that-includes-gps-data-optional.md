## Script that includes GPS data (optional) 

In case you also wish to include GPS data (longitude and latitude values from the KNOTs), use the script shown below: 

```
/system script add dont-require-permissions=no name=tracking+gps+temp owner=admin policy=\
    ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon source="# Required package\
    s: iot\r\
    \n\r\
    \n################################ Configuration ################################\r\
    \n# Name of an existing MQTT broker that should be used for publishing\r\
    \n:local broker \"tb\"\r\
    \n\r\
    \n# MQTT topic where the message should be published\r\
    \n:local topic \"v1/gateway/telemetry\"\r\
    \n:local gwtopic \"v1/devices/me/telemetry\"\r\
    \n\r\
    \n# POSIX regex for filtering advertisement Bluetooth addresses. E.g. \"^BC:33:AC\"\r\
    \n# would only include addresses which start with those 3 octets.\r\
    \n# To disable this filter, set it to \"\"\r\
    \n:local addressRegex \"\"\r\
```

1584 

```
    \n\r\
    \n# POSIX regex for filtering Bluetooth advertisements based on their data. Same\r\
    \n# usage as with 'addressRegex'.\r\
    \n:local advertisingDataRegex \"15ff\"\r\
    \n\r\
    \n# Signal strength filter. E.g. -40 would only include Bluetooth advertisements\r\
    \n# whose signal strength is stronger than -40dBm.\r\
    \n# To disable this filter, set it to \"\"\r\
    \n:local rssiThreshold \"\"\r\
    \n\r\
    \n#Name the KNOT. Identity of the unit that will be senting the message. This name will be \
    reported to the MQTT broker.\r\
    \n:local gwName \"2\"\r\
    \n\r\
    \n###########GPS#############\r\
    \n:global lat\r\
    \n:global lon\r\
    \n\r\
    \n/interface ppp-client set ppp-out1 disabled=yes\r\
    \n:log info (\"disabling WWAN to get GPS coordinates\")\r\
    \n\r\
    \n/interface ppp-client at-chat ppp-out1 input=\"AT+QGPSCFG=\\\"priority\\\",0\"\r\
    \n:log info (\"enabling priority for GPS\")\r\
    \n\r\
    \n###the time in the delay below is the time that the device will wait for to get the coord\
    inate fix\r\
    \n:delay 32000ms\r\
    \n:log info (\"reading GPS coordinates\")\r\
    \n/system gps monitor once do={\r\
    \n:set \$lat \$(\"latitude\")\r\
    \n:set \$lon \$(\"longitude\")\r\
    \n}\r\
    \n:if (\$lat != \"none\") do={\\\r\
    \n:log info (\"enabling priority back to WWAN\")\r\
    \n/interface ppp-client at-chat ppp-out1 input=\"AT+QGPSCFG=\\\"priority\\\",1\"\r\
    \n:log info (\"enabling WWAN\")\r\
    \n/interface ppp-client set ppp-out1 disabled=no\r\
    \n:delay 1000ms\r\
    \n###if dial on demand is enabled\r\
    \n/ping 1.1.1.1 count=1\r\
    \n\r\
    \n#the delay below waits for 5 seconds for the ppp connection to get established - this tim\
    e can differ based on the signal strength\r\
    \n:delay 5000ms\r\
    \n:log info (\"posting coordinates via mqtt\")\r\
    \n:local gpsmessage \\\r\
    \n    \"{\\\"latitude\\\":\$lat,\\\r\
    \n    \\\"longitude\\\":\$lon}\"\r\
    \n/iot mqtt publish broker=\$broker topic=\$gwtopic message=\$gpsmessage} else={\\\r\
    \n:log info (\"could not read GPS coordinates...enabling back WWAN\")\r\
    \n/interface ppp-client at-chat ppp-out1 input=\"AT+QGPSCFG=\\\"priority\\\",1\"\r\
    \n/interface ppp-client set ppp-out1 disabled=no\r\
    \n:delay 1000ms\r\
    \n###if dial on demand is enabled\r\
    \n/ping 1.1.1.1 count=1\r\
    \n:delay 5000ms\r\
    \n}\r\
    \n\r\
    \n##################################Bluetooth##################################\r\
    \n:global invertU16 do={\r\
    \n    :local inverted 0\r\
    \n    :for idx from=0 to=15 step=1 do={\r\
    \n        :local mask (1 << \$idx)\r\
    \n        :if (\$1 & \$mask = 0) do={\r\
    \n            :set \$inverted (\$inverted | \$mask)\r\
    \n        }\r\
    \n    }\r\
    \n    return \$inverted\r\
    \n}\r\
    \n\r\
    \n:global le16ToHost do={\r\
```

1585 

```
    \n    :local lsb [:pick \$1 0 2]\r\
    \n    :local msb [:pick \$1 2 4]\r\
    \n\r\
    \n    :return [:tonum \"0x\$msb\$lsb\"]\r\
    \n}\r\
    \n:local from88 do={\r\
    \n    :global invertU16\r\
    \n    :global le16ToHost\r\
    \n    :local num [\$le16ToHost \$1]\r\
    \n\r\
    \n    # Handle negative numbers\r\
    \n    :if (\$num & 0x8000) do={\r\
    \n        :set num (-1 * ([\$invertU16 \$num] + 1))\r\
    \n    }\r\
    \n\r\
    \n    # Convert from 8.8. Scale by 1000 since floating point is not supported\r\
    \n    :return ((\$num * 125) / 32)\r\
    \n}\r\
    \n:put (\"[*] Gathering Bluetooth info...\")\r\
    \n\r\
    \n:global makeRecord do={\r\
    \n    :local jsonStr \"{\\\"ts\\\":\$ts,\\\"values\\\":{\\\"KNOT_\$gwName\\\":\\\"\$gwName\
    \\\",\\\"temp\\\":\$temp}}\"\r\
    \n    :return \$jsonStr\r\
    \n}   \r\
    \n\r\
    \n# array of record strings collected for each advertising MAC address\r\
    \n:global macRecords [:toarray \"\"]\r\
    \n\r\
    \n# process advertisements and update macRecords\r\
    \n:local advertisements [/iot bluetooth scanners advertisements print detail as-value where\
    \_\\\r\
    \naddress ~ \$addressRegex and \\\r\
    \ndata ~ \$advertisingDataRegex and \\\r\
    \nrssi > \$rssiThreshold]\r\
    \n\r\
    \n/iot/bluetooth/scanners/advertisements clear\r\
    \n\r\
    \n:foreach adv in=\$advertisements do={\r\
    \n:local address (\$adv->\"address\")\r\
    \n:local ad (\$adv->\"data\")\r\
    \n:local rssi (\$adv->\"rssi\")\r\
    \n:local epoch (\$adv->\"epoch\")\r\
    \n:local temp [\$from88 [:pick \$ad 28 32]]\r\
    \n                \r\
    \n:local recordStr [\$makeRecord ts=\$epoch gwName=\$gwName temp=\$temp]\r\
    \n\r\
    \n:if ([:len (\$macRecords->\$address)] > 0) do={\r\
    \n:local str (\$macRecords->\$address)\r\
    \n:local newStr \"\$str,\$recordStr\"\r\
    \n:set (\$macRecords->\$address) \$newStr} else={:set (\$macRecords->\$address) \$recordStr\
    }}\r\
    \n\r\
    \n# TODO: add some logic to decide when we want to send data\r\
    \n:local sendData true\r\
    \n\r\
    \n:if (\$sendData) do={\r\
    \n:local jsonStr \"{\"\r\
    \n\r\
    \n:foreach addr,advRec in=\$macRecords do={\r\
    \n:set jsonStr \"\$jsonStr\\\"\$addr\\\":[\$advRec],\"}\r\
    \n\r\
    \n:local payloadlength\r\
    \n:set payloadlength [:len (\$jsonStr)]\r\
    \n:local remcom\r\
    \n:set remcom [:pick \$jsonStr 0 (\$payloadlength-1)]\r\
    \n:set jsonStr \"\$remcom}\"\r\
    \n:local message\r\
    \n:set message \"\$jsonStr\"\r\
    \n:log info \"\$message\";\r\
    \n:put (\"[*] Message structured: \$message\")\r\
```

1586 

```
    \n:put (\"[*] Total message size: \$[:len \$message] bytes\")\r\
```

```
    \n:put (\"[*] Sending message to MQTT broker...\")\r\
```

```
    \n/iot mqtt publish broker=\"\$broker\" topic=\"\$topic\" message=\$message}"
```

This is where you need to keep in mind the BG77 modem behavior → BG77 cellular modem (used in the KNOT) can not be used to have a cellular CAT-M /NB-IoT ongoing connection and to obtain GPS coordinates at the same time. 

When the script is run: 

- PPP interface is disabled and the highest priority is set for GPS reception (while the cellular PPP interface is down) for 32 seconds (this time can be altered in the script); 

- (a) If the device managed to obtain GPS latitude value during the configured 32 seconds (if the value obtained equals anything other than 

- "none"), the script will structure a JSON message with captured latitude and longitude values, the script will set the highest priority for WWAN (change the priority from GPS to WWAN) and enable PPP interface back (for internet access). After that, the script will send GPS data JSON message via the first MQTT publish and, the script will run the Bluetooth part, where the Bluetooth data JSON message is structured and sent via the second MQTT publish (x2 MQTT messages are sent → GPS data MQTT message and Bluetooth data MQTT message); 

- (b) If the device fails to obtain GPS latitude value during the 32-second interval (if the value obtained equals "none"), the script sets the highest priority for WWAN (changes the priority from GPS to WWAN), enables PPP interface back (for internet access) and just processes the Bluetooth part, where the Bluetooth data JSON message is structured and sent via MQTT publish (basically, if GPS data could not be obtained, x1 MQTT message with Bluetooth data is sent).
