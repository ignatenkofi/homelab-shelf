## Restart the container: 

```
[admin@MikroTik] > /container/stop 0
[admin@MikroTik] > /container/start 0
```

Make sure to wait for the container to stop ( `status=stopped` should be shown after using `/container/print` command) before initiating it again.
