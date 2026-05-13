## Introduction 

Many RouterOS devices have GPS support. It allows RouterOS to determine the precise location of its GPS receiver. GPS coordinates will indicate the latitude and the longitude values (among other parameters) of the current position. 

Let's say, you have LTAP (or any other RouterOS device with GPS support) and you wish to track its location. You want the router to send this data to a server, where the data will be stored and integrated into a map, as it is more convenient to monitor. In this guide, we will showcase how you can do that. This scenario will utilize MQTT protocol communication with a platform called ThingsBoard. 

ThingsBoard has a cloud solution and different local installation options (on different OS). 

Since we've added a container feature, it became possible to also run the platform within the RouterOS. Meaning, you can build this scenario, solely on RouterOS units → devices with GPS support that you wish to track (for example, cars equipped with LTAPs → RouterOS devices that act as MQTT publishers ), and a ThingsBoard server run within a more powerful RouterOS device (like a CHR machine → RouterOS device that acts as an MQTT broker ). 

If you want to choose this route (container route), make sure to pick the devices that you plan on using as a "server" carefully, because this implementation can be heavy on RAM usage (it is suggested to have a device that has at least 2 GB RAM or 1 GB RAM with minimal load and is either ARM64 or AMD64 architecture).
