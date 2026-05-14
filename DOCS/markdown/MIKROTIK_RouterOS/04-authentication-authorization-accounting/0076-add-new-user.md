## Add new user 

To add the user ex with password lkjrht and profile ex available for PPTP service only, enter the following command: 

312 

```
[admin@rb13] ppp secret> add name=ex password=lkjrht service=pptp profile=ex
[admin@rb13] ppp secret> print
Flags: X - disabled
 #   NAME                SERVICE CALLER-ID         PASSWORD          PROFILE            REMOTE-ADDRESS
 0   ex                  pptp                      lkjrht            ex                 0.0.0.0
[admin@rb13] ppp secret>
```

313
