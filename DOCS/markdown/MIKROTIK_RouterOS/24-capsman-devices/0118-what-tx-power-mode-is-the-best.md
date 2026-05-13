## What TX-power-mode is the best? 

TX-power-mode tells the wireless card which tx-power values should be used. By default, this setting is set to default. 

default means that the card will use the tx-power values from the cards eeprom and will ignore the setting what is specified by the user in the txpower field. 

card-rates means that for different data rates the tx-power is calculated according to the cards transmit power algorithm from the cards eeprom and as an argument it takes tx-power value specified by the user. all-rates-fixed means that that the card will use one tx-power value for all data rates which is specified by the user in tx-power field. 

Note that it is not recommended to use 'all-rates-fixed' mode as the wireless card tx-power for the higher data rates is lower and by forcing to use the fixed tx-power rates also for the higher data rates might result in the same problems like in the previous question about tx-power setting. In the case of MikroTik Radio devices, the power will not be higher than the power written in the EEPROM. For most of the cases if you want to change the tx-power settings it is recommended to use the tx-power-mode=card-rates and it is recommended to lower and not to raise tx-power. In case of AR9300 and newer Atheros wireless chipsets "tx-power-mode=all-rate-fixed" is the only option as "card-rates" option isn't working on those chipsets.
