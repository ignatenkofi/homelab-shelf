## Flow Identifiers 

target (multiple choice: IP address/netmask or interface): Target is to be viewed from perspective of the target. If you want to limit your users' upload capability, set "target upload". 

Each of these two properties can be used to determine which direction is target upload and which is download. Be careful to configure both of these options for the same queue - in case they will point to opposite directions queue will not work. If neither value of target nor of interface is specified, the queue will not be able to make the difference between upload and download and will limit all traffic twice.
