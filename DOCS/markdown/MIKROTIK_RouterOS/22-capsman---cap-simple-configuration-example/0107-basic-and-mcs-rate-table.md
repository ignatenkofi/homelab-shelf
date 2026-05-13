## Basic and MCS Rate table 

Default basic and supported rates, depending on selected band 

**==> picture [366 x 219] intentionally omitted <==**

**----- Start of picture text -----**<br>
band basic rates basic-HT-mcs basic-VHT-mcs VHT-mcs HT-mcs supported rates<br>2.4ghz-b 1 - - - - 1-11<br>2.4ghz-onlyg 6 - - - - 1-11,6-54<br>2.4ghz-onlyn 6 0-7 - - 0-23 1-11,6-54<br>2.4ghz-b/g 1-11 - - - - 1-11,6-54<br>2.4ghz-b/g/n 1-11 none - - 0-23 1-11,6-54<br>2.4ghz-g/n 6 none - - 0-23 6-54<br>2.4ghz-g-turbo 6 - - - - 6-54<br>5ghz-a 6 - - - - 6-54<br>5ghz-a/n 6 none - - 0-23 6-54<br>5ghz-onlyn 6 0-7 - - 0-23 6-54<br>5ghz-a/n/ac 6 none none 0-9 0-23 6-54<br>5ghz-onlyac 6 none 0-7 0-9 0-23 6-54<br>**----- End of picture text -----**<br>


Used settings when rate-set=configured 

**==> picture [403 x 99] intentionally omitted <==**

**----- Start of picture text -----**<br>
band used settings<br>2.4ghz-b basic-b, supported-b<br>2.4ghz-b/g, 2.4ghz-onlyg basic-b, supported-b, basic-a/g, supported-a/g<br>2.4ghz-onlyn, 2.4ghz-b/g/n basic-b, supported-b, basic-a/g, supported-a/g, ht-basic-mcs, ht-supported-mcs<br>2.4ghz-g/n basic-a/g,supported-a/g,ht-basic-mcs,ht-supported-mcs<br>**----- End of picture text -----**<br>


1398 

5ghz-a basic-a/g,supported-a/g 5ghz-a/n, 5ghz-onlyn basic-a/g,supported-a/g,ht-basic-mcs,ht-supported-mcs 5ghz-a/n/ac, 5ghz-onlyac basic-a/g,supported-a/g,ht-basic-mcs,ht-supported-mcs,vht-basic-mcs,vht-supported-mcs 

Settings independent from rate-set : 

1.  allowed mcs depending on number of chains: 

1 chain: 0-7 

2 chains: 0-15 

3 chains: 0-23 2.  if standard channel width (20Mhz) is not used, then 2ghz modes (except 2.4ghz-b) are not using b rates (1-11)
