## The Things Network 

Once you have installed the lora package on your router and created an account on `The Things Network you can set up a running gateway` 

Login into your account and go to Console and select Gateways 

**==> picture [505 x 112] intentionally omitted <==**

Select register gateway and fill in the blank spaces. Gateway EUI can be found in your lora interface 

**==> picture [505 x 339] intentionally omitted <==**

You will have to manually add the Network Servers, or you can upgrade your router to the stable version 6.48.2 and these servers will be added automatically (highly recommended) 

https://wiki.mikrotik.com/wiki/Manual:Upgrading_RouterOS 

1624 

**==> picture [505 x 154] intentionally omitted <==**

/lora servers 

add address=eu1.cloud.thethings.industries down-port=1700 name="TTS Cloud (eu1)" up-port=1700 add address=nam1.cloud.thethings.industries down-port=1700 name="TTS Cloud (nam1)" up-port=1700 add address=au1.cloud.thethings.industries down-port=1700 name="TTS Cloud (au1)" up-port=1700 

**==> picture [505 x 239] intentionally omitted <==**

After everything is filled press Register Gateway at the bottom of the page. If you have set everything accordingly to the previous steps you should see that your lora gateway is now connected 

**==> picture [505 x 51] intentionally omitted <==**

At this point everything is set and you have a working lora gateway. You can monitor incoming packets in Traffic section 

1625 

**==> picture [505 x 298] intentionally omitted <==**

**==> picture [505 x 308] intentionally omitted <==**

*Later this year, The Things Network will be migrating to a new version of network server, called The Things Stack. 

1626
