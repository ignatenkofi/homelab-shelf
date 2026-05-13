## Resource Saving 

Since reallocating hardware resources in runtime is not an option, RouterOS cannot automatically free queue buffers reserved for inactive ports. Those buffers remain unused. However, if the user knows that the specific ports will never be used (e.g., stay physically disconnected), the respective queue resources can be manually freed by using the built-in "offline" tx-manager with minimum resources: 

```
/interface/ethernet/switch/qos/port
```

```
set [find where !running] tx-manager=offline
```

**==> picture [13 x 13] intentionally omitted <==**

When configuring `tx-manager` setting to QSFP+ or QSFP28 interfaces, you must apply the same configuration to all four sub-interfaces of a port. For example, if the interface qsfp28-1-1 is active and linked at 100Gbps, while sub-interfaces (qsfp28-1-2, qsfp28-1-3, qsfp28-1-4) are showing a non-running flag, do not assign the "offline" tx-manager to thouse non-running sub-interfaces . Doing so will impact the 100Gbps link as well. However, if none of the four sub-interfaces are running, it is safe to assign the "offline" tx-manager setting.
