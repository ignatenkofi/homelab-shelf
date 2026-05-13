## Environment variables and mounts 

Per the eclipse-mosquitto docker hub, define a mount for the configuration file. We will mount not just the configuration file, but the whole folder, because, for SSL MQTT, we will need to upload certificates into the folder as well: 

```
/container mounts add src=/mosquitto_mounted dst=/mosquitto/config name=msqt_config
```
