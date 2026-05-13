## 6.  Create a Discord Bridge Container: 

```
/container/add remote-image=litetex/mau.mautrix.discord:latest interface=veth1 root-dir=disk1/synapse-
discord mounts=synapse_discord_data name=synapse_discord
```
