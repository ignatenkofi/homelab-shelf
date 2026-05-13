## 5.  Create Synapse Container mounts: 

```
/container/mounts/add name=synapse_data src=disk1/synapse-data dst=/data
```

6.  Create a Synapse Container for generating required data: 

1871 

```
/container/add remote-image=matrixdotorg/synapse:latest interface=veth1 cmd="generate" root-dir=disk1
/synapse mounts=synapse_data envlist=synapse_envs name=synapse
```

7.  Start and stop the Synapse Container to allow it to generate required files: 

```
/container/start [find where name=synapse]
/container/stop [find where name=synapse]
```

8.  Remove the `cmd` parameter from the Synapse Container: 

```
/container/set [find where name=synapse] cmd=""
```

9.  Connect to your RouterOS device using a SFTP client (for example, WinSCP if using Microsoft Windows) and adjust the `disk1/synapse-data /homeserver.yaml` file: 

```
database:
  name: psycopg2
  args:
    user: synapse_user
    password: <POSTGRE_PASSWORD_HERE>
    dbname: synapse
    host: localhost
    port: 5433
    cp_min: 5
    cp_max: 10
    keepalives_idle: 10 #optional
    keepalives_interval: 10 #optional
    keepalives_count: 3 #optional
```

10.  Start the PostgreSQL Container: 

```
/container/start [find where name=postgresql_synapse]
```

11.  Start the Synapse Container: 

```
/container/start [find where name=synapse]
```

12.  Enter the Synapse Container's shell and register a new user: 

```
register_new_matrix_user -c /data/homeserver.yaml
```

13.  You should now be able to access your Matrix server using your RouterOS device's address. 

**==> picture [13 x 13] intentionally omitted <==**

Make sure you check the official documentation for Synapse to get the latest configuration steps.
