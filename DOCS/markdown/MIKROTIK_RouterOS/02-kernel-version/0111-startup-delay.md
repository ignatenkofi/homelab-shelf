## Startup delay 

If your configuration relies on interfaces that might not yet have started up upon command execution, it is suggested to introduce delays or to monitor until all needed interfaces are available. This example script allows you to set how many interfaces you are expecting, and how long to wait until they become available: 

```
{
:local i 0
#Number of interfaces. It is necessary to reconfigure this number for each device (/interface print count-only)
:local x 10
#Max time to wait
:local t 30
while ($i < $t && [:len [/interface find]] < $x) do={
:put $i
:set $i ($i + 1)
:delay 1
}
if ($i = $t) do={
:log warning message="Could not load all physical interfaces"
} else={
#Rest of your script
}
}
```

61 

The above script will wait until there are 10 interfaces visible, or 30 seconds. If there are no 10 interfaces at this time, it will put a message in the log. Modify the variables according to your needs.
