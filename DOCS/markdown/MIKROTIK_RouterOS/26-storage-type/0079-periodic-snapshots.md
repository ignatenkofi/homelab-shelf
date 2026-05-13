## Periodic snapshots 

Snapshots can be used to save changes of your files in a set interval. Snapshots are most useful when you have a reliable interval at which data is copied so you can always revert your data to a previous state. Below you can find a ready-to-use script that creates periodic snapshots: 

```
/system/scheduler
```

```
add interval=1d name=BraidSnapshotStartCall on-event=BraidSnapshotStart policy=ftp,read,write,policy,test,sniff
start-date=1970-01-01 start-time=23:15:00
```

```
add interval=1d name=BraidSnapshotCleanUpStartCall on-event=BraidSnapshotCleanUpStart policy=ftp,read,write,
policy,test,sniff start-date=1970-01-01 start-time=23:00:00
```

```
add interval=3m name=SystemBackupStartCall on-event=SystemBackupStart policy=ftp,read,write,policy,test,sniff
start-time=startup
```

```
/system/script
```

```
add dont-require-permissions=no name=SystemBackupStart owner=admin policy=ftp,read,write,policy,test,sniff
source=":global systembackupstatuscheck;\
```

```
    \n:global systembackupdirectoryname; \
```

```
    \n:local sysadmin;\
```

```
    \n\
```

```
    \n:set \$sysadmin ( \$sysadmin \"servername@domain.tld\" );\
```

1696 

```
    \n:set \$systembackupdirectoryname (\$systembackupdirectoryname \"Braid17-20/@system-backup/\");\
    \n\
    \n if (\$systembackupstatuscheck != \"started\") do={\
    \n         :set \$systembackupstatuscheck (\$systembackupstatuscheck \"started\");\
    \n               :local datentime ([/system/clock/get date].\"-\".[/system/clock/get time]);\
    \n               :local servername ([/system identity get name]);\
    \n               /system backup save name=\"\$systembackupdirectoryname\$servername-\$datentime\";\
    \n\
    \n        :set \$systembackupstatuscheck (\$systembackupstatuscheck \"done\");\
    \n} else={\
    \n         /log info message=\"ERROR: Cannot create  \$systembackupdirectoryname\$servername-\$datentime.
Set manually :set systembackupstatuscheck (systembackupstatuscheck \\\"done\\\");\";\
    \n}\
    \n"
add dont-require-permissions=no name=BraidSnapshotStart owner=admin policy=ftp,read,write,policy,test,sniff
source=":global btrfssnapshotstatuscheck;\
    \n:global snapshotdirectoryname; \
    \n:local maxusedspace;\
    \n:local sysadmin;\
    \n\
    \n:set \$maxusedspace ( \$maxusedspace 80 );\
    \n:set \$sysadmin ( \$sysadmin \"<servername@domain.tld>\" );\
    \n:set \$snapshotdirectoryname (\$snapshotdirectoryname \"@snapshots\");\
    \n\
    \n if (\$btrfssnapshotstatuscheck != \"started\") do={\
    \n         :set \$btrfssnapshotstatuscheck (\$btrfssnapshotstatuscheck \"started\");\
    \n         foreach i in=[/disk/btrfs/filesystem/find] do={ \
    \n           :local temp [ /disk btrfs filesystem/get value-name=label \$i;]\
    \n           :local valueofusedspace [/disk print count-only where use>=\$maxusedspace and fs-label=\$temp];
\
    \n           if ( \$valueofusedspace=0) do={\
    \n            foreach j in=[/disk btrfs subvolume/find  where fs=\$temp and top-level!
=\$snapshotdirectoryname and fullname!=\$snapshotdirectoryname ] do={\
    \n               :local parentvar [ /disk/btrfs/subvolume/get value-name=name \$j; ];\
    \n               :local datentime ([/system/clock/get date].\"-\".[/system/clock/get time]);\
    \n                  /disk btrfs subvolume add read-only=yes fs=\"\$temp\" parent=\"\$parentvar\" name=\"
\$snapshotdirectoryname/\$temp-\$parentvar-\$datentime\";\
    \n                   /log info message=\"INFO: Braid snapshot created for  \$temp subvolume \$parentvar
snapshotname  \$snapshotdirectoryname/\$temp-\$parentvar-\$datentime\";\
    \n                :delay 1;\
    \n            }\
    \n          } else={\
    \n                   /log info message=\"ERROR: Snapshot was not created for safety reason.  Braid array
\$temp used space exceeded \$maxusedspace %. Add more disks or cleanup storage.\"; \
    \n                   /tool e-mail send to= \$sysadmin  subject=([/system identity get name].\" ERROR: Braid
snapshot was not created \") body=(\"Snapshot was not created for safety reason.  Braid array \" .\$temp. \"
used space exceeded \" .\$max\
    usedspace. \" % Add more disks or cleanup storage. \" );\
    \n          }\
    \n\
    \n          :delay 3; \
    \n         }\
    \n        :set \$btrfssnapshotstatuscheck (\$btrfssnapshotstatuscheck \"done\");\
    \n}\
    \n"
```

