## Discord bridge 

**==> picture [13 x 13] intentionally omitted <==**

The example below is for configuring a Discord bridge, but the procedure for other types of bridges is very similar. Check the official documentation of your desired bridge for more information. 

1.  Create PostgreSQL Discord bridge Container environment variables: 

1872 

```
/container/envs/add name=postgres_discord_envs key=POSTGRES_DB value="synapse-discord"
/container/envs/add name=postgres_discord_envs key=POSTGRES_PASSWORD value="
<POSTGRE_BRIDGE_PASSWORD_HERE>"
/container/envs/add name=postgres_discord_envs key=POSTGRES_USER value="synapse_discord"
/container/envs/add name=postgres_discord_envs key=PGDATA value="/var/lib/postgresql/data/pgdata"
/container/envs/add name=postgres_discord_envs key=POSTGRES_INITDB_ARGS value="--encoding='UTF8' --lc-
collate='C' --lc-ctype='C'"
/container/envs/add name=postgres_synapse_envs key=PGPORT value=5434
```
