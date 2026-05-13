## Method 2 

It is possible to use the join and leave commands and make the PWR-Line devices automatically synchronize the network-key value. It is advised to use the leave command before using the join command to make sure a new network-key is randomly generated and the device is not part of any old network. 

```
/interface pwr-line leave pwr-line1
```

Then we can issue the join command. When doing so, the pairing sequence is enabled for 60 seconds, meaning you have to enable pairing mode on another device within 60 seconds for them to successfully pair. 

```
/interface pwr-line join pwr-line1
```
