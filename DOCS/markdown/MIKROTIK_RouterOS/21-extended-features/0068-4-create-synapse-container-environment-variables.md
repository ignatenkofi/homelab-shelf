## 4.  Create Synapse Container environment variables: 

```
/container/envs/add name=synapse_envs key=SYNAPSE_CONFIG_DIR value="/data"
```

```
/container/envs/add name=synapse_envs key=SYNAPSE_CONFIG_PATH value="/data/homeserver.yaml"
/container/envs/add name=synapse_envs key=SYNAPSE_SERVER_NAME value="test.mt.lv"
```

```
/container/envs/add name=synapse_envs key=SYNAPSE_REPORT_STATS value="yes"
```
