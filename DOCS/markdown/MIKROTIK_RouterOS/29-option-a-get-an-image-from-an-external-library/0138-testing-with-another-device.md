## Testing with another device 

When you have two RouterOS devices, one that is running the container (and, in our example, is the same device that generated the certificate) and the other one that you wish to test the MQTT connection from (let's say, an LTAP or any other RouterOS device with IoT package installed) → you will need to import the certificate to the second device. 

Drag and drop the exported certificate ( mqttserver.p12 ) into the device's "File List": 

```
[admin@LTAP] > /file/print
Columns: NAME, TYPE, SIZE, CREATION-TIME
#  NAME            TYPE       SIZE  CREATION-TIME
0  mqttserver.p12  .p12 file  2438  jan/30/2023 13:28:11
1  flash           disk             jul/06/2021 14:51:53
2  flash/pub       directory        jul/06/2021 14:51:53
3  flash/skins     directory        jan/01/1970 02:00:07
[admin@LTAP] >
```
