## Peripheral Devices 

This section displays decoded Eddystone TLM, Eddystone UID, iBeacon and MikroTik Bluetooth payloads. If the "Peripheral Devices" captures other beacon types, they will not be decoded. 

You can view a decoded list with a `print detail` command: 

- `/iot bluetooth peripheral-devices print detail` 

- `0 address-type=public address=60:C0:BF:87:E2:1C name="60:C0:BF:87:E2:1C" persist=no mtik-key="" rssi=-64` 

- `last-data="0201041BFFCD0960C0BF87E21C025B1F198B21AC62CDAE0045FAFEFE057D7B" last-seen=2023-08-22 11:20:09 beacon-types=""` 

- `1 address-type=public address=DC:2C:6E:0F:C0:3D name="DC:2C:6E:0F:C0:3D" persist=no mtik-key="" rssi=-47` 

- `last-data="0303AAFE1716AAFE00E5B2B98DE4C81C47C2B14E7500000000000000" last-seen=2023-08-22 11:20:05 beacon-types=mikrotik,ibeacon,eddystone-uid mtik-version=1 mtik-encrypted=no mtik-acc-x=-0.007G mtik-acc-y=-0.015G mtik-acc-z=-0.007G mtik-temperature=23.808C mtik-battery=100% mtik-uptime=14342160s mtik-flags=""` 

- `ibeacon-uuid="55555555-5555-5555-5555-222222222222" ibeacon-major=1280 ibeacon-minor=512 ibeacon-rssi-at-1m=-68dBm eddy-rssi-at-1m=-27dBm eddy-namespace="b2b98de4c81c47c2b14e" eddy-instance="750000000000"` 

- `2 address-type=public address=DC:2C:6E:F6:54:7D name="DC:2C:6E:F6:54:7D" persist=no mtik-key="" rssi=-74` 

- `last-data="0201060303AAFE1116AAFE20000B701549023532D802384F46" last-seen=2023-08-22 11:20:13 beacon-types=eddystone-tlm eddy-version=0 eddy-battery-voltage=2.928V eddy-temperature=21.285C eddy-packet-count=37040856 eddy-uptime=3724474.2s` 

- `3 address-type=public address=DC:2C:6E:0F:C0:3E name="DC:2C:6E:0F:C0:3E" persist=no mtik-key="" rssi=-72 last-data="15FF4F0901000214FFFF0200FDFF4F1774E00F000064" last-seen=2023-08-22 11:20:06 beacon-types=mikrotik mtik-version=1 mtik-encrypted=no mtik-acc-x=-0.003G mtik-acc-y=0.007G mtik-acc-z=-0.011G mtik-temperature=23.308C mtik-battery=100% mtik-uptime=1040500s mtik-flags=""` 

- `4 address-type=public address=60:C0:BF:20:9A:50 name="60:C0:BF:20:9A:50" persist=no mtik-key="" rssi=-66` 

- `last-data="0201041BFF4160C0BF209A50FFA4CA8906E48C0377DCFDD2DF7AF02FFC6AC5" last-seen=2023-08-22 11:20:11 beacon-types=""` 

You can filter the list, for example, based on the "address" of the device (knowing MAC-address of the tag): 

1562 

```
/iot bluetooth peripheral-devices print detail where address="DC:2C:6E:0F:C0:3E"
 0 address-type=public address=DC:2C:6E:0F:C0:3E name="my_tag" persist=yes
   mtik-key="" rssi=-60 last-data="15FF4F090100669DFCFF0600FCFF6117F1E50F000064"
   last-seen=2023-08-22 11:43:31 beacon-types=mikrotik mtik-version=1
   mtik-encrypted=no mtik-acc-x=-0.015G mtik-acc-y=0.023G mtik-acc-z=-0.015G
   mtik-temperature=23.378C mtik-battery=100% mtik-uptime=1041905s mtik-flags=""
/iot bluetooth peripheral-devices print value-list where address="DC:2C:6E:0F:C0:3E"
      address-type: public
           address: DC:2C:6E:0F:C0:3E
              name: my_tag
           persist: yes
          mtik-key:
              rssi: -71
         last-data: 15FF4F0901002AC60400000004004F17D4E90F000064
         last-seen: 2023-08-22 12:00:06
      beacon-types: mikrotik
      mtik-version: 1
    mtik-encrypted: no
        mtik-acc-x: 0.015G
        mtik-acc-y: 0G
        mtik-acc-z: 0.015G
  mtik-temperature: 23.308C
      mtik-battery: 100%
       mtik-uptime: 1042900s
        mtik-flags:
```

Or, for example, filter the list based on the beacon type: 

```
/iot bluetooth peripheral-devices print detail where beacon-types=mikrotik
```

```
 0 address-type=public address=DC:2C:6E:0F:C0:3E name="my_tag" persist=yes
   mtik-key="" rssi=-69 last-data="15FF4F0901000747020002000100611778E60F000064"
   last-seen=2023-08-22 11:45:46 beacon-types=mikrotik mtik-version=1
   mtik-encrypted=no mtik-acc-x=0.007G mtik-acc-y=0.007G mtik-acc-z=0.003G
   mtik-temperature=23.378C mtik-battery=100% mtik-uptime=1042040s mtik-flags=""
```

```
 7 address-type=public address=2C:C8:1B:4B:BB:0A name="2C:C8:1B:4B:BB:0A" persist=no
   mtik-key="" rssi=-44 last-data="15FF4F09010077090000FCFFFDFFD519BF9EFF00005B"
   last-seen=2023-08-22 11:45:53 beacon-types=mikrotik mtik-version=1
   mtik-encrypted=no mtik-acc-x=0G mtik-acc-y=-0.015G mtik-acc-z=-0.011G
   mtik-temperature=25.832C mtik-battery=91% mtik-uptime=16752319s mtik-flags=""
```

Additionally, you have the option to set " `persist=yes` ", which will make sure that the device/tag stays on the list forever (because devices that stop 

broadcasting payloads will be timed-out after one minute and removed from the list until new payloads start appearing in the air): 

```
/iot bluetooth peripheral-devices set persist=yes address="DC:2C:6E:0F:C0:3E"
```

You can also set a name for the device, so you can easier find it on the list, with the command: 

```
/iot bluetooth peripheral-devices set name="my_tag" address="DC:2C:6E:0F:C0:3E"
```
