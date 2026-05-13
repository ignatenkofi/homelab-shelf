## What TX-power values can I use? 

The tx-power default setting is the maximum tx-power that the card can use and is taken from the cards eeprom. If you want to use larger tx-power values, you are able to set them, but do it at your own risk , as it will probably damage your card eventually! Usually, one should use this parameter only to reduce the tx-power. 

In general, tx-power controlling properties should be left at the default settings. Changing the default setting may help with some cards in some situations, but without testing, the most common result is the degradation of range and throughput. Some of the problems that may occur are: 

overheating of the power amplifier chip and the card which will cause lower efficiency and more data errors; 

overdriving the amplifier which will cause more data errors; 

excessive power usage for the card and this may overload the 3.3V power supply of the board that the card is located on resulting in voltage drop and reboot or excessive temperatures for the board.
