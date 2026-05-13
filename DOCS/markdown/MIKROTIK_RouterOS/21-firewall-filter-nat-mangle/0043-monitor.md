## Monitor 

To print out a current link rate and other Ethernet related properties or to see detailed diagnostics information for transceivers, use " `/interface ethernet monitor` " command. The provided information can differ for different interface types (e.g. Ethernet over twisted pair or SFP interface) or for different transceivers (e.g. SFP and QSFP). 

Properties 

Property Description 

1301 

advertising (since RouterOS v7.12: 10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1G-baseT-half | 1G-baseT-full | 1G-baseX | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR | 40GbaseSR4-LR4 | 40G-baseCR4 | 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100G-baseSR4-LR4 | 100G-baseCR4) 

advertising (since RouterOS v7.12: 10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1G-baseT-half | Advertised link 1G-baseT-full | 1G-baseX | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR | 40Gmodes, only applies baseSR4-LR4 | 40G-baseCR4 | 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100G-baseSR4-LR4 | when auto100G-baseCR4) negotiation is enabled (older RouterOS: 10M-full | 10M-half | 100M-full | 100M-half | 1000M-full | 1000M-half | 2500M-full | 5000M-full | 10000M-full) auto-negotiation (disabled | done | failed | incomplete) Current autonegotiation status: disabled - negotiation disabled done - negotiation completed failed - negotiation failed incomplete - negotiation not completed yet default-cable-settings (short | standard) Default cable length setting (only applicable to NS DP83815/6 cards) short - support short cables standard - support standard cables fec (fec74 | fec91 | off) Current FEC mode. full-duplex (yes | no) Whether transmission of data occurs in two directions simultaneously link-partner-advertising (since RouterOS v7.12: 10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1GLink partner baseT-half | 1G-baseT-full | 1G-baseX | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR advertised link | 40G-baseSR4-LR4 | 40G-baseCR4 | 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100Gmodes, only applies baseSR4-LR4 | 100G-baseCR4) when autonegotiation is (older RouterOS: 10M-full | 10M-half | 100M-full | 100M-half | 1000M-full | 1000M-half | 2500M-full | 5000M-full | 10000M-full) enabled rate (10Mbps | 100Mbps | 1Gbps | 2.5Gbps | 5Gbps | 10Gbps | 25Gbps | 40Gbps | 50Gbps | 100Gbps | 200Gbps | 400Gbps) Actual data rate of the connection. 

1302 

status (link-ok | no-link | unknown) Current link status of an interface link-ok - the card is connected to the network no-link - the card is not connected to the network unknown - the connection is not recognized (if the card does not report connection status) tx-flow-control (yes | no) Whether TX flow control is used rx-flow-control (yes | no) Whether RX flow control is used combo-state (copper | sfp) Used combo-mode for combo interfaces sfp-module-present (yes | no) Whether a transceiver is in cage sfp-rx-lose (yes | no) Whether a receiver signal is lost sfp-tx-fault (yes | no) Whether a transceiver transmitter is in fault state sfp-type (SFP/SFP+/SFP28/SFP56 | DWDM-SFP/SFP+ | QSFP | QSFP+ | QSFP28/QSFP56 | QSFPDD) Used transceiver type sfp-cmis-revision (string) Transceiver CMIS revision number sfp-connector-type (SC | LC | optical-pigtail | copper-pigtail | multifiber-parallel-optic-1x12 | multifiber-parallel-optic-1x16 | noUsed transceiver separable-connector | RJ45) connector type sfp-link-length-9um (m) Transceiver supported link length for single mode 9 /125um fiber sfp-link-length-sm (km) Transceiver supported link length for single mode fiber sfp-link-length-om3 (m) Transceiver supported link length for multi mode (OM3) sfp-link-length-om4 (m) Transceiver supported link length for multi mode (OM4) 

1303 

**==> picture [506 x 668] intentionally omitted <==**

**----- Start of picture text -----**<br>
sfp-link-length-om5  (m) Transceiver<br>supported link length<br>for multi mode (OM5)<br>sfp-link-length-50um  (m) Transceiver<br>supported link length<br>for multi mode 50<br>/125um fiber (OM2)<br>sfp-link-length-62um  (m) Transceiver<br>supported link length<br>for multi mode 62.5<br>/125um fiber (OM1)<br>sfp-link-length-copper  (m) Supported link<br>length of copper<br>transceiver<br>sfp-vendor-name  (string) Transceiver<br>manufacturer<br>sfp-vendor-part-number  (string) Transceiver part<br>number<br>sfp-vendor-revision  (string) Transceiver revision<br>number<br>sfp-vendor-serial  (string) Transceiver serial<br>number<br>sfp-manufacturing-date  (date) Transceiver<br>manufacturing date<br>sfp-power-class  (string) Transceiver power<br>class<br>sfp-max-power  (W) Transceiver<br>maximum power<br>consumption<br>sfp-wavelength  (nm) Transceiver<br>transmitter optical<br>signal wavelength<br>sfp-temperature  (C) Transceiver<br>temperature<br>sfp-supply-voltage  (V) Transceiver supply<br>voltage<br>sfp-tx-bias-current  (mA) Transceiver Tx bias<br>current<br>sfp-tx-power  (dBm) Transceiver<br>transmitted optical<br>power<br>sfp-rx-power  (dBm) Transceiver<br>received optical<br>power<br>sfp-supported  (10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1G-baseT-half | 1G-baseT-full | 1G- Module supported<br>baseX | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR | 40G-baseSR4-LR4 | 40G- link modes. This<br>baseCR4 | 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100G-baseSR4-LR4 | 100G-baseCR4 |  property only applies<br>50G-baseSR-LR | 50G-baseCR | 100G-baseSR2-LR2 | 100G-baseCR2 | 200G-baseSR4-LR4 | 200G-baseCR4 | 400G- to certain devices.<br>baseSR8-LR8 | 400G-baseCR8)<br>**----- End of picture text -----**<br>


