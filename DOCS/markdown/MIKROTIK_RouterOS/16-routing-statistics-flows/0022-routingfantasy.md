## /routing/fantasy 

Fantasy menu is a fancy way to generate large amount of routes for testing purposes. Main benefits of this approach compared to script is the generation speed and simplicity. It is easy to remove all fantasy generated routes just by disabling fantasy rule. 

Fantasy uses random generator from hashed route sequence number, seed and other parameters. 

**==> picture [516 x 399] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>comment  (string)<br>count  (integer:[0..4294967295]) How many routes to generate.<br>dealer-id  (start-[end]:: integer:<br>[0..4294967295])<br>disabled  (yes | no) ID reference is not used.<br>dst-address (Prefix) Prefix from which route will be generated.<br>gateway  (string)<br>instance-id  (start-[end]:: integer:<br>[0..4294967295])<br>name  (string) Reference name<br>offset  (integer:[0..4294967295]) Route sequence number offset<br>prefix-length  (start-[end]:: intege Prefix length for generated route (can be specified as integer range). For example dst-address 192.168.0.0/16 and<br>r:[0..4294967295] ) prefix-length 24 will generate /24 routes from 192.168.0.0/16 subnet.<br>priv-offset  (start-[end]:: integer:<br>[0..4294967295])<br>priv-size  (start-[end]:: integer:<br>[0..100000])<br>scope  (start-[end]:: integer: [0.. Scope to be set, can be set as range<br>255])<br>seed  (string) Random generator seed<br>target-scope  (start-[end]:: intege Target scope to be set, can be set as range<br>r: [0..255])<br>use-hold  (yes | no)<br>**----- End of picture text -----**<br>


959
