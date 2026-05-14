## enable SMB service: 

```
#this step is optional, as the default is "enabled=auto"
/ip/smb/set enabled=yes
```

Now check for results: 

Check general service settings: 

```
/ip/smb/print
      enabled: yes
       domain: MSHOME
      comment: MikrotikSMB
   interfaces: all
```

SMB user settings: 

```
/ip smb/users/print
Flags: X - DISABLED; * - DEFAULT; r - READ-ONLY
Columns: NAME, PASSWORD
#     NAME    PASSWORD
0 X*r guest
1     mtuser  mtpasswd
```

And finally SMB shares settings: 

1899 

```
/ip/smb/shares/print
Flags: X - DISABLED; * - DEFAULT
Columns: NAME, DIRECTORY, REQUIRE-ENCRYPTION
#    NAME    DIRECTORY  REQUIRE-ENCRYPTION
;;; default share
0 X* pub     /pub       no
1    backup  backup     no
```

Now, additional configuration changes can be done, like disabling the default user and share, etc. 

1900
