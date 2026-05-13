## Introduction 

The introduction of the container feature into the RouterOS made it possible to run all kinds of servers for all sorts of tasks inside the router. This is especially relevant for people, who want to reduce the number of devices in their network. Instead of running a server on a separate device/machine, why not run it inside the router? 

In this guide, we will showcase how to install a basic MQTT broker (or in other words, server) called eclipse-mosquitto. MQTT protocol is a very popular choice, especially in IoT topologies. It is an open OASIS and ISO standard lightweight, publish-subscribe network protocol that transports messages between devices. A typical topology consists of an MQTT publisher (a device that sends information), an MQTT broker (a server where the data is stored), and an MQTT subscriber (a device that listens to the data published on the server). 

RouterOS supports MQTT publish, subscribe feature, and, now, we can also run the MQTT broker as well. 

The image that we are going to use, can be found by following the hub.docker link.
