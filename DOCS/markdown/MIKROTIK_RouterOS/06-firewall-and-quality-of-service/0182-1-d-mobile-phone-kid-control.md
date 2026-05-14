## `1  D ;;; Mobile-phone, kid-control` 

```
      name="queue1" target=192.168.88.254/32 parent=none packet-marks="" priority=8/8 queue=default-small
/default-small limit-at=3M/3M max-limit=3M/3M burst-limit=0/0
```

```
      burst-threshold=0/0 burst-time=0s/0s bucket-size=0.1/0.1
```

It is possible to monitor how much data is used by the specific device: 

```
[admin@MikroTik] > /ip kid-control device print stats
```

```
Flags: X - disabled, D - dynamic, B - blocked, L - limited, I - inactive
 #
```

```
NAME
IDLE-TIME    RATE-DOWN   RATE-UP   BYTES-DOWN     BYTES-UP
```

```
 1 BI Mobile-
```

```
phone
30s         0bps      0bps    3438.1KiB       8.9KiB
```

It is also possible to pause Internet access for the created kids, it will restrict all access until resume is used, which will continue with configured settings: 

```
[admin@MikroTik] > /ip kid-control pause Peter
[admin@MikroTik] > /ip kid-control print
```

```
Flags: X - disabled, P - paused, B - blocked, L - rate-limited
 #
```

```
NAME
SUN      MON      TUE      WED      THU      FRI      SAT
 0 PB
```

```
Peter
15h-21h                             11h-22h          18:30h-22h
```

749
