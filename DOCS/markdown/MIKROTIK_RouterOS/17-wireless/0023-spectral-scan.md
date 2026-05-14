## Spectral scan 

The spectral scan can scan frequencies supported by your wifi interface, and plot them directly in the console. The spectral scan has been available since the 7.16beta1 version. 

1339 

**==> picture [13 x 13] intentionally omitted <==**

Spectral scan is supported only by the wifi-qcom driver, it is not supported by the wifi-qcom-ac driver. 

```
/interface/wifi/spectral-scan <wifiinterface name> range=
```

**==> picture [434 x 316] intentionally omitted <==**

Continuously monitors spectral data. This command uses the same data source as 'spectral-history', and shares many parameters. 

To use spectral scan, you must use the "range=" attribute. 

Each line displays one spectrogram bucket -- frequency, magnitude (dBm), peak, and a character graphic bar. A bar shows power value with ':' characters and average peak hold with '.' characters. 

`data` - min/max/avg, by default average is used for data. The average should be used in most scenarios, but in some cases "min" can be useful to check if there are any frequencies that have a constant signal output on them. Max represents the strongest signal that was detected during the interval of the scan, similar to the peak. 

`duration` - terminate command after a specified time. default is indefinite; 

`freeze-frame-interval` - Time interval at which to update command output 

`interval` - interval of how often to update the primary data values, not peak 

`peak-mode` - avg/max/disabled - peak reflects the strongest signal over peak-hold-duration. By default "avg" is used, it is the average of max values over "peak-hold-duration", if "max" is used, then the highest value will be shown until the next "peak-hold-duration" update. `peak-hold-duration` - changes the peak hold duration used by peak-mode, by default 5 seconds. 

`range` - scan specific range, required; 

`resolution` - frequency step for spectral scan 

`show-interference` - yes/no 

Possible types of classified interference: 

Microwave oven ( `MWO` ) Continuous Wave ( `CW` ) WLAN (Wideband) ( `WIFI` ) 

1340 

- Cordless phone 2.4 ( `CORDLESS24` ) Cordless phone 5 ( `CORDLESS5` ) Bluetooth ( `BLUETOOTH` ) Frequency hopping spread spectrum ( `FHSS` )
