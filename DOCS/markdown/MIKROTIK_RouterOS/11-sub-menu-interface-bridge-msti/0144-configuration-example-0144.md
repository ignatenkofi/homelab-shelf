## Configuration example 

In the following example, we have one SOHO device with two connected units PC and Server. 

**==> picture [504 x 273] intentionally omitted <==**

We have a 15 Mbps connection available from ISP in this case. We want to be sure the server receives enough traffic, so we will configure a simple queue with a limit-at parameter to guarantee a server receives 5Mbps: 

```
/queue simple
```

```
add limit-at=5M/5M max-limit=15M/15M name=queue1 target=192.168.88.251/32
```

That is all. The server will get 5 Mbps of traffic rate regardless of other traffic flows. If you are using the default configuration, be sure the FastTrack rule is disabled for this particular traffic, otherwise, it will bypass Simple Queues and they will not work.
