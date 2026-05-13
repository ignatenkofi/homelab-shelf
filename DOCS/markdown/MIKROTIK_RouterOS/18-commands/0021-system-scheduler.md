## `/system scheduler` 

```
add interval=10s name=run-script-use-script-perms on-event="/system script run add-dhcp-no-perms use-script-
permissions" policy=ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon
```

```
add interval=10s name=run-script-direct on-event=add-dhcp-no-perms policy=ftp,reboot,read,write,policy,test,
password,sniff,sensitive,romon
```

```
add interval=10s name=run-script-scheduler-perms on-event="/system script run add-dhcp-no-perms" policy=ftp,
reboot,read,write,policy,test,password,sniff,sensitive,romon
```

After these schedulers run, the logs show that the two methods using `use-script-permissions` or calling the script by name fail due to insufficient permissions. 

In contrast, `run-script-scheduler-perms` executes the script successfully, as it inherits the scheduler's permissions.
