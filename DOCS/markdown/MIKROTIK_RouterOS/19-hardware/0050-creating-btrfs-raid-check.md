## Creating Btrfs-RAID check 

It is extremely important for you to monitor the Btrfs-RAID array's health. One way you can do this is by using the script below as a working example: 

```
/system scheduler
add interval=1w30s name=BraidBalanceStartCall on-event=BraidBalanceStart policy=ftp,read,write,policy,test,
sniff start-date=1970-01-01 start-time=01:00:00
```

```
add interval=1w30s name=BraidScrubStartCall on-event=BraidScrubStart policy=ftp,read,write,policy,test,sniff
start-date=1970-01-01 start-time=02:00:00
```

```
add interval=2m name=BraidBalanceStatusCheckCall on-event=BraidBalanceStatus policy=ftp,read,write,policy,test,
sniff start-time=startup
```

```
add interval=2m name=BraidScrubStatusCheckCall on-event=BraidScrubStatus policy=ftp,read,write,policy,test,
sniff start-time=startup
```

```
add interval=30s name=BraidHealthCheckCall on-event=BraidHealthCheck policy=ftp,read,write,policy,test,sniff
start-time=startup
add interval=2m name=BraidReplaceStatusCheckCall on-event=BraidReplaceStatus policy=ftp,read,write,policy,test,
sniff start-time=startup
```

```
/system script
```

```
add dont-require-permissions=no name=BraidScrubStart owner=admin policy=ftp,read,write,policy,test,sniff
source=":global btrfsscrubstatuscheck;\
```

```
    \nif (\$btrfsscrubstatuscheck != \"started\") do={\
```

```
    \n  :set \$btrfsscrubstatuscheck (\$btrfsscrubstatuscheck \"started\");\
```

```
    \n  foreach i in=[/disk/btrfs/filesystem/find] do={ /disk/btrfs/filesystem/scrub-start \$i;\
    \n    :local temp [ /disk btrfs filesystem/get value-name=label \$i;]\
```

```
    \n    /log info message=\"INFO: Btrfs scrub process started on  \$temp\";\
    \n    :delay 3; \
    \n  }\
    \n}\
    \n"
add dont-require-permissions=no name=BraidBalanceStart owner=admin policy=ftp,read,write,policy,test,sniff
source=":global btrfsbalancestatuscheck;\
```

```
    \nif (\$btrfsbalancestatuscheck != \"started\") do={\
```

```
    \n:set \$btrfsbalancestatuscheck (\$btrfsbalancestatuscheck \"started\");\
    \n:local percentage;\
    \n:set \$percentage (\$percentage 50);\
    \n  foreach i in=[/disk/btrfs/filesystem/find] do={ /disk/btrfs/filesystem/balance-start data-
usage=\$percentage \$i;\
    \n    :local temp [ /disk btrfs filesystem/get value-name=label \$i;]\
    \n    /log info message=\"INFO: Btrfs balance process started on  \$temp\";\
    \n    :delay 3; \
    \n  }\
    \n}"
```

1685 

