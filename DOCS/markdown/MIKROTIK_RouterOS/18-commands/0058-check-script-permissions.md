## Check script permissions 

Lets say we have a script that creates and writes content to the file: 

- `/system script add name=script1 policy=ftp,read,write source={ /file print file=test;` 

- `/file set test.txt content="my content"` 

```
}
```

Now lets add scheduler that will try to execute this script: 

```
/system scheduler
```

```
add interval=10s name=test on-event=script2 policy=read,write
```

So now we wait 10 seconds, file not created, we wait another 10 seconds and still no file. What is going on? If you look closely script requires policy "ftp", to create a file, but scheduler has only "read" and "write" policies, so script will not be executed. Fix is to set scheduler to run with correct policies "read, write,ftp". 

This applies also if you are trying to run script from netwatch, ppp on event and so on, which are limited to specific policies "read,write,test,reboot", so you will not be able to run advanced scripts that creates backups, creates files and so on. 

Limitation could be fixed by using dont-require-permissions, but be very careful, read below.
