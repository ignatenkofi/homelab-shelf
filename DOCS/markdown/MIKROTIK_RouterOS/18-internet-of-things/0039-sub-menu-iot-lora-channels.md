## Sub-menu: `/iot lora channels` 

**==> picture [516 x 149] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bandwidth  (7.8_kHz | 15.6_kHz | 31.2_kHz | 62.5_kHz |  Bandwidth of specific channel, predefined when any of channel-plan preset is used, but<br>125_kHz | 250_kHz | 500_kHz; Default:  125_kHz ) could be manually changed when channel-plan is set to custom.<br>disabled  (yes | no; Default:  no ) Disable or enable the channel.<br>freq-off  (integer [-400000..400000]; Default:  ) Channel frequency offset against radio central frequency, it makes possible to adjust<br>channel frequencies so that channels does not overlap.<br>radio  (radio0 | radio1; Default: ) Defines which radio uses selected channel.<br>spread-factor  (SF7 | SF8 | SF9 | SF10 | SF11 | SF12;  Defines the Spread Factor for a channel with type=LoRa. Lower Spread Factor means<br>Default: ) higher data rate.<br>**----- End of picture text -----**<br>

To view current channels, issue the command `/iot lora cannels print` : 

1600 

```
/iot lora channels print
Columns: NAME, TYPE, RADIO, FREQ-OFF, BANDWIDTH, FREQ, SPREAD-FACTOR, DATARATE
# NAME       TYPE  RADIO   FREQ-OFF  BANDWIDTH  FREQ   SPREAD-FACTOR  DATARATE
0 gateway-0  MSF   radio1  -400000   125_kHz    868.1
1 gateway-0  MSF   radio1  -200000   125_kHz    868.3
2 gateway-0  MSF   radio1  0         125_kHz    868.5
3 gateway-0  MSF   radio0  -400000   125_kHz    867.1
4 gateway-0  MSF   radio0  -200000   125_kHz    867.3
5 gateway-0  MSF   radio0  0         125_kHz    867.5
6 gateway-0  MSF   radio0  200000    125_kHz    867.7
7 gateway-0  MSF   radio0  400000    125_kHz    867.9
8 gateway-0  LoRa  radio1  -200000   250_kHz    868.3  SF7
9 gateway-0  FSK   radio1  300000    125_kHz    868.8                    50000
```

Channels are created using `freq-off` and radio's `center-freq` frequencies. To view radios center frequencies use the command `/iot lora` . 

```
radios print
```

To understand how each channel's frequency is calculated, check the example below: 

```
# NAME       TYPE  RADIO   FREQ-OFF  BANDWIDTH  FREQ   SPREAD-FACTOR  DATARATE
0 gateway-0  MSF   radio1  -400000   125_kHz    868.1
```

`radio1` is selected to be used for channel #0 and it is configured with `center-freq=868500000` (868500000 Hz or 868.5 MHz). 

By using frequency offset, `freq-off=-400000` (-400000 Hz or -0.4 MHz), we define channel #0 to be `868500000-400000=868100000` Hz or 868.1 MHz. 

**==> picture [13 x 13] intentionally omitted <==**

To configure custom channels, select "custom" channel profle with the help of the command: 

```
/iot lora set [find] channel-plan=custom
```
