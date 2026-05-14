## `/interface wireless scan wlan1 rounds=1 save-file=scan1` 

To use background wireless scan the 'background=yes' setting should be provided. Example: 

- `/interface wireless scan wlan1 background=yes` 

1421 

Background scan feature is working in such conditions: 

Wireless interface should be enabled 

For wireless interface in AP mode - when it is operating in 802.11 protocol mode and is on fixed channel (that is - channel selection and initial radar checking is over) 

For wireless interface in Station mode - when it is connected to 802.11 protocol AP. 

Scan command is supported also on the Virtual wireless interfaces with such limitations: 

It is possible when virtual interface and its master is fixed on channel (master AP is running or master station is connected to AP). Scan is only performed in channel master interface is on. 

It does not matter if background=yes|no - on virtual interface scan does not disconnect clients/AP, so it is always "background".