1304 

supported (10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1G-baseT-half | 1G-baseT-full | 1G-baseX | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR | 40G-baseSR4-LR4 | 40G-baseCR4 | 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100G-baseSR4-LR4 | 100G-baseCR4 | 50G-baseSRLR | 50G-baseCR | 100G-baseSR2-LR2 | 100G-baseCR2 | 200G-baseSR4-LR4 | 200G-baseCR4 | 400G-baseSR8-LR8 | 400G-baseCR8) 

eeprom-checksum (good | bad) eeprom (hex dump) 

Shows the supported interface hardware link mode capabilities. 

Whether EEPROM checksum is correct Raw EEPROM of the transceiver 

Example output of an Ethernet status: 

```
[admin@MikroTik] > /interface ethernet monitor ether2
                      name: ether2
                    status: link-ok
          auto-negotiation: done
                      rate: 1Gbps
               full-duplex: yes
           tx-flow-control: no
           rx-flow-control: no
                 supported: 10M-baseT-half,10M-baseT-full,100M-baseT-half,100M-baseT-full,1G-baseT-half,1G-
baseT-full
               advertising: 10M-baseT-half,10M-baseT-full,100M-baseT-half,100M-baseT-full,1G-baseT-half,1G-
baseT-full
  link-partner-advertising: 10M-baseT-half,10M-baseT-full,100M-baseT-half,100M-baseT-full,1G-baseT-half,1G-
baseT-full
```

Example output of an SFP status: 

1305 

```
[admin@MikroTik] > /interface ethernet monitor sfp3
                      name: sfp3
                    status: link-ok
          auto-negotiation: done
                      rate: 1Gbps
               full-duplex: no
           tx-flow-control: no
           rx-flow-control: no
                 supported: 10M-baseT-half,10M-baseT-full,100M-baseT-half,100M-baseT-full,1G-baseT-half,1G-
baseT-full,1G-baseX
             sfp-supported: 1G-baseX
               advertising: 1G-baseX
  link-partner-advertising:
        sfp-module-present: yes
               sfp-rx-loss: no
              sfp-tx-fault: no
                  sfp-type: SFP/SFP+/SFP28/SFP56
        sfp-connector-type: LC
       sfp-link-length-om1: 500m
       sfp-link-length-om2: 550m
           sfp-vendor-name: Mikrotik
    sfp-vendor-part-number: S-85DLC05D
         sfp-vendor-serial: SG85M31401687
    sfp-manufacturing-date: 13-04-24
            sfp-wavelength: 850nm
           sfp-temperature: 33C
        sfp-supply-voltage: 3.237V
       sfp-tx-bias-current: 2mA
              sfp-tx-power: -5.792dBm
              sfp-rx-power: -5.22dBm
           eeprom-checksum: good
                    eeprom: 0000: 03 04 07 00 00 00 01 00  00 00 00 03 0d 00 00 00  ........ ........
                            0010: 37 32 00 00 4d 69 6b 72  6f 74 69 6b 20 20 20 20  72..Mikr otik
                            0020: 20 20 20 20 00 00 00 00  53 2d 38 35 44 4c 43 30      .... S-85DLC0
                            0030: 35 44 20 20 20 20 20 20  00 00 00 00 03 52 00 50  5D       .....R.P
                            0040: 00 1a 00 00 53 47 38 35  4d 33 31 34 30 31 36 38  ....SG85 M3140168
                            0050: 37 20 20 20 31 33 30 34  32 34 20 20 68 b0 01 f3  7   1304 24  h...
                            0060: 00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  ........ ........
                            *
                            0080: 64 00 d2 ff 5a 00 d7 ff  8c a0 75 30 88 b8 79 18  d...Z... ..u0..y.
                            0090: 75 30 00 fa 61 a8 01 f4  1f 07 03 1a 18 a5 03 e7  u0..a... ........
                            00a0: 31 2e 00 13 27 12 00 27  00 00 00 00 00 00 00 00  1...'..' ........
                            00b0: 00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  ........ ........
                            00c0: 00 00 00 00 3f 80 00 00  00 00 00 00 01 00 00 00  ....?... ........
                            00d0: 01 00 00 00 01 00 00 00  01 00 00 00 00 00 00 23  ........ .......#
                            00e0: 21 7c 7e 72 05 27 0a 4b  0b be 00 00 00 00 00 94  !|~r.'.K ........
                            00f0: 00 00 00 00 00 00 00 00  20 21 2a ff ff ff ff 00  ........  !*.....
```
