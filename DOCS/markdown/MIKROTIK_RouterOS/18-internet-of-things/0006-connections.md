## Connections 

**==> picture [13 x 13] intentionally omitted <==**

Availible starting with v 7.12beta9 . 

**==> picture [516 x 302] intentionally omitted <==**

**----- Start of picture text -----**<br>
Currenetly, only " central " role is supported. " Pheriperal device " role, "p airing " and " encryption " options are not supported.<br>Availible sections are:<br>Section Description<br>async-data used to view subscribed data.<br>characteristics used to view all supported characteristics of the device.<br>connect used to connect to the device that is in the  connactable  state.<br>disconnect used to disconnect from the device.<br>read used to read characteristics values.<br>write used to write characteristics values.<br>subscribe used to subscribe to a charasteristic value.<br>unsubscribe used to unsubscribe from a charasteristic value.<br>In order to connect to a Bluetooth device that is in the  connactable  state, use the command (where  pdev  is the device address):<br>/iot bluetooth connections connect pdev=DC:2C:6E:0F:C0:3D<br>To connect to TG-BT5-IN/OUT tags, make sure to put it into the  connactable  state by applying a magnet to the magnetic switch.<br>**----- End of picture text -----**<br>

To view an already established connection: 

```
/iot bluetooth connections print
```

To view device characteristics: 

```
/iot bluetooth connections characteristics print
Columns: PDEV, NAME, UUID
 #  PDEV               NAME                              UUID
 0  DC:2C:6E:0F:C0:3D  Service Changed                   2a05
 1  DC:2C:6E:0F:C0:3D  Database Hash                     2b2a
 2  DC:2C:6E:0F:C0:3D  Client Supported Features         2b29
 3  DC:2C:6E:0F:C0:3D  Device Name                       2a00
 4  DC:2C:6E:0F:C0:3D  Appearance                        2a01
...
...
...
```

To read a specific characteristic, specify the `pdev` address and the `uuid` : 

```
/iot bluetooth connections read pdev=DC:2C:6E:0F:C0:3D uuid=2a00
```

Scanners 

1558 

In this menu, you can set up the scanner settings for the Bluetooth chip. When disabled, the device is no longer able to receive advertising reports. When enabled, you can monitor advertising reports in the "Advertising reports" tab (which will be explained later in the guide). You can check and set scanner settings with the commands: 

```
/iot bluetooth scanners print
Flags: X - DISABLED
```

```
Columns: DEVICE, TYPE, INTERVAL, WINDOW, OWN-ADDRESS-TYPE, FILTER-POLICY, FILTER-DUPL
ICATES
```

```
#   DEVICE  TYPE     INTERVAL  WINDOW  OWN-ADDRESS-TYPE  FILTER-POLICY  FIL
0 X bt1     passive  10ms      10ms    random-static     default        off
/iot bluetooth scanners set
```

Configurable properties are shown below: 

**==> picture [516 x 527] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (yes | no; Default:  no ) An option to disable or enable the Bluetooth chip to receive advertising reports.<br>filter-duplicates  (keep-newest |  An option to discard duplicate advertisements from the same advertiser:<br>keep-oldest | keep-unique | off;<br>Default:  off ) keep-newest → Keeps the newest report (discards the oldest). Only the newest PDU from a single AdvA will be<br>kept.<br>keep-oldest → Keeps the oldest report (discards the newest). Only the oldest PDU from a single AdvA will be<br>kept. This type of PDU filtering happens at the controller level and as such it's the most efficient (energy<br>/bandwidth-wise) method of duplicate filtering.<br>keep-unique → Only displays advertisements that have a unique payload. Meaning, if 1+ identical payloads<br>(AdvData) are found, only the first payload is going to be displayed, while the "clones" are discarded/ignored.<br>off → Duplicates are not discarded. All PDUs with the same AdvA will be kept.<br>A duplicate advertising report is an advertising report sent from the same device address. The actual data<br>("AdvData" part of the payload) may change/differ and it is not considered significant when determining du<br>plicate advertising reports. Meaning that, for example, if the Bluetooth interface receives 10 payloads<br>(payload after payload with a 1-second interval) from the same tag:<br>if you are using the "keep-oldest" setting → Bluetooth interface will only display the first payload<br>received (9 follow-up payloads will be filtered out) from that tag.<br>if you are using the "keep-newest" setting → Bluetooth interface will only display the last payload<br>received (each follow-up payload will rewrite the previous one) from that tag.<br>filter-policy  (default | whitelist |  An option to set up a filtering policy (controller-level advertisement filtering):<br>no; Default:  default )<br>default → When this policy is enabled, the scanner will only accept ADV_IND, ADV_NOCONN_IND,<br>ADV_SCAN_IND, SCAN_RSP, and ADV_DIRECT_IND (where TargetA is the scanner's own Bluetooth address)<br>PDU types.<br>whitelist → When this policy is enabled, the scanner will only accept ADV_IND, ADV_NOCONN_IND,<br>ADV_SCAN_IND, SCAN_RSP PDU types that are broadcasted by the advertiser, whose address is configured<br>in the "Whitelist" section, and ADV_DIRECT_IND type PDU (where TargetA is the scanner's own Bluetooth<br>address).<br>interval  (integer:3..10240; Time after which scanner will start scanning the next advertisement channel.<br>Default:  10 ms )<br>own-address-type  (public |  Address type used in scan requests (if active scanning type is used):<br>random-static | rpa-fallback-to-<br>public | rpa-fallback-to-random;  public →  To use the IEEE registered, permanent address.<br>Default:  random-static ) random-static →  To use user-configurable address (will be changed on the next power-cycle).<br>rpa-fallback-to-public → To use Resolvable Random Private Address (RPA) that can only be resolved with our<br>Identity Resolving Key (IRK). If RPA can not be generated, the public address will be used instead.<br>rpa-fallback-to-random → Same as "rpa-fallback-to-public" but if RPA can not be generated, the random-static<br>address will be used instead.<br>**----- End of picture text -----**<br>

1559 

type (active | passive; Default: p Defines the scanner's type: assive ) SCAN_REQ in order to acquire a SCAN_RSP response. window (integer:3..10240; Defau The time that the scanner will spend scanning a single advertisement channel. lt: 10 ms ) 

active → Scanner can send scan requests if it receives a scannable advertisement. The scanner can send a SCAN_REQ in order to acquire a SCAN_RSP response. 

passive → Scanner will only listen for advertisements, no data (e.g. scan requests) will be sent. 

For example, if the scanner interval is set to 20ms, it means that only after 20ms, the device will begin scanning the next channel in line. If the scanner window is set to 10ms, it means that the device will scan each channel only during that 10ms window. Meaning, it will scan channel 37 for 10ms (window time) and begin scanning the next channel after 10 more ms (20ms[interval]-10ms[window]). It will take 10ms to scan channel 38, and after 10 more ms, the device will begin scanning channel 39.
