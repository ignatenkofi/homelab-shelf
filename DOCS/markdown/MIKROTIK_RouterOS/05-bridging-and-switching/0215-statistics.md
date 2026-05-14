## Statistics 

Some switch chips are capable of reporting statistics, this can be useful to monitor how many packets are sent to the CPU from the built-in switch chip. These statistics can also be used to monitor CPU Flow Control. You can find an example of the switch chip's statistics below: 

491 

```
[admin@MikroTik] > /interface ethernet switch print stats
```

```
                      name:      switch1
            driver-rx-byte:  221 369 701
          driver-rx-packet:    1 802 975
            driver-tx-byte:   42 621 969
          driver-tx-packet:      310 485
                  rx-bytes:  414 588 529
                 rx-packet:    2 851 236
              rx-too-short:            0
               rx-too-long:            0
              rx-broadcast:    1 040 309
                  rx-pause:            0
              rx-multicast:      486 321
              rx-fcs-error:            0
            rx-align-error:            0
               rx-fragment:            0
                rx-control:            0
             rx-unknown-op:            0
           rx-length-error:            0
             rx-code-error:            0
          rx-carrier-error:            0
                 rx-jabber:            0
                   rx-drop:            0
                  tx-bytes:   44 071 621
                 tx-packet:      312 597
              tx-too-short:            0
               tx-too-long:        8 397
              tx-broadcast:        2 518
                  tx-pause:        2 112
              tx-multicast:        7 142
    tx-excessive-collision:            0
     tx-multiple-collision:            0
       tx-single-collision:            0
     tx-excessive-deferred:            0
               tx-deferred:            0
         tx-late-collision:            0
        tx-total-collision:            0
                   tx-drop:            0
                 tx-jabber:            0
              tx-fcs-error:            0
                tx-control:        2 112
               tx-fragment:            0
                  tx-rx-64:        6 646
              tx-rx-65-127:    1 509 891
             tx-rx-128-255:    1 458 299
             tx-rx-256-511:      178 975
            tx-rx-512-1023:          953
           tx-rx-1024-1518:          672
            tx-rx-1519-max:            0
```

Some devices have multiple CPU cores that are directly connected to a built-in switch chip using separate data lanes. These devices can report which data lane was used to forward the packet from or to the CPU port from the switch chip. For such devices an extra line is added for each row, the first line represents data that was sent using the first data lane, the second line represents data that was sent using the second data line, and so on. You can find an example of the switch chip's statistics for a device with multiple data lanes connecting the CPU and the built-in switch chip: 

492 

```
[admin@MikroTik] > /interface ethernet switch print stats
                  name:      switch1
        driver-rx-byte:  226 411 248
                                   0
      driver-rx-packet:    1 854 971
                                   0
        driver-tx-byte:   45 988 067
                                   0
      driver-tx-packet:      345 282
                                   0
              rx-bytes:  233 636 763
                                   0
             rx-packet:    1 855 018
                                   0
          rx-too-short:            0
                                   0
           rx-too-long:            0
                                   0
              rx-pause:            0
                                   0
          rx-fcs-error:            0
                                   0
           rx-overflow:            0
                                   0
              tx-bytes:   47 433 203
                                   0
             tx-packet:      345 282
                                   0
    tx-total-collision:            0
                                   0
```
