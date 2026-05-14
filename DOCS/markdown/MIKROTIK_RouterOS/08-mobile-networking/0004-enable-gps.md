## Enable GPS: 

```
[admin@MikroTik] /system gps> set enable=yes port=usb1
[admin@MikroTik] /system gps> print
          enabled: yes
             port: usb1
          channel: 0
     init-channel: 0
      init-string:
  set-system-time: no
```

Monitor status: 

798 

```
[admin@MikroTik] /system gps> monitor
        date-and-time: sep/07/2021 08:26:26
             latitude: 56.969689
            longitude: 24.162471
             altitude: 25.799999m
                speed: 0.759320 km/h
  destination-bearing: none
         true-bearing: 185.500000 deg. True
     magnetic-bearing: 0.000000 deg. Mag
                valid: yes
           satellites: 6
          fix-quality: 1
  horizontal-dilution: 1.3
```

Port and GPS settings for LtAP 

```
/port set serial1 baud-rate=115200
```

```
/system gps set port=serial1 channel=0 enabled=yes
```

We have also created an in-depth article about live GPS tracking, using scripting and a web server: GPS-tracking.
