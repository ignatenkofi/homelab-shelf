## Introduction 

One of the many cloud services that you can use to monitor information that is sent by an MQTT publisher is Thingsboard. This article will demonstrate how to configure both Thingsboard and RouterOS to publish the data using the MQTT protocol. RouterOS, in this scenario, is going to act as a gateway and publish the data from the RouterBoard to the Thingsboard's server. Thingsboard, in this scenario, will act as an MQTT broker (server, where data will be posted). 

Before we proceed with the settings, you need to either: 

- a) Create an account in the Thingsboard's system. You can do so by following this link. This will allow you to use the ThingsBoard cloud solution for free for a limited/test time period. 

- b) Set up your own server by following the guide. There is a community edition that can be installed and used free of charge. 

**==> picture [13 x 13] intentionally omitted <==**

Please consider using SSL MQTT (TCP port 8883 and certificates) , instead of non-SSL MQTT (TCP port 1883). If you use non-SSL MQTT, the communication between the client (MQTT publisher) and the server (MQTT broker) can be easily sniffed/packet captured, and that will compromise authentication data (such as client-ids, usernames and passwords).
