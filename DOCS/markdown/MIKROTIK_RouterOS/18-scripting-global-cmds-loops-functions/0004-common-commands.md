## Common commands 

The following commands are available from most sub-menus: 

**==> picture [509 x 229] intentionally omitted <==**

**----- Start of picture text -----**<br>
Command Syntax Description<br>add add  add new item<br><param>=<value>.<br>.<param>=<value><br>remove remove <id> remove selected item<br>enable enable <id> enable selected item<br>disable disable <id> disable selected item<br>set set <id>  change selected items parameter, more than one parameter can be specified at the time. The parameter can<br><param>=<value>. be unset by specifying '!' before the parameter.<br>.<param>=<value><br>Example:<br>/ip firewall filter add chain=blah action=accept protocol=tcp port=123 nth=4,2<br>print<br>set 0 !port chain=blah2 !nth protocol=udp<br>get get <id>  get the selected item's parameter value<br><param>=<value><br>**----- End of picture text -----**<br>


1105 

**==> picture [509 x 140] intentionally omitted <==**

**----- Start of picture text -----**<br>
print print  print menu items. Output depends on the print parameters specified. The most common print parameters are<br><param><param>= described here<br>[<value>]<br>export export  export configuration from the current menu and its sub-menus (if present). If the file parameter is specified<br>[file=<value>] output will be written to the file with the extension '.rsc', otherwise the output will be printed to the console.<br>Exported commands can be imported by import command<br>edit edit <id>  edit selected items property in the built-in text editor<br><param><br>find find  Returns list of internal numbers for items that are matched by given expression. For example:   :put [<br><expression> /interface find name~"ether"]<br>**----- End of picture text -----**<br>
