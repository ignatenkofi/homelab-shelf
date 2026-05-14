## Advanced: Postgres with Pgadmin 

This example shows how to configure Pgadmin on RouterOS: 

1.  Create mount points for Pgadmin Container: 

   - `/container/mounts/add name=MOUNT_PGADMIN_CONFIG src=disk1/volumes/pgadmin/config dst=/config /container/mounts/add name=MOUNT_PGADMIN_DATA src=disk1/volumes/pgadmin/data dst=/var/lib/pgadmin C` 

2.  Create environment variables for Pgadmin Container: 

1882 

```
/container/envs/add name=ENV_PGADMIN key=PGADMIN_LISTEN_PORT value=80
```

```
/container/envs/add name=ENV_PGADMIN key=PGADMIN_DEFAULT_EMAIL value="sysadmin@domain.com"
/container/envs/add name=ENV_PGADMIN key=PGADMIN_DEFAULT_PASSWORD value="<changeme>"
/container/envs/add name=ENV_PGADMIN key=PGADMIN_SERVER_JSON_FILE value="/config/servers.json"
/container/envs/add name=ENV_PGADMIN key=PGADMIN_PREFERENCES_JSON_FILE value="/config/preferences.json"
/container/envs/add name=ENV_PGADMIN key=PGPASS_FILE value="/config/pgpass"
/container/envs/add name=ENV_PGADMIN key=PGADMIN_DISABLE_POSTFIX value="True"
```