```
add dont-require-permissions=no name=BraidBalanceStatus owner=admin policy=ftp,read,write,policy,test,sniff
source=":global btrfsbalancestatuscheck;\
    \nif (\$btrfsbalancestatuscheck = \"started\") do={\
    \n:local arraycnt [/disk/btrfs/filesystem/print count-only as-value];\
    \n:local counter [:set \$counter (\$counter 0)];\
    \n:local counterdiff [:set \$counterdiff (\$counterdiff 0)];\
    \n  foreach i in=[/disk/btrfs/filesystem/find] do={ \
    \n    :local barray [ /disk btrfs filesystem/get value-name=balance-status  \$i;]\
    \n    :local temp [ /disk btrfs filesystem/get value-name=label \$i;]\
    \n    if ( \$barray != \"done\" and \$btrfsbalancestatuscheck = \"started\") do={\
    \n        /log info message=\"INFO: Btrfs current balance status on  \$temp is \$barray\";\
    \n    }\
    \n    if ( \$barray = \"done\" and \$btrfsbalancestatuscheck = \"started\") do={\
    \n      :set \$counter (\$counter +1);\
    \n      :set \$counterdiff (\$arraycnt - \$counter);\
    \n      if (\$counterdiff =1) do={\
    \n        /log info message=\"INFO: Btrfs balancing already done on \$counter arrays\";\
    \n      }\
    \n    }\
    \n    if ( \$counter = \$arraycnt) do={\
    \n      /log info message=\"INFO: Btrfs array balance status on  \$temp is \$barray \";\
    \n      :set \$btrfsbalancestatuscheck (\$btrfsbalancestatuscheck \"done\");\
    \n    }\
    \n  } \
    \n}"
add dont-require-permissions=no name=BraidScrubStatus owner=admin policy=ftp,read,write,policy,test,sniff
source=":global btrfsscrubstatuscheck;\
    \nif (\$btrfsscrubstatuscheck = \"started\") do={\
    \n:local arraycnt [/disk/btrfs/filesystem/print count-only as-value];\
    \n:local counter [:set \$counter (\$counter 0)];\
    \n:local counterdiff [:set \$counterdiff (\$counterdiff 0)];\
    \n  foreach i in=[/disk/btrfs/filesystem/find] do={ \
    \n    :local barray [ /disk btrfs filesystem/get value-name=scrub-status  \$i;]\
    \n    :local temp [ /disk btrfs filesystem/get value-name=label \$i;]\
    \n    if ( \$barray != \"done\" and \$btrfsscrubstatuscheck = \"started\") do={\
    \n      /log info message=\"INFO: Btrfs current scrub status on  \$temp is \$barray\";\
    \n    }\
    \n    if ( \$barray = \"done\" and \$btrfsscrubstatuscheck = \"started\") do={\
    \n      :set \$counter (\$counter +1);\
    \n      :set \$counterdiff (\$arraycnt - \$counter);\
    \n      if (\$counterdiff =1) do={\
    \n        /log info message=\"INFO: Btrfs scrubbing already done on \$counter arrays\";\
    \n      }\
    \n    }\
    \n    if ( \$counter = \$arraycnt ) do={\
    \n      /log info message=\"INFO: Btrfs array scrub status on  \$temp is \$barray \";\
    \n      :set \$btrfsscrubstatuscheck (\$btrfsscrubstatuscheck \"done\");\
    \n    }\
    \n  } \
    \n}"
```

```
add dont-require-permissions=no name=BraidReplaceStatus owner=admin policy=ftp,read,write,policy,test,sniff
source=":global btrfsreplacestatuscheck;\
```

```
    \nif (\$btrfsreplacestatuscheck = \"started\") do={\
```

```
    \n:local arraycnt [/disk/btrfs/filesystem/print count-only as-value];\
    \n:local counter [:set \$counter (\$counter 0)];\
```

```
    \n:local counterdiff [:set \$counterdiff (\$counterdiff 0)];\
```

```
    \n  foreach i in=[/disk/btrfs/filesystem/find] do={ \
    \n    :local barray [ /disk btrfs filesystem/get value-name=replace-status  \$i;]\
    \n    :local temp [ /disk btrfs filesystem/get value-name=label \$i;]\
```

```
    \n    :local multipleprofiles [ /disk btrfs filesystem/get value-name=spaces \$i; ]\
    \n    if ( \$barray ~ \"working\" and \$btrfsreplacestatuscheck = \"started\") do={\
    \n      /log info message=\"INFO: Btrfs current replace status on  \$temp is \$barray\";\
    \n    }\
    \n    if ( \$barray ~ \"done\" and \$btrfsreplacestatuscheck = \"started\" and \$multipleprofiles~\"
single\" ) do={\
```

```
    \n      /log info message=\"INFO: Braid balance after replace-device  started on  \$temp\";\
    \n         if (\$btrfsbalancestatuscheck!=\"started\") do={\
    \n             /disk/btrfs/filesystem/balance-start \$temp;\
```

```
    \n             :set \$btrfsbalancestatuscheck (\$btrfsbalancestatuscheck \"started\");\
    \n         }\
    \n    }\
```

1686 

