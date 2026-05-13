## Environment variables and mounts 

Per the home-assist documentation, define mounts for the configuration files (where, `/usb1` is our external USB storage folder): 

```
/container mounts add dst=/config name=ha_config src=/usb1/ha_config
```

Create an environmental variable for home-assistant: 

```
/container envs add key=TZ name=ha_env value=America/Los_Angeles
```
