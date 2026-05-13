## Method 1 

There are two ways to set the same network-key on different devices. You can either use the network-key parameter which is a hashed version of networkpassword parameter. Or use the network-password parameter and let the router apply the hash on a human-readable string. 

For example: 

```
/interface pwr-line configure pwr-line1 network-password=mynetwork
```
