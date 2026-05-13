## Resolve host-name 

Many users are asking features to use DNS names instead of IP addresses for radius servers, firewall rules, etc. 

So here is an example of how to resolve the RADIUS server's IP. 

Let's say we have the radius server configured: 

```
/radius
add address=3.4.5.6 comment=myRad
```

And here is a script that will resolve the IP address, compare resolved IP with configured one, and replace it if not equal: 

```
/system script add name="resolver" source= {
:local resolvedIP [:resolve "server.example.com"];
:local radiusID [/radius find comment="myRad"];
:local currentIP [/radius get $radiusID address];
:if ($resolvedIP != $currentIP) do={
   /radius set $radiusID address=$resolvedIP;
   /log info "radius ip updated";
}
}
```

Add this script to the scheduler to run for example every 5 minutes 

```
/system scheduler add name=resolveRadiusIP on-event="resolver" interval=5m
```

Write simple queue stats in multiple files 

1115 

Let's consider queue namings are "some text.1" so we can search queues by the last number right after the dot. 

```
:local entriesPerFile 10;
:local currentQueue 0;
:local queuesInFile 0;
:local fileContent "";
#determine needed file count
:local numQueues [/queue simple print count-only] ;
:local fileCount ($numQueues / $entriesPerFile);
:if ( ($fileCount * $entriesPerFile) != $numQueues) do={
   :set fileCount ($fileCount + 1);
}
#remove old files
/file remove [find name~"stats"];
:put "fileCount=$fileCount";
:for i from=1 to=$fileCount do={
#create file
   /file print file="stats$i.txt";
#clear content
   /file set [find name="stats$i.txt"] contents="";
   :while ($queuesInFile < $entriesPerFile) do={
     :if ($currentQueue < $numQueues) do={
         :set currentQueue ($currentQueue +1);
         :put $currentQueue ;
         /queue simple
         :local internalID [find name~"\\.$currentQueue\$"];
         :put "internalID=$internalID";
         :set fileContent ($fileContent . [get $internalID target-address] . \
           " " . [get $internalID total-bytes] . "\r\n");
     }
     :set queuesInFile ($queuesInFile +1);
   }
   /file set "stats$i.txt" contents=$fileContent;
   :set fileContent "";
   :set queuesInFile 0;
}
```
