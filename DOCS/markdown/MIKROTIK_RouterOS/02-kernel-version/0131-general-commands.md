## General Commands 

Some commands are common to nearly all menu levels, namely: add , edit , find , move , print , remove , set , reset , export , get , enable , disable , and comment . These commands have similar behavior throughout different menu levels. 

- add - this command usually has all the same arguments as set , except the item number argument. It adds a new item with the values you have specified, usually at the end of the item list, in places where the order of items is relevant. There are some required properties that you have to supply, such as the interface for a new address, while other properties are set to defaults unless you explicitly specify them. 

   - Common Parameters 

      - copy-from - Copies an existing item. It takes the default values of a new item's properties from another item. If you do not want to make an exact copy, you can specify new values for some properties. When copying items that have names, you will usually have to give a new name to a copy 

      - place-before - places a new item before an existing item with a specified position. Thus, you do not need to use the move command after adding an item to the list. 

      - disabled - controls disabled/enabled state of the newly added item(-s) 

      - comment - holds the description of a newly created item 

   - Return Values 

add command returns the internal number of item it has added 

- edit - this command is associated with the set command. It can be used to edit values of properties that contain a large amount of text, such as scripts, but it works with all editable properties. Depending on the capabilities of the terminal, either a fullscreen editor or a single-line editor is launched to edit the value of the specified property. The edit field for console scripts is limited to 30 thousand characters. 

- find - The find command has the same arguments as set, plus the flag arguments like disabled or active that take values yes or no depending on the value of the respective flag. To see all flags and their names, look at the top of the print command's output. The find command returns internal numbers of all items that have the same values of arguments as specified. 

- move - changes the order of items in the list. 

   - Parameters 

first argument specifies the item(-s) being moved. 

   - the second argument specifies the item before which to place all items being moved (they are placed at the end of the list if the second argument is omitted). 

- print - shows all information that's accessible from a particular command level. Thus, /system clock print shows the system date and time, /ip route 

- print shows all routes, etc. If there's a list of items in the current level and they are not read-only, i.e. you can change/remove them (an example of a read-only item list is /system history, which shows a history of executed actions), then print command also assigns numbers that are used by all commands that operate with items in this list. 

Common Parameters 

   - from - show only specified items, in the same order in which they are given. 

   - where - show only items that match specified criteria. The syntax of where the property is similar to the find command. 

   - brief - forces the print command to use tabular output form 

   - detail - forces the print command to use property=value output form count-only - shows the number of items 

   - file - prints the contents of the specific submenu into a file on the router. 

   - interval - updates the output from the print command for every interval of seconds. 

   - oid - prints the OID value for properties that are accessible from SNMP 

   - without-paging - prints the output without stopping after each screenful. 

- remove - removes specified item(-s) from a list. 

set - allows you to change values of general parameters or item parameters. The set command has arguments with names corresponding to values you can change. Use "F1" or double [Tab] to see a list of all arguments. If there is a list of items in this command level, then "set" has one action argument that accepts the number of item (or list of numbers) you wish to set up. This command does not return anything. 

- reset - reset parameters to default values. You can also include parameters with arguments in the same command, allowing you to reset and configure settings at the same time. 

- export - export configuration from the current menu and its sub-menus (if present). If the file parameter is specified output will be written to the file with the extension '.rsc', otherwise the output will be printed to the console. More information regarding export command. get - gets the selected item's parameter value and does not display it in the terminal by default. (if used in combination with :put command, displays the retrived value in Terminal, for example :put [system/resource/get version] will show version of RouterOS installed on the device) enable - enables selected item. 

disable - disables selected item. 

comment - allows you to comment selected item. 

75 

**==> picture [13 x 13] intentionally omitted <==**

You can combine commands, here are two variants of the same command that will place a new firewall filter entry, by looking up the comment: /ip firewall/filter/add chain=forward place-before=[find where comment=CommentX] /ip/firewall/filter/add chain=forward place-before="CommentX"
