## `/routing/bgp/session` 

**==> picture [516 x 110] intentionally omitted <==**

**----- Start of picture text -----**<br>
Read-only Property Description<br>name<br>Also, in this menu is located a session-specific set of commands.<br>Command Description<br>**----- End of picture text -----**<br>


955 

**==> picture [516 x 254] intentionally omitted <==**

**----- Start of picture text -----**<br>
clear Clear the session flags. For example, to be able to re-establish a session after the prefix limit is reached "limit-exceeded" flag must be<br>cleared. It can be done by specifying " flag " parameter, which is able to take the following values:<br>input-last-notification<br>limit-exceeded<br>output-last-notification<br>refused-cap-opt<br>stopped<br>dump-saved- Dump saved advertisements from specified BGP session in the *.pcap file. The filename to store data is set by " save-to " parameter.<br>advertisements<br>refresh Send route refresh to a specified BGP session. Is used to trigger re-sending all the routes from the remote peer. " address-family "<br>parameters allow specifying for which address family to send route refresh.<br>resend Resend prefixes to a specified BGP session. The command takes two parameters:<br>" address-family " - parameters allow specifying for which address family to resend prefixes.<br>" save-to " - the name of the pcap file where to dump resent messages, can be used for debugging purposes.<br>reset Reset specified BGP session.<br>stop Stop specified BGP session.<br>**----- End of picture text -----**<br>
