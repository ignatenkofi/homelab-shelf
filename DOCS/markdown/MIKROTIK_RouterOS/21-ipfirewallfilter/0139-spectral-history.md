## Spectral history 

```
/interface/wifi/spectral-history <wifi interface name> range=
```

**==> picture [505 x 120] intentionally omitted <==**

Plots spectrogram. Power values that fall in different ranges are printed as different colored characters with the same foreground and background color, so it is possible to copy and paste the terminal output of this command. 

`data` - min/max/avg, by default average is used for data. The average should be used in most scenarios, but in some cases "min" can be useful to check if there are any frequencies that have a constant signal output on them. Max will show the strongest signal that was detected, instead of the average signal. `interv` - interval of how often to update the data values; 

- `interval` - interval at which spectrogram lines are printed; `duration` - terminate command after a specified time. default is indefinite; 

- `range` - scan specific range, required; 

- `resolution` - frequency step; 

`show-interference` - yes/no 

Possible types of classified interference: 

- Microwave oven ( `O` ) Continuous Wave ( `C` ) WLAN (Wideband)  ( `W` ) Cordless phone 2.4 ( `T` ) Cordless phone 5 ( `T` ) Bluetooth ( `BB` ) Frequency hopping spread spectrum ( `F` )
