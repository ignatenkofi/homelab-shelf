## `/user/print` 

```
Columns: NAME, GROUP, LAST-LOGGED-IN, INACTIVITY-POLICY
# NAME   GROUP  LAST-LOGGED-IN       INACTIVITY-POLICY
;;; system default user
0 admin  full   2025-07-22 17:09:59  none
```

```
[admin@MikroTik] > system/script/run add-dhcp-no-perms  use-script-permissions
not enough permissions (9)
[admin@MikroTik] > system/script/run add-dhcp-no-perms
Added DHCP client on ether2!
```

Similarly, there are multiple ways to run a script using the scheduler tool. When using the scheduler, the script can run with the scheduler's permissions. 

You can also call the script by name using the scheduler, which works the same way as `/system script run use-script-permissions` . 

To demonstrate this, we create three schedulers, each configured to run the script in a different way:
