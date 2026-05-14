## MQTT publish 

You can test MQTT publish with a static message by using the command: 

804 

```
/iot/mqtt/publish broker="tb" topic="v1/devices/me/telemetry" message="{\"test\":\"123\"}"
```

To post GPS coordinates, import the script shown below: 

```
/system/script/add dont-require-permissions=no name=mqttgps owner=admin policy="ftp,re\
    boot,read,write,policy,test,password,sniff,sensitive,romon" \
    source="    ###Configuration###\r\
    \n    #Enter pre-configured broker's name within \"\":\r\
    \n    :local broker \"tb\"\r\
    \n    #Enter the topic name within \"\", per the broker's config\
    uration:\r\
    \n    :local topic \"v1/devices/me/telemetry\"\r\
    \n\r\
    \n    ###Variables####\r\
    \n    :global lat\r\
    \n    :global lon\r\
    \n    :global alt1\r\
    \n    :global alt2\r\
    \n\r\
    \n    ###GPS####\r\
    \n    :put (\"[*] Capturing GPS coordinates...\")\r\
    \n    /system gps monitor once do={\r\
    \n    :set \$lat \$(\"latitude\");\r\
    \n    :set \$lon \$(\"longitude\");\r\
    \n    :set \$alt1 \$(\"altitude\")}\r\
    \n    ###remove \"meters\" from the value because JSON format wi\
    ll not understand it###\r\
    \n    :set \$alt2 [:pick \$alt1 0 [find \$alt1 \" m\"]]\r\
    \n\r\
    \n    :local message \\\r\
    \n    \"{\\\"latitude\\\":\$lat,\\\r\
    \n    \\\"longitude\\\":\$lon,\\\r\
    \n    \\\"altitude\\\":\$alt2}\"\r\
    \n\r\
    \n    ###MQTT###\r\
    \n    :if (\$lat != \"none\") do={\\\r\
    \n    :put (\"[*] Sending message to MQTT broker...\");\r\
    \n    /iot mqtt publish broker=\$broker topic=\$topic message=\$\
    message} else={:put (\"[*] Lattitude=none, not posting anything!\
    \");:log info \"Latitude=none, not posting anything!\"}"
```

In short, the script captures GPS information, specifically the latitude, longitude, and altitude values. Then it structures a JSON message out of them. In case, at the moment when the script is initiated, the latitude value equals anything other than "none" (equals any actual value-number) → it sends the JSON message via MQTT to the broker named " tb ". In case, the GPS data can not be captured →  "latitude" is recognized as "none" →  the script just logs that nothing could be captured and does nothing else. 

This is a very basic example. Feel free to alter the script and add your own "if" (maybe an email notification if there is no GPS signal) and additional parameters (any other RouterOS captured value, like, maybe, its firmware version) per your requirements. 

Run the script with the command: 

805 

```
/system/script/run mqttgps
[*] Capturing GPS coordinates...
        date-and-time: feb/01/2023 10:39:37
             latitude: 56.969862
            longitude: 24.162425
             altitude: 31.799999 m
                speed: 1.000080 km/h
  destination-bearing: none
         true-bearing: 153.089996 deg. True
     magnetic-bearing: 0.000000 deg. Mag
                valid: yes
           satellites: 6
          fix-quality: 1
  horizontal-dilution: 1.42
             data-age: 0s
[*] Sending message to MQTT broker...
```

To automate the process, add a scheduler (to run the script, for example, every 30 seconds): 

```
/system/scheduler/add name=mqttgpsscheduler interval=30s on-event="/system/script/run mqttgps"
```
