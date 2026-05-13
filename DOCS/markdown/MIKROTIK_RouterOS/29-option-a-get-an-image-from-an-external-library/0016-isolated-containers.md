## Isolated Containers 

In this networking setup, you have multiple Containers and you want to make sure that some of them can communicate without Firewall restrictions, but some need to be isolated from other Containers. For example, you might want to create two database Containers and isolate them. 

- The network configuration: 

```
/interface/veth/add name=veth1 address=172.17.0.2/24 gateway=172.17.0.1
/interface/veth/add name=veth2 address=172.18.0.2/24 gateway=172.18.0.1
/interface/bridge/add name=containers1
/interface/bridge/add name=containers2
/ip/address/add address=172.17.0.1/24 interface=containers1
/ip/address/add address=172.18.0.1/24 interface=containers2
/interface/bridge/port add bridge=containers1 interface=veth1
/interface/bridge/port add bridge=containers2 interface=veth2
/ip firewall nat
add chain=srcnat action=masquerade src-address=172.17.0.0/24
add chain=srcnat action=masquerade src-address=172.18.0.0/24
add action=dst-nat chain=dstnat dst-address=192.168.88.1 dst-port=81 protocol=tcp to-addresses=172.
17.0.2 to-ports=80
add action=dst-nat chain=dstnat dst-address=192.168.88.1 dst-port=82 protocol=tcp to-addresses=172.
18.0.2 to-ports=80
```

1852 

The first and second database Container configuration: 

```
/container/envs/add list=ENV_POSTGRES1 key=POSTGRES_DB value="webapp1"
/container/envs/add list=ENV_POSTGRES1 key=POSTGRES_PASSWORD value="<changeme>"
/container/envs/add list=ENV_POSTGRES1 key=POSTGRES_USER value="webapp1"
/container/envs/add list=ENV_POSTGRES1 key=PGDATA value="/var/lib/postgresql/data/pgdata"
/container/envs/add list=ENV_POSTGRES1 key=POSTGRES_INITDB_ARGS value="--encoding='UTF8' --lc-
collate='C' --lc-ctype='C'"
/container/mounts/add name=MOUNT_POSTGRES1 src=disk1/volumes/postgres1/data dst=/var/lib/postgresql/data
/container/add remote-image=postgres:15 interface=veth1 root-dir=disk1/images/postgres1
mounts=MOUNT_POSTGRES1 envlist=ENV_POSTGRES1 name=postgres1 start-on-boot=yes logging=yes
```

```
/container/envs/add list=ENV_POSTGRES2 key=POSTGRES_DB value="webapp2"
/container/envs/add list=ENV_POSTGRES2 key=POSTGRES_PASSWORD value="<changeme>"
/container/envs/add list=ENV_POSTGRES2 key=POSTGRES_USER value="webapp2"
/container/envs/add list=ENV_POSTGRES2 key=PGDATA value="/var/lib/postgresql/data/pgdata"
/container/envs/add list=ENV_POSTGRES2 key=POSTGRES_INITDB_ARGS value="--encoding='UTF8' --lc-
collate='C' --lc-ctype='C'"
```

```
/container/mounts/add name=MOUNT_POSTGRES2 src=disk1/volumes/postgres2/data dst=/var/lib/postgresql/data
/container/add remote-image=postgres:15 interface=veth2 root-dir=disk1/images/postgres2
mounts=MOUNT_POSTGRES2 envlist=ENV_POSTGRES2 name=postgres2 start-on-boot=yes logging=yes
```

The first and second webapp Container configuration: 

```
/container/add remote-image=dpage/pgadmin4 interface=veth1 root-dir=disk1/images/pgadmin1 name=pgadmin1
start-on-boot=yes logging=yes
```

```
/container/add remote-image=dpage/pgadmin4 interface=veth2 root-dir=disk1/images/pgadmin2 name=pgadmin2
start-on-boot=yes logging=yes
```

In this example, `pgadmin1` is able to reach `postgres1` , but is not able to reach `postgres2` . Similarly `pgadmin2` is able to reach `postgres2` , but is not able to reach `postgres1` .
