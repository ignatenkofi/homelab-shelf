## Queue Types 

```
/queue type
```

This sub-menu list by default created queue types and allows the addition of new user-specific ones. 

By default, RouterOS creates the following pre-defined queue types: 

```
[admin@MikroTik] > /queue type print
Flags: * - default
```

```
 0 * name="default" kind=pfifo pfifo-limit=50
```

```
 1 * name="ethernet-default" kind=pfifo pfifo-limit=50
```

```
 2 * name="wireless-default" kind=sfq sfq-perturb=5 sfq-allot=1514
```

```
 3 * name="synchronous-default" kind=red red-limit=60 red-min-threshold=10 red-max-threshold=50 red-burst=20
red-avg-packet=1000
```

```
 4 * name="hotspot-default" kind=sfq sfq-perturb=5 sfq-allot=1514
```

```
 5 * name="pcq-upload-default" kind=pcq pcq-rate=0 pcq-limit=50KiB pcq-classifier=src-address pcq-total-
limit=2000KiB pcq-burst-rate=0 pcq-burst-threshold=0 pcq-burst-time=10s pcq-src-address-mask=32
     pcq-dst-address-mask=32 pcq-src-address6-mask=128 pcq-dst-address6-mask=128
```

```
 6 * name="pcq-download-default" kind=pcq pcq-rate=0 pcq-limit=50KiB pcq-classifier=dst-address pcq-total-
limit=2000KiB pcq-burst-rate=0 pcq-burst-threshold=0 pcq-burst-time=10s pcq-src-address-mask=32
     pcq-dst-address-mask=32 pcq-src-address6-mask=128 pcq-dst-address6-mask=128
```

```
 7 * name="only-hardware-queue" kind=none
```

```
 8 * name="multi-queue-ethernet-default" kind=mq-pfifo mq-pfifo-limit=50
```

```
 9 * name="default-small" kind=pfifo pfifo-limit=10
```

All MikroTik products have the default queue type " only-hardware-queue" with "kind=none". "only-hardware-queue" leaves the interface with only hardware transmit descriptor ring buffer which acts as a queue in itself. Usually, at least 100 packets can be queued for transmit in the transmit descriptor ring buffer. Transmit descriptor ring buffer size and the number of packets that can be queued in it varies for different types of ethernet MACs. Having no software queue is especially beneficial on SMP systems because it removes the requirement to synchronize access to it from different CPUs/cores which is resource-intensive. Having the possibility to set "only-hardware-queue" requires support in an ethernet driver so it is available only for some ethernet interfaces mostly found on RouterBOARDs. 

A "multi-queue-ethernet-default" can be beneficial on SMP systems with ethernet interfaces that have support for multiple transmit queues and have a Linux driver support for multiple transmit queues. By having one software queue for each hardware queue there might be less time spent on synchronizing access to them. 

**==> picture [13 x 13] intentionally omitted <==**

Improvement from only-hardware-queue and multi-queue-ethernet-default is present only when there is no "/queue tree" entry with a particular interface as a parent.
