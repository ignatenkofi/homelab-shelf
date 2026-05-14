## 3.  Create a PostgreSQL Container for Discord bridge: 

```
/container/add remote-image=postgres:17.2-alpine interface=veth1 root-dir=disk1/postgres-17.2-discord
mounts=discord_postgres_data envlist=postgres_discord_envs name=postgresql_discord
```

4.  Follow the guide for HAProxy Container and setup a reverse proxy for port `8080` 

5.  sdaCreate Discord bridge Container mount points: 

```
/container/mounts/add name=synapse_discord_data src=disk1/synapse-discord-data dst=/data
```
