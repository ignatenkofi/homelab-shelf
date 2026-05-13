## Detect new log entry 

This script is checking if a new log entry is added to a particular buffer. 

In this example we will use PPPoE logs: 

```
/system logging action
add name="pppoe"
/system logging
add action=pppoe topics=pppoe,info,!ppp,!debug
```

Log buffer will look similar to this one: 

```
[admin@mainGW] > /log print where buffer=pppoe
13:11:08 pppoe,info PPPoE connection established from 00:0C:42:04:4C:EE
```

Now we can write a script to detect if a new entry is added. 

1119 

```
:global lastTime;
:global currentBuf [ :toarray [ /log find buffer=pppoe  ] ] ;
:global currentLineCount [ :len $currentBuf ] ;
:global currentTime [ :totime [/log get [ :pick $currentBuf ($currentLineCount -1) ] time   ] ];
:global message "";
:if ( $lastTime = "" ) do={
        :set lastTime $currentTime ;
        :set message [/log get [ :pick $currentBuf ($currentLineCount-1) ] message];
} else={
        :if ( $lastTime < $currentTime ) do={
                :set lastTime $currentTime ;
                :set message [/log get [ :pick $currentBuf ($currentLineCount-1) ] message];
        }
}
```

After a new entry is detected, it is saved in the "message" variable, which you can use later to parse log messages, for example, to get the PPPoE client's mac addresses.
