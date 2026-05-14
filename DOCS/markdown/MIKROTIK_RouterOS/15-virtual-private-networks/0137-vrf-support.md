## VRF support 

Support starting from 7.17 version is added, and couple changes introduced in configuration, if you use latest version, please refer to this example: 

Server side configuration: 

```
      /interface ovpn-server server
        add disabled=no certificate=yourcert auth=sha1 cipher=aes128-cbc require-client-certificate=yes
protocol=tcp name=ovpn-server1 vrf=main
```

1249
