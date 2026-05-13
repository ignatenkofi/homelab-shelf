## Script 

Import the script shown below to each KNOT. To do that, just copy the below shown "code" and paste it into a new terminal window and press "ENTER": 

```
/system script add dont-require-permissions=no name=tracking owner=admin policy=\
    ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon source="# Requ\
    ired packages: iot\r\
    \n\r\
    \n################################ Configuration ##############################\
    ##\r\
    \n# Name of an existing MQTT broker that should be used for publishing\r\
    \n:local broker \"tb\"\r\
    \n\r\
    \n# MQTT topic where the message should be published\r\
    \n:local topic \"v1/gateway/telemetry\"\r\
    \n\r\
    \n# POSIX regex for filtering advertisement Bluetooth addresses. E.g. \"^BC:33:\
    AC\"\r\
    \n# would only include addresses which start with those 3 octets.\r\
    \n# To disable this filter, set it to \"\"\r\
    \n:local addressRegex \"\"\r\
    \n\r\
    \n# POSIX regex for filtering Bluetooth advertisements based on their data. Sam\
    e\r\
    \n# usage as with 'addressRegex'.\r\
    \n:local advertisingDataRegex \"\"\r\
    \n\r\
    \n# Signal strength filter. E.g. -40 would only include Bluetooth advertisement\
    s\r\
    \n# whose signal strength is stronger than -40dBm.\r\
    \n# To disable this filter, set it to \"\"\r\
    \n:local rssiThreshold \"\"\r\
    \n\r\
    \n#Name the KNOT. Identity of the unit that will be senting the message. This n\
    ame will be reported to the MQTT broker.\r\
    \n:local gwName \"KNOT_A\"\r\
    \n\r\
    \n################################## Bluetooth ################################\
    ##\r\
    \n:put (\"[*] Gathering Bluetooth info...\")\r\
    \n\r\
    \n:global makeRecord do={\r\
    \n    :local jsonStr \"{\\\"ts\\\":\$ts,\\\"values\\\":{\\\"reporter\\\":\\\"\$\
    gwName\\\",\\\"rssi\\\":\$rssi}}\"\r\
    \n    :return \$jsonStr\r\
    \n}   \r\
    \n\r\
    \n# array of record strings collected for each advertising MAC address\r\
    \n:global macRecords [:toarray \"\"]\r\
    \n\r\
    \n# process advertisements and update macRecords\r\
    \n:local advertisements [/iot bluetooth scanners advertisements print detail as\
    -value where \\\r\
    \naddress ~ \$addressRegex and \\\r\
    \ndata ~ \$advertisingDataRegex and \\\r\
    \nrssi > \$rssiThreshold]\r\
    \n\r\
    \n/iot/bluetooth/scanners/advertisements clear\r\
    \n\r\
    \n:foreach adv in=\$advertisements do={\r\
```

1570 

```
    \n:local address (\$adv->\"address\")\r\
    \n:local rssi (\$adv->\"rssi\")\r\
    \n:local epoch (\$adv->\"epoch\")\r\
    \n                \r\
    \n:local recordStr [\$makeRecord ts=\$epoch gwName=\$gwName rssi=\$rssi]\r\
    \n\r\
    \n:if ([:len (\$macRecords->\$address)] > 0) do={\r\
    \n:local str (\$macRecords->\$address)\r\
    \n:local newStr \"\$str,\$recordStr\"\r\
    \n:set (\$macRecords->\$address) \$newStr} else={:set (\$macRecords->\$address)\
    \_\$recordStr}}\r\
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
    \n:put (\"[*] Total message size: \$[:len \$message] bytes\")\r\
    \n:put (\"[*] Sending message to MQTT broker...\")\r\
    \n/iot mqtt publish broker=\"\$broker\" topic=\"\$topic\" message=\$message}"
```

The script should appear under the "System>Scripts>Script List" tab with the name "tracking" or with the help of the command " `/system script print` ". 

There are certain script lines that you need to pay attention to. 

Broker name configuration line, where you need to input the MQTT broker name that you have set: 

:local broker "tb" 

You need to input a correct topic, used by the MQTT broker. Check ThingsBoard documentation for more details and, by default, the topic should be: 

:local topic "v1/gateway/telemetry" 

MAC address filtering option inside the script itself. You can type in all 6 octets of the MAC address (to apply the filter to 1 specific tag), or you can filter the list using a few/couple of octets, like "^BC:33:AC" (to apply the filter, so that only MAC addresses that begin with "BC:33:AC:..." would be processed): 

:local addressRegex "DC:2C:6E:0F:C0:3D" 

Payload content/data line. Allows you to filter the list, per specific payload content, like "manufacturer data". For example, "15ff4f09" would discard all payloads that are not MikroTik format payloads: 

:local advertisingDataRegex "15ff4f09" 

RSSI signal strength filtering option. This filtering option was mentioned in the "Scenario explanation" section. This filter allows you to ignore any payload that has RSSI weaker than the configured value. For example. "-40" would only include Bluetooth advertisements that have signal strength stronger than -40dBm: 

:local rssiThreshold "-40" 

1571 

KNOT identifier line. You will need to change it for each unique KNOT. For example, name your first KNOT →  KNOT_A and your second KNOT →  KNOT_B: 

:local gwName "KNOT_A" 

The rest of the script does not need to be changed/altered 

How does the script work when you run it? The script "inspects" the "Advertising reports" tab (payload list tab) using the filters applied and structures a JSON message. An example of the JSON message would be: 

```
{
 "2C:C8:1B:4B:BB:0A": [
   {
     "ts": 1678967250600,
     "values": {
       "reporter": "KNOT_A",
       "rssi": -47
     }
   }
 ],
 "DC:2C:6E:0F:C0:3D": [
   {
     "ts": 1678967247850,
     "values": {
       "reporter": "KNOT_A",
       "rssi": -59
     }
   },
   {
     "ts": 1678967257849,
     "values": {
       "reporter": "KNOT_A",
       "rssi": -67
     }
   }
 ]
}
```

The data is structured per the ThingsBoard guide, where " `2C:C8:1B:4B:BB:0A` " and " `DC:2C:6E:0F:C0:3D` " are MAC addresses of tags that appeared in the KNOT's range, " `ts` " is unix timestamp of each payload broadcasted by the tag in milliseconds, " `reporter` " indicates which specific KNOT has sent the message and " `rssi` " is the signal strength of each payload broadcasted by the tag in dBm. 

After the payload list is "searched" and the JSON message is structured, the Bluetooth interface payload list gets "cleaned" (or "flashed"), and the previously structured JSON message is sent to the ThingsBoard MQTT broker. 

To run the script, use the command: 

```
/system script run tracking
```
