## Same priority 

if all, or some ports will have the same poe-priority, then port with the lowest port number will have higher priority 

**==> picture [13 x 13] intentionally omitted <==**

/interface ethernet poe set ether2 poe-priority=10 /interface ethernet poe set ether3 poe-priority=10 /interface ethernet poe set ether4 poe-priority=10 /interface ethernet poe set ether5 poe-priority=10 

In this example, if the total PoE-Out limit is reached ether5 will be turned off first, then ether4 then ether3 as all of these ports have same poe priority.
