## `/log print` 

```
 2025-07-22 18:11:25 script,error executing script add-dhcp-no-perms from scheduler (run-script-direct) failed,
please check it manually
```

```
 2025-07-22 18:11:25 script,error,debug not enough permissions (9) (/ip/dhcp-client/add; line 1)
```

```
 2025-07-22 18:11:25 script,error executing script from scheduler (run-script-use-script-perms) failed, please
check it manually
```

```
 2025-07-22 18:11:25 script,error,debug (scheduler:run-script-use-script-perms) not enough permissions (9) (/ip
/dhcp-client/add; line 1)
```

```
 2025-07-22 18:11:25 system,info dhcp client added by scheduler:run-script-scheduler-perms/script:add-dhcp-no-
perms (*7 = /ip dhcp-client add interface=ether2)
```

**==> picture [13 x 13] intentionally omitted <==**

A script with higher or more permissions than the user/scheduler cannot be run; use-script-permissions won’t override this.
