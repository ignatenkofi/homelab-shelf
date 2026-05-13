## Starting the container 

After you make sure that the container has been added and the status changed to `status=stopped` after using `/container/print` → you can initiate it: 

```
/container/start 0
```

If you have enabled container logging, you would see something like this in the Logs section: 

```
 12:12:46 container,info,debug 1707214366: mosquitto version 2.0.18 starting
 12:12:46 container,info,debug 1707214366: Config loaded from /mosquitto/config/mosquitto.conf.
 12:12:46 container,info,debug 1707214366: Opening ipv4 listen socket on port 1883.
 12:12:46 container,info,debug 1707214366: Opening ipv6 listen socket on port 1883.
 12:12:46 container,info,debug 1707214366: mosquitto version 2.0.18 running
```
