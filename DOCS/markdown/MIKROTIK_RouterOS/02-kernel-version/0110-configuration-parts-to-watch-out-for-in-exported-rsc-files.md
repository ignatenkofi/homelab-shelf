## Configuration parts to watch out for in exported .rsc files 

Things that should be removed from export files that were created with "/export", before attempting import on a new device. 

Interface renaming conflicts with the default ethernet naming scheme. 

```
/interface ethernet
set [ find default-name=ether5 ] auto-negotiation=no name=ether1-gateway
set [ find default-name=ether6 ] name=ether2
set [ find default-name=ether7 ] name=ether3
set [ find default-name=ether8 ] name=ether4
set [ find default-name=ether1 ] name=ether5
set [ find default-name=ether2 ] name=ether6
set [ find default-name=ether3 ] name=ether7
set [ find default-name=ether4 ] name=ether8
```

In older versions "export" default entries might show with "add" instead of the "set" command. That should be edited before import to avoid errors. Check if the total number of physical interfaces count matches the new and old devices. If there are some missing that will end up in error during . rsc import. 

In case of problematic import, attempt the following: 

Use the dry-run parameter to simulate the import without making any configuration changes. This helps in catching syntax errors. This option is only available in verbose mode. 

Reset the configuration on that device. 

Run the import command again with the "verbose=yes" argument. It will also stop the import process on a problem that you already encountered, but will also show the place where the export failed. This way shows you the place where things need to be edited in the .rsc import file.
