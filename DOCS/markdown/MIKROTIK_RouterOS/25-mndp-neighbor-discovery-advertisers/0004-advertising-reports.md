## Advertising reports 

In this section, it is possible to monitor Bluetooth advertising reports (from the nearby broadcasters). The list is limited to 1024 entries (if the list gets full with 1024 entries, each new payload received will overwrite the "oldest" one). You can monitor advertising reports with the command: 

```
/iot bluetooth scanners advertisements print
```

```
Columns: DEVICE, PDU-TYPE, TIME, ADDRESS-TYPE, ADDRESS, RSSI
```

```
 #  DEV  PDU-TYPE        TIME                  ADDRES  ADDRESS            RSSI
 0  bt1  adv-noconn-ind  jul/28/2021 09:30:56  public  2C:C8:1B:93:16:49  -24dBm
 1  bt1  adv-noconn-ind  jul/28/2021 09:30:56  random  0B:16:17:9E:7B:EF  -60dBm
```

It is possible to set up a filter for the reports with the command: 

```
/iot bluetooth scanners advertisements print where
```

For example, to print reports that are broadcasted by a specific Bluetooth address, use the command: 

```
/iot bluetooth scanners advertisements print where address=XX:XX:XX:XX:XX:XX
```

```
 # DEVICE    PDU-TYPE       TIME                 ADD... ADDRESS                    RSSI     LENGTH DATA
79 bt1       adv-noconn-ind jul/28/2021 09:46:38 public XX:XX:XX:XX:XX:XX        -70dBm         30 02010...
80 bt1       adv-noconn-ind jul/28/2021 09:46:43 public XX:XX:XX:XX:XX:XX        -67dBm         30 02010...
81 bt1       adv-noconn-ind jul/28/2021 09:46:44 public XX:XX:XX:XX:XX:XX        -70dBm         28 1bff0...
82 bt1       adv-noconn-ind jul/28/2021 09:46:48 public XX:XX:XX:XX:XX:XX        -75dBm         30 02010...
```

To show only advertising reports that have RSSI stronger than -30 dBm, use the command: 

```
/iot bluetooth scanners advertisements print where rssi > -30
```

```
 # DEVICE         PDU-TYPE       TIME                 ADDRESS-TYPE ADDRESS                    RSSI     LENGTH
DATA
307 bt1            adv-noconn-ind jul/29/2021 10:11:31 public       2C:C8:1B:93:16:49        -24dBm         22
15ff4f09.>
```

```
308 bt1            adv-noconn-ind jul/29/2021 10:11:31 public       2C:C8:1B:93:16:49        -26dBm         22
15ff4f09.>
```

Possible filters (you can filter the list of advertising reports with the help of the following parameters): 

**==> picture [300 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Filter Description<br>address Bluetooth advertisers address<br>address-type Advertisers address type (for example, public or random)<br>data Advertisement data in hex format (AdvData payload)<br>**----- End of picture text -----**<br>


1560 

**==> picture [300 x 133] intentionally omitted <==**

**----- Start of picture text -----**<br>
device Bluetooth chip/interface name<br>epoch Milliseconds since Unix Epoch<br>filter-comment Comment of the matching whitelist filter<br>length Advertisement data length<br>pdu-type Advertisement PDU type<br>rssi Signal strength<br>time Time of the advertisement packet reception<br>**----- End of picture text -----**<br>
