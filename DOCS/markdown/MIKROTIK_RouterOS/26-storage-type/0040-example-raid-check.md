## Example: RAID check 

It is extremely important to monitor your RAID array for failures. There are multiple ways to do it, but the simplest way is to create a script that sends an e- mail whenever a RAID member has failed. You can use the following script as an working example: 

```
/system scheduler
add interval=30s name=MRaidHealthCheckCall on-event=MraidHealthCheck policy=ftp,read,write,policy,test,sniff
start-time=startup
/system script
add dont-require-permissions=no name=MraidHealthCheck owner=admin policy=ftp,read,write,policy,test,sniff
source=":global CheckRAID;\
    \n:local sysadmin; \
    \n\
    \n:set  \$sysadmin \"<servername@domain.tld>\";\
    \n\
    \n:local temp [/disk print count-only where raid-member-failed];\
    \n:if ( \$temp > 0 ) do={\
    \n   :if ( \$CheckRAID < 1 ) do={\
    \n      /log info message=\"ERROR: RAID has failed!\";\
    \n      /tool e-mail send to= \$sysadmin subject=([/system identity get name].\" RAID failed\") body=(\"Go
check it! Value: \".\$temp);\
    \n      :set \$CheckRAID 7;\
    \n      :delay 5s;\
    \n    }\
    \n   }       \
    \n   :if ( \$CheckRAID > 0 ) do={\
    \n      :set \$CheckRAID ( \$CheckRAID -1 );\
    \n   }\
    \n"
```

You will also need to configure your RouterOS device's e-mail server settings: 

```
/tool e-mail
```

```
set from=<raidcheck@domain.tld> port=587 server=smtp.domain.com tls=starttls
```

**==> picture [13 x 13] intentionally omitted <==**

Make sure you configure your e-mail server's settings under `/tool e-mail` and change the e-mail address in the script above with the values that matches your e-mail server's settings.
