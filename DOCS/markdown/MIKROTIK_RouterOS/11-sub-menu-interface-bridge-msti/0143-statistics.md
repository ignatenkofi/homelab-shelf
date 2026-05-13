## Statistics 

> rate (read-only/read-only) : average queue passing data rate in bytes per second packet-rate (read-only/read-only) : average queue passing data rate in packets per second bytes (read-only/read-only) : number of bytes processed by this queue 

697 

packets (read-only/read-only) : number of packets processed by this queue 

- queued-bytes (read-only/read-only) : number of bytes waiting in the queue queued-packets (read-only/read-only) : number of packets waiting in the queue dropped (read-only/read-only) : number of dropped packets 

borrows (read-only/read-only) : packets that passed queue over its "limit-at" value (and was unused and taken away from other queues) lends (read-only/read-only) : packets that passed queue below its "limit-at" value OR if queue is a parent - sum of all child borrowed packets pcq-queues (read-only/read-only) : number of PCQ substreams, if queue type is PCQ 

And corresponding options for global-total HTB queue: 

total-rate (read-only): corresponds to rate 

- total-packet-rate (read-only): corresponds to packet-rate total-bytes (read-only): corresponds to bytes 

- total-packets (read-only): corresponds to packets 

- total-queued-bytes (read-only): corresponds to queued-bytes total-queued-packets (read-only): corresponds to queued-packets total-dropped (read-only): corresponds to dropped total-lends (read-only): corresponds to lends total-borrows (read-only): corresponds to borrows 

- total-pcq-queues (read-only): corresponds to pcq-queues