```
    \n    if ( \$barray = \"done\" and \$btrfsreplacestatuscheck = \"started\") do={\
    \n      :set \$counter (\$counter +1);\
    \n      :set \$counterdiff (\$arraycnt - \$counter);\
    \n      if (\$counterdiff =1) do={\
    \n        /log info message=\"INFO: Btrfs replace already done on \$counter arrays\";\
    \n      }\
    \n    }\
    \n    if ( \$counter = \$arraycnt ) do={\
    \n      /log info message=\"INFO: Btrfs array replace status on  \$temp is \$barray \";\
    \n      :set \$btrfsreplacestatuscheck (\$btrfsreplacestatuscheck \"done\");\
    \n    }\
    \n  } \
    \n}\
    \n:set \$btrfsreplacestatuscheck (\$btrfsreplacestatuscheck \"started\");"
add dont-require-permissions=no name=BraidHealthCheck owner=admin policy=ftp,read,write,policy,test,sniff
source="foreach i in=[/disk/btrfs/filesystem/find] do={ \
    \n:local sysadmin; \
    \n\
    \n:set  \$sysadmin \"<servername@domain.tld>\";\
    \n\
    \n:local temp [ /disk/btrfs/filesystem/get value-name=label \$i;]\
    \n:local haserror [/disk/btrfs/filesystem/get value-name=about \$i; ]\
    \n:local hasmissing [ /disk/btrfs/filesystem/get value-name=devs \$i; ]\
    \n:local hasmultiprofile [ /disk/btrfs/filesystem/get value-name=spaces \$i; ]\
    \n:local replacestatus [ /disk/btrfs/filesystem/get value-name=replace-status \$i; ]\
    \n:local multiplediskarray [:len [/disk btrfs filesystem find where label=\$temp and dev-ids~\"2\"];]\
    \n\
    \n  if ( \$hasmissing~\"missing\" and ([:len \$replacestatus]=0)) do= {\
    \n    /log info message=\"ERROR: BtrfsHealthCheck found missing array member on \$temp\";\
    \n    /tool e-mail send to= \$sysadmin  subject=([/system identity get name].\" BtrfsHealthCheck found
missing array member\") body=(\"Btrfs array where found missing array member on \" .\$temp . \"   \");\
    \n   :delay 19; \
    \n  }\
    \n\
    \n  if ( \$multiplediskarray > 0 and \$hasmultiprofile~\"single\") do= {\
    \n    /log info message=\"ERROR: BtrfsHealthCheck found multiprofile on \$temp array. To start balance
process, run  /disk btrfs filesystem balance-start \$temp command \";\
    \n    /tool e-mail send to= \$sysadmin  subject=([/system identity get name].\" BtrfsHealthCheck found
multiprofile on \" .\$temp. \" array.\") body=(\"Btrfs array where found with multiprofile status on \" .\$temp
. \"To start balance process, run once\
    \_ /disk btrfs filesystem balance-start \" .\$temp. \" command \");\
    \n   :delay 19; \
    \n  }  \
    \n\
    \n  if (([:len \$haserror]) > 0 ) do= {\
    \n    /log info message=\"ERROR: BtrfsHealthCheck found errors on \$temp\";\
    \n    /tool e-mail send to= \$sysadmin  subject=([/system identity get name].\" BtrfsHealthCheck found
errors\") body=(\"Btrfs array where found errors on \" .\$temp . \"   \");\
    \n    :delay 20; \
    \n  }\
    \n}\
    \n"
```

You also need to adjust e-mail server settings on your RouterOS device: 

```
/tool e-mail
```

```
set from=<raidcheck@domain.tld> port=587 server=smtp.domain.com tls=starttls
```

**==> picture [13 x 13] intentionally omitted <==**

Make sure you adjust the e-mail settings with the required settings on your e-mail server. Remember to adjust the e-mail address in the script above. 

Creating subvolumes 

1687 

The main benefit of creating subvolumes is to organize data on your Btrfs main (root) subvolume. Consider subvolumes as folders with features of a partition, while still sharing the total disk space between all subvolumes. You can later use these subvolumes for much more advanced tasks and it is recommended to create subvolumes when you have large amounts of different types of data, especially that requires frequent backups. Follow the guide to setup a few example subvolumes: 

**==> picture [13 x 13] intentionally omitted <==**

Subvolumes are most useful when used together with snapshots. Be sure to check out the snapshot feature as well. 

1.  Find the disk name of your disk that you want to use as your Btrfs disk: 

```
/disk print
```

**==> picture [13 x 13] intentionally omitted <==**

In this example, the disk used is going to be called `<disk-name-1>` , make sure you replace the placeholder with your actual disk name! 

2.  Format the disk to Btrfs, in this case `<disk-name-1>` : 

```
/disk format <disk-name-1> file-system=btrfs
```

3.  Add a label for the Btrfs disk for simplicity: 

```
/disk/btrfs/filesystem set [find where present-devs=<disk-name-1>] label=BtrfsDisk
```

4.  You can also change the Btrfs disk mount point for simplicity: 

```
/disk set <disk-name-1> mount-point-template=BtrfsDisk
```

5.  Create a new subvolume called `Documents` to `BtrfsDisk` : 

```
/disk/btrfs/subvolume/add name=Documents fs=BtrfsDisk
```

**==> picture [13 x 13] intentionally omitted <==**

Subvolumes are also snapshots. You might encounter both of these names in various menus. In simple terms, snapshots are subvolumes created at a specific time and contains data from that time point. 

6.  Create another subvolume called `Photos` to `BtrfsDisk` : 

```
/disk/btrfs/subvolume/add name=Photos fs=BtrfsDisk
```

7.  You can view the currently available subvolumes: 

```
/disk/btrfs/subvolume/print
```

8.  You can now access these subvolumes as `/BtrfsDisk/Documents` and `/BtrfsDisk/Photos`
