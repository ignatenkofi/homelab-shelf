## Radios 

Information about the capabilities of each radio can be gained by running the `/interface/wifi/radio print detail` command.  It can be useful to see what bands are supported by the interface and what channels can be selected. The country profile that is applied to the interface will influence the results. 

```
interface/wifi/radio/print detail
Flags: L - local
```

```
 0 L radio-mac=48:A9:8A:0B:F7:4A phy-id=0 tx-chains=0,1 rx-chains=0,1
     bands=5ghz-a:20mhz,5ghz-n:20mhz,20/40mhz,5ghz-ac:20mhz,20/40mhz,20/40/80mhz,5ghz-ax:20mhz,
      20/40mhz,20/40/80mhz
```

```
     ciphers=tkip,ccmp,gcmp,ccmp-256,gcmp-256,cmac,gmac,cmac-256,gmac-256 countries=all
     5g-channels=5180,5200,5220,5240,5260,5280,5300,5320,5500,5520,5540,5560,5580,5600,5620,5640,5660,
            5680,5700,5720,5745,5765,5785,5805,5825
```

```
     max-vlans=128 max-interfaces=16 max-station-interfaces=3 max-peers=120 hw-type="QCA6018"
     hw-caps=sniffer interface=wifi1 current-country=Latvia
```

```
     current-channels=5180/a,5180/n,5180/n/Ce,5180/ac,5180/ac/Ce,5180/ac/Ceee,5180/ax,5180/ax/Ce,
                 5180/ax/Ceee,5200/a,5200/n,5200/n/eC,5200/ac,5200/ac/eC,5200/ac/eCee,5200/ax...
                 ...5680/n/eC,5680/ac,5680/ac/eC,5680/ax,5680/ax/eC,5700/a,5700/n,5700/ac,5700/ax
     current-gopclasses=115,116,128,117,118,119,120,121,122,123 current-max-reg-power=30
```

While Radio information gives us information about supported channel width, it is also possible to deduce this information from the product page, to do so you need to check the following parameters: number of chains , max data rate . Once you know these parameters, you need to check the modulation and coding scheme (MCS) table, for example, here: https://mcsindex.com/. 

If we take hAP ax2, as an example, we can see that number of chains is 2, and the max data rate is 1200 - 1201 in the MCS table. In the MCS table we need to find entry for 2 spatial streams - chains, and the respective data rate, which in this case shows us that 80MHz is the maximum supported channel width.
