## Prefix Operators 

**==> picture [516 x 135] intentionally omitted <==**

**----- Start of picture text -----**<br>
Operator Description<br>in Return true if the prefix is the subnet of the provided network. If an operator is used to match prefixes from the address list (e.g " dst in<br>list_name "), then it will match only the exact prefix.<br>!= Return true if the prefix is not equal to the provided value<br>== Return true if the prefix is equal to the provided value<br>Address lists by design are matching host address which menas that it will match also  /32 prefix that belongs to any range from the address list.<br>Workaround to exclude /32  prefixes from being advertised is to use dst-len " if (dst in list_name && dst-len < 32) {} "<br>**----- End of picture text -----**<br>
