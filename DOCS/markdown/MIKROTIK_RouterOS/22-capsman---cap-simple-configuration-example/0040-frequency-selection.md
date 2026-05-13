## Frequency selection 

As mentioned in the introduction, local authorities regulate Wi-Fi device's output powers. Different frequency ranges in different countries can have different allowed powers. You can check which limitations apply to your country profile using the command: 

```
/interface/wifi/radio/reg-info country=Latvia 0
  ranges: 2402-2482/20dBm/40MHz
          5170-5250/23dBm/160MHz/indoor
          5250-5330/23dBm/160MHz/indoor/dfs
          5490-5730/30dBm/160MHz/dfs
          5735-5875/14dBm/80MHz
```

As per the table, we can see that the most power (using "Latvia" country profile) we can get is `30 dBm` on channels `5490-5730` . 

"dBm" showed in this table represents "allowed EIRP" (EIRP=Tx power + antenna gain). Not to break any regulations and "laws", the more antenna gain the device has, the lower Tx power is set (if the device has a built-in antenna, it will happen automatically ), to match the allowed "EIRP" value. 

1367 

Also note, that it could be that the highest "EIRP" channels are "DFS" channels (meaning that if a radar is detected on the channel, the broadcasting stops). This is something to keep in mind! 

With this information, per the table, we can see that it would be wise to avoid using `5735-5875` range, as it only allows `14 dBm` . 

The more "EIRP" is allowed on the channel = the more output power will be available = the stronger the signal will be = the bigger distance you can get. 

**==> picture [13 x 13] intentionally omitted <==**

Please note that there is a country profile called "Superchannel". In this profile, there are no software limitations applied to output powers. This mode should only be used in controlled environments, or if you have special permission to use it in your region. You can combine it with "reducing" Tx power value directly in the settings to get "custom" power output. 

Frequency-wise, additionally, remember! that the lower the channel width is, the less interference and the bigger the distance you can get. Meaning, for longer distances, use 20 MHz.
