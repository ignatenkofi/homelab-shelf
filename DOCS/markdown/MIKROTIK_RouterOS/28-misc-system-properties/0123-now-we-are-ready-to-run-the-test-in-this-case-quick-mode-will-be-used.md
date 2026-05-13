## Now we are ready to run the test. In this case, quick mode will be used: 

```
[admin@test-host] /tool traffic-generator> quick mbps=450
SEQ    NUM     TX-PACKET   TX-RATE     RX-PACKET   RX-RATE        RX-OOO   LOST-PACKET LOST-RATE
37     4          39 488 458.0Mbps        39 270 455.5Mbps        15 509           218   2.5Mbps
37     TOT        78 976 916.1Mbps        76 485 887.2Mbps        22 529         2 491  28.8Mbps
38     3          38 957 451.9Mbps        37 657 436.8Mbps         7 078         1 300  15.0Mbps
38     4          38 958 451.9Mbps        38 402 445.4Mbps        14 763           556   6.4Mbps
38     TOT        77 915 903.8Mbps        76 059 882.2Mbps        21 841         1 856  21.5Mbps
39     3          38 816 450.2Mbps        37 893 439.5Mbps         7 307           923  10.7Mbps
39     4          38 815 450.2Mbps        38 642 448.2Mbps        15 110           173   2.0Mbps
39     TOT        77 631 900.5Mbps        76 535 887.8Mbps        22 417         1 096  12.7Mbps
40     3          39 779 461.4Mbps        37 415 434.0Mbps         7 136         2 364  27.4Mbps
40     4          39 780 461.4Mbps        39 567 458.9Mbps        15 908           213   2.4Mbps
40     TOT        79 559 922.8Mbps        76 982 892.9Mbps        23 044         2 577  29.8Mbps
41     3          39 218 454.9Mbps        37 089 430.2Mbps         7 075         2 129  24.6Mbps
41     4          39 218 454.9Mbps        38 663 448.4Mbps        15 752           555   6.4Mbps
41     TOT        78 436 909.8Mbps        75 752 878.7Mbps        22 827         2 684  31.1Mbps
42     3          39 188 454.5Mbps        37 906 439.7Mbps         6 729         1 282  14.8Mbps
42     4          39 187 454.5Mbps        38 954 451.8Mbps        15 565           233   2.7Mbps
42     TOT        78 375 909.1Mbps        76 860 891.5Mbps        22 294         1 515  17.5Mbps
TOT    3       1 645 468 454.4Mbps     1 568 201 433.1Mbps       280 174        77 267  21.3Mbps
TOT    4       1 645 464 454.4Mbps     1 626 896 449.3Mbps       627 480        18 568   5.1Mbps
TOT    TOT     3 290 932 908.9Mbps     3 195 097 882.4Mbps       907 654        95 835  26.4Mbps
```

Stats show throughput of each stream and total throughput of both streams, Out-of-order packet count, Lost rate, latency, and jitter. 

1841
