## Failover script example 

Now create a script that will run with a scheduler. This script will go through a few key points: 

Check if the LTE interface is initialized (shown in `/interface lte` ), otherwise, try a power reset Check if an LTE connection is established (the interface is in a "running" state), otherwise, create a log entry and simply wait for the next scheduler Read the currently used LTE slot and make a decision whether to change SIM slots based on interface status 

Note: Keep in mind that the SIM slot will only be changed if the current one is not able to connect to the network if you need to switch back to the main SIM card you need to schedule another action that does it at a certain time. It is not possible to know if the other SIM card is in service without switching back to it. 

Let's call this script "failoverScript", and see below the source: 

832 

```
{
# Setup and read current values
:global simSlot [/system routerboard modem get sim-slot]
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
   if ($isConnected=false) do={
   # Check which SIM slot is used
       :if ($simSlot="down") do={
           # If "down" slot, switch to up
       :log info message="LTE down, switching slot to UP"
           /interface lte settings set sim-slot=up
   }
       :if ($simSlot="up") do={
           # If "up" slot, switch to down
       :log info message="LTE down, switching slot to DOWN"
           /interface lte settings set sim-slot=down
           }
       } else={
           # Else "running"
           :if ($isConnected=true) do={
               :log info message="LTE UP"
           } else={
       :log info message="LTE interface did not connect to network, wait for next scheduler"
       }
   }
   } else={
   :log info message="LTE modem did not appear, trying power-reset"
   /system routerboard usb power-reset duration=5s
}
}
```
