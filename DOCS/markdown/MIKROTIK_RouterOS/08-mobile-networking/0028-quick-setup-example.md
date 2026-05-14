## Quick setup example 

Start with network settings - Add new connection parameters under LTE apn profile (provided by network provider): 

```
/interface lte apn add name=profile1 apn=phoneprovider.net authentication=chap password=web user=web
```

Select the newly created profile for an LTE connection: 

```
/interface lte set [find] apn-profiles=profile1
```

LTE interface should appear with the running (R) flag: 

```
[admin@MikroTik] > /interface lte print
Flags: X - disabled, R - running
0 R name="lte1" mtu=1500 mac-address=AA:AA:AA:AA:AA:AA
```

816 

If required, add NAT Masquerade for LTE Interface to get internet to the local network: 

```
/ip firewall nat add action=masquerade chain=srcnat out-interface=lte1
```

After the interface is added, you can use the "info" command to see what parameters the client acquired (parameters returned depends on the LTE hardware device): 

```
[admin@MikroTik] > interface/lte/monitor
lte1
           status: connected
            model: EG18-EA
         revision: EG18EAPAR01A12M4G
 current-operator: LMT
   current-cellid: 3103242
           enb-id: 12122
        sector-id: 10
       phy-cellid: 480
       data-class: LTE
   session-uptime: 15m54s
             imei: 86981604098XXXX
             imsi: 24701060267XXXX
             iccid: 8937101122102057XXXX
     primary-band: B3@20Mhz earfcn: 1300 phy-cellid: 480
    dl-modulation: qpsk
              cqi: 7
               ri: 2
              mcs: 1
             rssi: -68dBm
             rsrp: -97dBm
             rsrq: -9dB
             sinr: 6dB
```
