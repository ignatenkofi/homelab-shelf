## 7.  Start and stop the Discord bridge Container to generate files: 

```
/container/start [find where name=synapse_discord]
/container/stop [find where name=synapse_discord]
```

8.  Connect to your RouterOS device using SFTP client (for example, WinSCP when using Microsoft Windows) and adjust the file `disk1/dynapsediscord/config.yaml` : 

```
homeserver
    address: http://localhost:8008
    domain: test.mt.lv
    software: standard
    async_media: true
appservice
    address: leave default
    hostname: leave default
    port: leave default
    database:
        type: postgres
        uri: postgres://synapse_discord:<POSTGRE_DISCORD_PASSWORD_HERE>@172.17.0.2:5434/synapse-discord?
sslmode=disable
bridge:
    encryption:
        allow: true
    permissions:
        "*": relay
        "@your_admin_user1:test.mt.lv": admin
        "@your_admin_user2:test.mt.lv": admin
```

1873 

9.  Start and stop the Discord bridge Container again: 

```
/container/start [find where name=synapse_discord]
```

```
/container/stop [find where name=synapse_discord]
```

10.  Download the file `disk1/synapse-discord/registration.yaml` and upload it as file `disk1/synapse-data/mautrix-discordregistration.yaml` 

11.  Connect to your RouterOS device using a SFTP client (for example, WinSCP when using Microsoft Windows) and add the following lines to `disk 1/synapse-data/homeserver.yaml` : 

```
...
app_service_config_files:
- /data/mautrix-discord-registration.yaml
```

12.  Start and stop the Synapse and Discord bridge Containers: 

```
/container/start [find where name=synapse_discord]
/container/stop [find where name=synapse_discord]
/container/start [find where name=synapse]
/container/stop [find where name=synapse]
```

13.  Your Matrix server should not have a new user called "Discord bridge bot". Follow the official documentation to create bridged rooms. 

1874
