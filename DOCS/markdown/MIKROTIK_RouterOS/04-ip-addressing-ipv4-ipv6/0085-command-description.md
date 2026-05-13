## Command description 

/cancel optional argument: =tag=tag of command to cancel, without it, cancels all running commands does not cancel itself all canceled commands are interrupted and in the usual case generate '!trap' and '!done' responses please note that /cancel is separate command and can have its own unique '.tag' parameter, that is not related to '=tag' argument of this command listen listen command is available where console print command is available, but it does not have the expected effect everywhere (i.e. may not work) "!re" sentences are generated as something changes in a particular item list when an item is deleted or disappears in any other way, the '!re' sentence includes the value '=.dead=yes' This command does not terminate. To terminate it, use /cancel command. getall getall command is available where console print command is available (getall is an alias for print). replies contain =.id=Item internal number property. print API print command differs from the console counterpart in the following ways: where an argument is not supported. Items can be filtered using query words (see below). 

198 

- .proplist argument is a comma-separated list of property names that should be included for the returned items. returned items may have additional properties. 

   - order of returned properties is not defined. 

   - if a list contains duplicate entries, handling of such entries is not defined. 

   - if a property is present in ".proplist", but absent from the item, then that item does not have this property value (?name will evaluate to false for that item). 

   - if ".proplist" is absent, all properties are included as requested by the print command, even those that have slow access time (such as file contents and performance counters). Thus the use of .proplist is encouraged. The omission of .proplist may have a high-performance penalty if the "=detail=" argument is set.
