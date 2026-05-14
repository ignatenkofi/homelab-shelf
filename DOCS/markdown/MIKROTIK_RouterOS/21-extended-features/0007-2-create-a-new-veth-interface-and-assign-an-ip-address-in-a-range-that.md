## 2.  Create a new veth interface and assign an IP address in a range that is unique in your network: 

```
/interface/veth/add name=veth1 address=172.17.0.2/24 gateway=172.17.0.1
```

**==> picture [13 x 13] intentionally omitted <==**

The following configuration is equivalent to "bridge" networking mode in other Container engines such as Docker. It is possible to create a "host" equivalent configuration as well. 

**==> picture [13 x 13] intentionally omitted <==**

One veth interface can be used for many Containers. You can create multiple veth interfaces to create isolated networks for different Containers.
