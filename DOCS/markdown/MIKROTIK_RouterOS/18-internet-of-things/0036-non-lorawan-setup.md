## Non-LoRaWAN setup 

However, if you do not wish to use a LoRaWAN network/topology, and you wish to forward "raw LoRa" payloads to your own server, you have an option to do so. You can use MQTT or HTTP post to forward received payloads to your MQTT/HTTP server, but it will require additional scripting. The script will have to collect information (payloads) from the `IoT>LoRa>Traffic` tab, store those payloads as variables, structure MQTT/HTTP message out of the variables and post it. 

**==> picture [13 x 13] intentionally omitted <==**

Please note that if the payloads broadcasted by the node are encrypted, and you wish to forward them to your own MQTT/HTTP server (without using LoRaWAN), you will need to decipher the payloads on the server-side. The gateway does not have the built-in functionality to decipher node's data. Servers are responsible for this task. 

Also, there is no option to "relay" downlink MQTT/HTTP messages back from the MQTT/HTTP server to the LoRa node (only "uplink" payloads from the nodes can be "forwarded" to the server). Primarily, because there is no way to "make" LR cards "broadcast" custom payloads (there is no way to pass the content of the MQTT/HTTP downlink message into the LoRa chip). 

1598
