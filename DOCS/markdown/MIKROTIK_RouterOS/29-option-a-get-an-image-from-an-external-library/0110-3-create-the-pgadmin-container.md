## 3.  Create the Pgadmin Container: 

```
//container/add remote-image=dpage/pgadmin4 envlist=ENV_PGADMIN mounts=MOUNT_PGADMIN_CONFIG,
MOUNT_PGADMIN_DATA interface=veth1 logging=yes name=pgadmin root-dir=disk1/images/pgadmin start-on-
boot=yes user=0:0
```
