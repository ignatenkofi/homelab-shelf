## Sub-menu: `/iot lora traffic` 

**==> picture [516 x 279] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>options Allows to configure additional options for the traffic tab:<br>crc-errors (yes | no) → Set to "no" to discard packets that have "crc error" status from appear in the traffic tab;<br>pckt-limit (10...1024) → To limit traffic tab's log list.<br>clear  To clear the list (to remove all entries).<br>To view the list, use the  print  command:<br>[admin@MikroTik] /iot/lora/traffic/print<br>Columns: TIME, GWID, MSGTYPE, DEVADDR, MVER, FCNT, CRC, TYPE, JOINEUI, DEVEUI<br> #  TIME                             GWID  MSGTYPE                DEVADDR      MVER         FCNT  CRC    TY<br>JOINEUI                  DEVEUI<br> 0  2024-11-08 13:33:28  xxxxxxxxxxxxxxxx  Unconfirmed Data Up    6C B9 XX XX  LoRaWAN R1  59434  Error<br>Rx<br> 1  2024-11-08 13:33:50  xxxxxxxxxxxxxxxx  Rejoin-request                      LoRaWAN R1         Error<br>Rx                           50 62 9F FE XX XX XX XX<br> 2  2024-11-08 13:34:09  xxxxxxxxxxxxxxxx  Unconfirmed Data Down  5E 00 XX XX  RFU         41736  Error<br>Rx<br> 3  2024-11-08 13:34:15  xxxxxxxxxxxxxxxx  Rejoin-request                      RFU                Error<br>Rx                           D9 C2 BD 4B XX XX XX XX<br> 4  2024-11-08 13:34:55  xxxxxxxxxxxxxxxx  Join-request                        LoRaWAN R1         Error  Rx  A1<br>AE B1 8A XX XX XX XX  F4 62 81 BE XX XX XX XX<br>**----- End of picture text -----**<br>

To clear the list (to remove all entries), issue the `clear` command: 

```
[admin@MikroTik] /iot/lora/traffic/clear
```

Traffic tab displays "LoRa" payloads. As soon as the LoRa interface is enabled with the `/iot lora enable [find]` command, all the payloads from the list will be converted into TCP/UDP packets (depending on whether you use UDP 1700 or LNS/CUPS protocol) and forwarded to the configured server. 

If you do not wish to use LoRaWAN topology, and if you wish to forward "raw" LoRa payloads to your own server, you have an option to do so, using MQTT or Fetch post (HTTP post). To do that, remove the LoRa server configuration (so that no server is selected by the LoRa interface, thus the payloads are not forwarded anywhere) and then you will have to create a script. The script will have to store the traffic as variables, structure MQTT/HTTP messages out of them (in a format that your server expects to receive the data) and then send it. After that, you can apply a scheduler, to run the script with an interval of your choice to constantly send the data. 

A basic example (first step in the script) on how to convert traffic payloads into a varible called "traffic": 

```
[admin@MikroTik] > :global traffic;:set traffic [/iot lora traffic print as-value ];put $traffic
.id=*4f;band=125 kHz;coderate=?/?;counter=890652548;crc=Error;datarate=SF 7;freqhz=868300;gwid=50313xxxxxx;ifcha
in=1;mod=LoRa;msgtype=Proprietary;mver=RFU;rfchain=1;rssi=-116.00;rxcrc=3809;size=213;snr=-12.00;snrmax=-8.25;
snrmin=
```

```
-14.25;time=2024-11-08 14:39:45;type=Rx
```
