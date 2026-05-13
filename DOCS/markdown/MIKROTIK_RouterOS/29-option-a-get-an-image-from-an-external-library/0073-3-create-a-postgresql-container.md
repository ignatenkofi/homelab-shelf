## 3.  Create a PostgreSQL Container: 

```
/container/add remote-image=postgres:17.2-alpine interface=veth1 root-dir=disk1/postgres-17.2-synapse
mounts=synapse_postgres_data envlist=postgres_synapse_envs name=postgresql_synapse
```
