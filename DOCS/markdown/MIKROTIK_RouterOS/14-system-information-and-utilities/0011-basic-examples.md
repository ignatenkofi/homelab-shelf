## Basic examples 

This example will show how to send an email with configuration export every 24hours. 

1. Configure SMTP server 

```
[admin@MikroTik] /tool e-mail> set server=10.1.1.1 port=25 from="router@mydomain.com"
```

2. Add a new script named "export-send": 

```
/export file=export
```

```
/tool e-mail send to="config@mydomain.com" subject="$[/system identity get name] export" \
body="$[/system clock get date] configuration file" file=export.rsc
```

3. Add scheduler to run our script: 

```
/system scheduler add on-event="export-send" start-time=00:00:00 interval=24h
```

Send e-mail to a server using TLS/SSL encryption. For example, Google mail requires that. 

**==> picture [13 x 13] intentionally omitted <==**

After the Google mail added a new security policy that does not allow 3d-party devices to authenticate using your standard Gmail password → you need to generate a 16-digit passcode ("App password") and use it instead of your Gmail password. To configure this, navigate to the " Securi ty>How you sign in to Google " section settings and: 

Enable 2-Step Verification; Generate an App password . 

Use the newly generated App password in the "set password= mypassword " setting shown below. 

1. configure a client to connect to the correct server: 

1137 

```
/tool e-mail
set address=smtp.gmail.com
set port=465
set tls=yes
set from=myuser@gmail.com
set user=myuser
set password=mypassword
```
