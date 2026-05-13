## Queue 

This is a simple queue tree that is placed on the Interface HTB - "public" is an interface where your ISP is connected, and "local" is where are your clients. If you have more than 1 "public" or more than 1 "local" you will need to mangle upload and download separately and place the queue tree in global-out: 

745 

```
/queue tree
```

```
add name=upload parent=public max-limit=6M
```

```
add name=other_upload parent=upload limit-at=4M max-limit=6M packet-mark=other_traffic priority=1
add name=heavy_upload parent=upload limit-at=2M max-limit=6M packet-mark=heavy_traffic priority=8
add name=download parent=local max-limit=6M
```

```
add name=other_download parent=download limit-at=4M max-limit=6M packet-mark=other_traffic priority=1
add name=heavy_download parent=download limit-at=2M max-limit=6M packet-mark=heavy_traffic priority=8
```

746
