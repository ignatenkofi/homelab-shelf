## Troubleshooting 

Note that sometimes to make the GPS module recognized in RouterOS you need to change the baud-rate setting in the ' `/port` ' menu. LtAP mini has a low-gain GPS antenna built-in and for a better experience, we suggest using an additional external antenna. 

Switch between internal and external antennas under the GPS menu: 

```
[admin@MikroTik] > /system gps set gps-antenna-select=external
```

On some modems with GPS support, you need to send multiple init commands for continuous GPS monitoring, for example, for Huawei cards you need to send "AT^WPDST=1,AT^WPDGP" init string to get continuous monitoring. 

799
