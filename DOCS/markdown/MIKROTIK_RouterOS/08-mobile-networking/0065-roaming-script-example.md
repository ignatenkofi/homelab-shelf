## Roaming script example 

Now create a script that will run with a scheduler. This script will go through a few key points: 

Check if the LTE interface is initialized (shown in `/interface lte` ), otherwise, try a power reset 

Check if an LTE connection is established (the interface is in a "running" state), otherwise create a log entry and simply wait for the next scheduler Read the currently used LTE slot and decide whether to change SIM slots based on roaming status 

Let's call this script "roamingScript", and see below the source: 

831 

```
{
# Setup and read current values, "up" SIM slot will be used for roaming, "down" for home network
:global simSlot [/system routerboard sim get sim-slot]
:global timeoutLTE 60
:global timeoutConnect 60
# Wait for LTE to initialize for maximum "timeoutLTE" seconds
:local i 0
:local isLTEinit false
:while ($i<$timeoutLTE) do={
   :foreach n in=[/interface lte find] do={:set $isLTEinit true}
   :if ($isLTEinit=true) do={
       :set $i $timeoutLTE
   }
   :set $i ($i+1)
   :delay 1s
}
# Check if LTE is initialized, or try power-reset the modem
:if ($isLTEinit=true) do={
   # Wait for LTE interface to connect to mobile network for maximum "timeoutConnet" seconds
   :local isConnected false
   :set $i 0
   :while ($i<$timeoutConnect) do={
       :if ([/interface lte get [find name="lte1"] running]=true) do={
           :set $isConnected true
           :set $i $timeoutConnect
       }
       :set $i ($i+1)
       :delay 1s
   }
   # Check if LTE is connected
   if ($isConnected=true) do={
       :local Info [/interface lte monitor lte1 once as-value]
       :local isRoaming ($Info->"roaming")
       # Check which SIM slot is used
       :if ($simSlot="down") do={
           # If "down" (home) slot, check roaming status
           :if ($isRoaming=true) do={
               :log info message="Roaming detected, switching to SIM UP (Roaming)"
               /system routerboard sim set sim-slot=up
           }
       } else={
           # Else "up" (roaming) slot, check roaming status
           :if (!$isRoaming=true) do={
               :log info message="Not roaming, switching to SIM DOWN (Home)"
               /interface lte settings set sim-slot=down
           }
       }
   } else={
       :log info message="LTE interface did not connect to network, wait for next scheduler"
   }
} else={
   :log info message="LTE modem did not appear, trying power-reset"
   /system routerboard usb power-reset duration=5s
}
}
```
