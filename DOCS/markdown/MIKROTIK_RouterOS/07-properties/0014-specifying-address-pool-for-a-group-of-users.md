## Specifying address pool for a group of users 

We can group up multiple similar users and assign RADIUS attributes to all of them at once. First of all, create a new group: 

```
/user-manager user group
```

```
add name=location1 outer-auths=chap,eap-mschap2,eap-peap,eap-tls,eap-ttls,mschap1,mschap2,pap \
inner-auths=peap-mschap2,ttls-chap,ttls-mschap1,ttls-mschap2,ttls-pap attributes=Framed-Pool:pool1
```

The next step is to assign a user to the group: 

```
/user-manager user
 set [find name=username] group=location1
```

In this case, an IP address from pool1 will be assigned to the user upon authentication - make sure pool1 is created on the NAS device.
