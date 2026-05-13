## 14.8 Thermal Attributes

Important:       Information contained in this section is preliminary and subject to change without notice.

### 14.8.1 Designing for Thermal Performance

Section 14.12 and Section 14.13 describe the PCB and system design recommendations required to
achieve the proper X550 thermal performance.

1178                                                                                                               333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Thermal Design Recommendations

### 14.8.2 Typical System Definition

A system with the following attributes was used to generate thermal characteristics data:
 • A heat sink case with the default enhanced thermal solution (see Section 14.9).
 • Six-layer, 4.5 x 4 inch PCB.
    Note:         Keep the following in mind when reviewing the data that is included in this sub-section:
              •   All data is preliminary and is not validated against physical samples.
              • Your system design might be significantly different.
              • A larger board with more than six copper layers might improve the X550 thermal
                performance.

### 14.8.3 Package Mechanical Attributes

The X550 is packaged in a 25 mm or 17 mm FCBGA as shown in Section 12.7.4.

#### 14.8.3.1 Package Thermal Characteristics

Refer to Table 14-3 for an aid in determining the optimum airflow and heat sink combination for the
X550. See Section 12.2.2) for more details.
Table 14-3 lists Tcase as a function of airflow and ambient temperature at the TDP for a typical X550
system. Again, your system design might vary considerably from the typical system board environment
used to generate the values listed in Table 14-1 and Table 14-2.
Note:        Thermal models are available upon request (Flotherm*). Contact your local Intel sales
             representative for the X550 thermal models.

Table 14-3. X550 Expected Tcase (°C) for High Heat Sink in Figure 14-3 at 11.5 W (JEDEC
            Card)
   Ambient/
                      0         50          100     150       200        250      300      350       400
 Airflow (LFM)

        45           121.7     113.6        98.67   90.27     85.04     81.37     78.61    76.42   74.64

        50           125.6     117.3        103     94.82     89.7      86.09     83.38    81.23   79.47

        55           129.8     120.9        107.4   99.36     94.34     90.81     88.14    86.02   84.29

        60           133       124.2        111.6   103.9     98.97     95.51     92.9     90.81     89.1

        65           133.5     127.4        115.8   108.3     103.6     100.2     97.63    95.59   93.91

        70           135.9     131          120     112.8     108.2     104.9     102.4    100.4     98.7

        75           139.1     134.7        124.1   117.3     112.8     109.5     107.1    105.1   103.5

        80           142.2     138.6        128.2   121.7     117.2     114.2     111.8    109.9   108.3

        85           145.6     142.5        132.3   126.1     121.9     118.8     116.5    114.6     113

Note:        The red blocked value(s) indicate airflow/ambient combinations that exceed the allowable
             junction temperature for the X550 at 11.5 W.

333369-009                                                                                              1179
                                  Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                            Thermal Design Recommendations
