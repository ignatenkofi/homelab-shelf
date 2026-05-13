## print parameters 

Several parameters are available for print command: 

**==> picture [509 x 206] intentionally omitted <==**

**----- Start of picture text -----**<br>
Parameter Description Example<br>append<br>as-value print output as an array of parameters and its values :put [/ip address print as-<br>value]<br>brief print brief description<br>detail print detailed description, the output is not as readable as brief output but may be useful<br>to view all parameters<br>count-only print only count of menu items<br>file print output to a file<br>follow print all current entries and track new entries until ctrl-c is pressed, very useful when  /log print follow<br>viewing log entries<br>follow-only print and track only new entries until ctrl-c is pressed, very useful when viewing log entries /log print follow-only<br>**----- End of picture text -----**<br>


1106 

**==> picture [509 x 175] intentionally omitted <==**

**----- Start of picture text -----**<br>
from print parameters only from specified item /user print from=admin<br>interval continuously print output in a selected time interval, useful to track down changes where  f /interface print interval=2<br>ollow is not acceptable<br>terse show details in a compact and machine-friendly format<br>value-list show values single per line (good for parsing purposes)<br>without- If the output does not fit in the console screen then do not stop, print all information in one<br>paging piece<br>where expressions followed by where parameters can be used to filter outmatched entries /ip route print where<br>interface="ether1"<br>about returns entries that have the "about" parameter, such as "managed by CAPsMAN  /interface wifi print where<br>"information or warnings about<br>**----- End of picture text -----**<br>


More than one parameter can be specified at a time, for example, `/ip route print count-only interval=1 where interface="ether1"`