```
add dont-require-permissions=no name=BraidSnapshotCleanUpStart owner=admin policy=ftp,read,write,policy,test,
sniff source=":global btrfssnapshotcleanupstatuscheck;\
```

```
    \n:global snapshotdirectoryname; \
    \n:local maxsnapshotstokeep;\
    \n:local maxdaysoldsnapshotstokeep;\
    \n:local sysadmin;\
    \n\
    \n:set \$maxsnapshotstokeep ( \$maxsnapshotstokeep 10);\
```

```
    \n:set \$maxdaysoldsnapshotstokeep (\$maxdaysoldsnapshotstokeep \"10d\");\
    \n:set \$sysadmin ( \$sysadmin \"<servername@domain.tld>\" );\
```

```
    \n:set \$snapshotdirectoryname (\$snapshotdirectoryname \"@snapshots\");\
    \n\
```

```
    \n if (\$btrfssnapshotcleanupstatuscheck != \"started\") do={\
```

```
    \n         :set \$btrfssnapshotcleanupstatuscheck (\$btrfssnapshotcleanupstatuscheck \"started\");\
    \n         foreach i in=[/disk/btrfs/filesystem/find] do={ \
```

```
    \n           :local temp [ /disk btrfs filesystem/get value-name=label \$i;]\
```

1697 

```
    \n           :local currenttimestamp; :set  \$currenttimestamp ( \$currenttimestamp [/system/clock/get date
] );\
```

```
    \n          :set  \$currenttimestamp ( \$currenttimestamp  -\$maxdaysoldsnapshotstokeep);\
    \n            foreach j in=[/disk btrfs subvolume/find  where fs=\$temp and top-
level=\$snapshotdirectoryname ] do={\
    \n               :local parentname [ /disk/btrfs/subvolume/get value-name=name \$j;];\
    \n               :local parentsubvol [ /disk/btrfs/subvolume/get value-name=parent \$j; ];\
    \n               :local creationtimeofsnapshot; :set \$creationtimeofsnapshot (\$creationtimeofsnapshot [
/disk/btrfs/subvolume/get value-name=creation-time \$j; ]);\
    \n               :local countparentsnapshots;  :set \$countparentsnapshots (\$countparentsnapshots [/disk
btrfs subvolume/print count-only  where fs=\$temp and top-level=\$snapshotdirectoryname and
parent=\$parentsubvol]);\
```

```
    \n               if ([:len \$parentsubvol]=0) do={\
    \n                   :local parentfullname [ /disk/btrfs/subvolume/get value-name=fullname \$j;];\
    \n                    /log info message=\"INFO: SnapshotCleanup found snapshot of completely deleted
subvolume. Location of snapshot \$temp/\$snapshotdirectoryname/\$parentname. This can only be removed manually.
\";\
```

```
    \n               } else={\
    \n                if (\$currenttimestamp>=\$creationtimeofsnapshot or
\$countparentsnapshots>\$maxsnapshotstokeep ) do={\
    \n                   /log info message=\"INFO: Braid snapshot  \$snapshotdirectoryname/\$parentname
deleted. SnapshotCleanUp keeps  \$maxsnapshotstokeep snapshots or snapshots not older than
\$maxdaysoldsnapshotstokeep days.\";\
    \n                  /disk btrfs subvolume remove \$parentname;\
    \n                :delay 1;\
    \n               }\
    \n             }\
    \n            }\
    \n          :delay 3; \
    \n         }\
    \n        :set \$btrfssnapshotcleanupstatuscheck (\$btrfssnapshotcleanupstatuscheck \"done\");\
    \n}\
    \n"
```
