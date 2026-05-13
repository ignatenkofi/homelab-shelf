## 1.  Create PostgreSQL Container environment variables: 

```
/container/envs/add name=postgres_synapse_envs key=POSTGRES_DB value="synapse"
```

```
/container/envs/add name=postgres_synapse_envs key=POSTGRES_PASSWORD value="<POSTGRES_PASSWORD_HERE>"
/container/envs/add name=postgres_synapse_envs key=POSTGRES_USER value="synapse_user"
```

```
/container/envs/add name=postgres_synapse_envs key=PGDATA value="/var/lib/postgresql/data/pgdata"
/container/envs/add name=postgres_synapse_envs key=POSTGRES_INITDB_ARGS value="--encoding='UTF8' --lc-
collate='C' --lc-ctype='C'"
```

```
/container/envs/add name=postgres_synapse_envs key=PGPORT value=5433
```

2.  Create PostgreSQL Container mounts: 

```
/container/mounts/add name=synapse_postgres_data src=disk1/synapse-postgres-data dst=/var/lib/postgresql
/data
```
