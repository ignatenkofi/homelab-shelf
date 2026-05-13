## Summary 

MQTT is an open OASIS and ISO standard lightweight, publish-subscribe network protocol that transports messages between devices. A typical MQTT communication topology consists of: 

an MQTT publisher → a device that sends information to the server; an MQTT broker → a server where the data is stored; 

an MQTT subscriber → a device that reads/monitors the data published on the server. 

RouterOS can act as an MQTT publisher and subscriber (starting with 7.11beta2 ). You can also run an MQTT broker/server via the container feature. For Mosquitto MQTT broker configuration visit the link here. 

You can find application examples for MQTT publish scenarios below: 

a) MQTT/HTTPS example with AWS cloud platform 

b) MQTT example with Azure cloud platform 

c) MQTT and ThingsBoard configuration 

Please note that AWS and Azure examples (scripts) showcase publishing Bluetooth tag data. Currently, only the KNOT has a Bluetooth chip built-in.
