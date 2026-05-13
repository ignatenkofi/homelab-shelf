## Configuration 

To setup a Postgres Container on your RouterOS device, follow these steps bellow. 

**==> picture [13 x 13] intentionally omitted <==**

Make sure you have created a Container network before proceeding. 

1.  Create Postgres Container mount points: 

```
/container/mounts/add name=MOUNT_POSTGRES src=disk1/volumes/postgres/data dst=/var/lib/postgresql/data
```

2.  Add environment variables: 

```
/container/envs/add name=ENV_POSTGRES key=POSTGRES_DB value="myapp"
/container/envs/add name=ENV_POSTGRES key=POSTGRES_PASSWORD value="<changeme>"
```

```
/container/envs/add name=ENV_POSTGRES key=POSTGRES_USER value="myapp"
```

```
/container/envs/add name=ENV_POSTGRES key=PGDATA value="/var/lib/postgresql/data/pgdata"
```

```
/container/envs/add name=ENV_POSTGRES key=POSTGRES_INITDB_ARGS value="--encoding='UTF8' --lc-collate='C'
--lc-ctype='C'"
```

3.  Create a Postgres Container: 

```
/container/add remote-image=postgres:15 interface=veth1 root-dir=disk1/images/postgres
mounts=MOUNT_POSTGRES envlist=ENV_POSTGRES name=postgres start-on-boot=yes logging=yes
```

**==> picture [13 x 13] intentionally omitted <==**

You can specify a different version for Postgres by changing the `postgres:15` value. 

4.  Start the Postgres Container: 

```
/container/start [find where name=postgres]
```
