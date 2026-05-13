## The database Container configuration: 

```
/container/envs/add list=ENV_POSTGRES key=POSTGRES_DB value="webapp"
```

```
/container/envs/add list=ENV_POSTGRES key=POSTGRES_PASSWORD value="<changeme>"
/container/envs/add list=ENV_POSTGRES key=POSTGRES_USER value="webapp"
```

```
/container/envs/add list=ENV_POSTGRES key=PGDATA value="/var/lib/postgresql/data/pgdata"
```

```
/container/envs/add list=ENV_POSTGRES key=POSTGRES_INITDB_ARGS value="--encoding='UTF8' --lc-collate='C'
--lc-ctype='C'"
```

```
/container/mounts/add name=MOUNT_POSTGRES src=disk1/volumes/postgres/data dst=/var/lib/postgresql/data
/container/add remote-image=postgres:15 interface=veth1 root-dir=disk1/images/postgres
mounts=MOUNT_POSTGRES envlist=ENV_POSTGRES name=postgres start-on-boot=yes logging=yes
```
