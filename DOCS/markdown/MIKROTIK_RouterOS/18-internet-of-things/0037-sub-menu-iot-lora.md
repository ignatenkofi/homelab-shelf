## Sub-menu: `/iot lora` 

**==> picture [516 x 281] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>antenna-gain  (integer [-128..127];  Antenna gain in dBi. This value should be equal to  setup-antenna-gain  minus  cable-loss . Using 6.5 dBi<br>Default: ) 0 antenna, 6.5 is the value to be configured (not taking into account cable loss).<br>Output power of the gateway is dictated by the server. The gateway will calculate its actual output power by<br>subtracting  antenna-gain  setting from  server_value  (value received in the downlink message).<br>channel-plan  (as-923 | au-915 |  Frequency plans for various regions.<br>custom | eu-868 | in-865 | kr-920<br>| ru-864 | ru-864-mid | us-915-1 |<br>us-915-2; Default:  eu-868 )<br>disabled  (yes | no; Default:  yes ) Whether LoRaWAN gateway is disabled.<br>forward  (ccrc-validtaion | dev- Defines what kind of packets should be forwarded to Network server:<br>addr-validtaion | proprietary-traffic<br>; Default:  crc-validtaion ) crc-validtaion - Forward valid packets with correct CRC.<br>dev-addr-validtaion - Checks if DevAddr of the packet corresponds to the NetID and if not, drops the packet.<br>The following sequence happens: 1) Dev. Addr value gets "obtained" from the received LoRa packet; 2) Dev.<br>Addr is "compared" against "valid" Net IDs list; 3) If there is no Net ID for the Dev. Addr, the packet is not<br>forwarded; 4) If Net ID is valid, Dev. Addr range is valid, the packet is forwarded.<br>proprietary-traffic - Checks the content of the LoRa packet and if the "type" of the frame is "proprietary", the<br>packet is not forwarded.<br>gateway-id  (string) Gateway ID or Gateway EUI, is used when registering the gateway with the server.<br>**----- End of picture text -----**<br>

1599 

**==> picture [516 x 232] intentionally omitted <==**

**----- Start of picture text -----**<br>
lbt-enabled  (yes | no; Default:  no ) Whether gateway should use LBT (Listen Before Talk) protocol.<br>listen-time  (integer [0us.. Time in microseconds to track RSSI before TX (used when  lbt-enabled=yes ).<br>4294967295us]; Default:  5000us )<br>name  (string; Default: ) Name of LoRaWAN gateway.<br>network  (private | public; Default:  Whether sync word should (network=private) or should not (network=public) be used.<br>public )<br>rssi-threshold  (integer [-32,768 ..  RSSI value to determine whether forwarder may use specific channel to talk. If RSSI value is below  rssi-threshold ,<br>32,767]; Default:  -65dB ) channel could be used (used when  lbt-enabled=yes ).<br>servers  (list of string; Default: ) Name of the server from the  /iot lora servers  section.<br>src-address  (IP; Default: ) Specifies uplink packet source address if necessary (address should match an address configured on the RB).<br>spoof-gps  (string; Default: ) Set custom GPS location:<br>Latitude [-90..90]<br>Longitude [-180..180]<br>Altitude( m ) [-2147483648..2147483647]<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

Once the server is selected and LoRa interface is enabled using `/iot lora enable [find]` command, the device will start operating as a LoRaWAN gateway. It will start forwarding LoRa payloads from the `/iot lora traffic` tab to the configured server.
