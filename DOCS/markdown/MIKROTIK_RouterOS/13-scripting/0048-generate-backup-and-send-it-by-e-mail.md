## Generate backup and send it by e-mail 

This script generates a backup file and sends it to a specified e-mail address. The mail subject contains the router's name, current date, and time. 

Note that the SMTP server must be configured before this script can be used. See /tool e-mail for configuration options. 

```
/system backup save name=email_backup
```

```
/tool e-mail send file=email_backup.backup to="me@test.com" body="See attached file" \
   subject="$[/system identity get name] $[/system clock get time] $[/system clock get date] Backup")
```

1116 

**==> picture [13 x 13] intentionally omitted <==**

The backup file contains sensitive information like passwords. So to get access to generated backup files, the script or scheduler must have a 'sensitive' policy.
