## Introduction 

The introduction of the container feature into the RouterOS made it possible to run all kinds of servers for all sorts of tasks inside the router. This is especially relevant for people, who want to reduce the number of devices in their network. Instead of running a server on a separate device/machine, why not run it inside the router? 

A lot of users need a server that is able to gather the data, store it and display it in a way it is easy to understand. This is where a platform like ThingsBoard can come into play. 

It is primarily positioned as an IoT platform and you can find all sorts of use cases for it that they demonstrate in the 

link. 

The most appealing part, from the RouterOS user standpoint, is that it can be used as an MQTT server (MQTT broker) or an HTTP server. Meaning, you can use MQTT publish or HTTP post to post the data. You can find ThingsBoard MQTT API guide by using the link here and HTTP API by using the link he re. 

In short, you can utilize scripting to collect RouterOS statistics (like uptime, GPS coordinates, packet statistics, and almost anything else that you print into the terminal), then store this information into variables and structure a JSON message out of those. You can, then send this message using MQTT or HTTP post to the ThingsBoard via a scheduler (that will run this script whenever you need it). You can find an example of a basic script that does it in this guide. 

ThingsBoard will store and display the data with the help of widgets, which can be used to help you set up dashboards that visualize the data in graphs, tables, maps, and other ways. 

For example, there are 2 below mentioned options of the ThingsBoard instances available and each of them uses a different database: 

thingsboard/tb-postgres thingsboard/tb-cassandra 

You can find more information in the ThingsBoard/docker documentation. 

In our example, we will showcase tb-postgres - a single instance of ThingsBoard with PostgreSQL database for testing purposes. 

The guide will showcase "in-memory" queue type service, but for production environment, consider using other service types. You can find more information here.
