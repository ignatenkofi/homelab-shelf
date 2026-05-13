## Introduction 

Bluetooth interface implementation in RouterOS allows the device to capture Bluetooth advertising packets that are broadcasted over 37, 38, and 39 advertising channels. More information can be found in the guide here. 

Bluetooth tags like, for example, TG-BT5-IN and TG-BT5-OUT, do exactly that. They broadcast advertising payloads over the mentioned channels. To understand what kind of information is stored in the payload, make sure to check the link. The tags can be configured (using the MikroTik Beacon Manager app) to broadcast the payloads automatically, with an interval or/and when a movement, tilt, or free-fall trigger is detected. In simple terms, the tag will "tell" (broadcast to) all the surrounding Bluetooth scanners (like the KNOT) information about itself periodically. 

When the payload is broadcasted by the tag, and the tag is within the KNOT's Bluetooth operating range, the KNOT will capture and display the payload under its "scanner" Bluetooth interface section. It would look like this: 

```
/iot bluetooth scanners advertisements print
Columns: DEVICE, PDU-TYPE, TIME, ADDRESS-TYPE, ADDRESS, RSSI, LENGTH, DATA
#  DEVICE  PDU-TYPE        TIME                  ADDRESS-TYPE  ADDRESS            RSSI    LENGTH
DATA
0  bt1     adv-noconn-ind  mar/07/2023 12:11:57  public        DC:2C:6E:0F:C0:3D  -51dBm      22
15ff4f09010079100000ffff0000cf188a6b2b000064
1  bt1     adv-noconn-ind  mar/07/2023 12:11:58  public        2C:C8:1B:4B:BB:0A  -49dBm      22
15ff4f090100168dfefffffffeffa51ae1362200005e
```

The example above shows us, that the KNOT sees two Bluetooth tags within its operating range with MAC addresses "DC:2C:6E:0F:C0:3D" and "2C:C8: 1B:4B:BB:0A", their respective payloads ("DATA" field) and the signal strength ("RSSI" field). 

1565 

**==> picture [13 x 13] intentionally omitted <==**

When testing locally to see how many payloads can the KNOT handle, we've achieved the following results →  with 300 tags (in factory settings), scattered around the KNOT and using a Bluetooth filter "keep-newest" (which overwrites previously received payloads for each unique MAC address with the newest one, so that the Bluetooth list would display 1 payload per 1 unique tag's MAC address at all times), all 300 MAC addresses appeared in the KNOT's range after 30-40 seconds. This is where you need to keep in mind that all 300 tags broadcasting over the same channels at the same time will cause interference (delay in the reception). When we "cleared" the Bluetooth payload list, each second the list got 20 new entries and after about ~15 seconds, the list had 250-290 payloads. Then after ~15 seconds more, the list displayed all 300 unique tag payloads. The actual number of tags your KNOT is able to handle is heavily dependent on the environment, so it is better to test it on sight. 

With the help of RouterOS scripting and scheduling, we can make the KNOT automatically-periodically scan the payload list and, in case, a specific payload or a specific tag's MAC address is found on the list, we can make the KNOT structure an MQTT message (out of the printed information shown in the example above) and send it to the configured server via MQTT, e-mail or HTTP post. Script examples will be shown later on in the guide. 

As the title suggests, the goal is to implement a Bluetooth tag-tracking solution and the idea is quite simple. When you have 2 KNOTs (KNOT-A and KNOTB), running the same script on a scheduler, and the tag moves between their Bluetooth operating ranges , the data on the server will indicate whether it was KNOT-A or KNOT-B that have sent the tag's payload . That will help you figure out the proximity of the tag. Whether the tag is broadcasting payloads in the KNOT-A zone, or in the KNOT-B zone. 

You will need a server where the data is going to be stored and visualized. In this guide, we will showcase a platform called ThingsBoard and how to communicate with it using the MQTT protocol. 

ThingsBoard has a cloud solution and different local installation options (on different OS). Since we've added a container feature, it became possible to also run the platform within RouterOS. In order to do that, you will need a RouterOS device that has at least 2 GB RAM to spare or 1 GB RAM to spare with minimal load, has the option to increase storage (for example, an additional USB port), and is either ARM64 or AMD64 architecture. Consider using C HR machine, as it could be a good fit.
