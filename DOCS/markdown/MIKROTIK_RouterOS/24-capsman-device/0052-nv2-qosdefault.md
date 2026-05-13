## Nv2-qos=default 

In this mode outgoing frame at first is inspected by built-in QoS policy algorithm that selects queue based on packet type and size. If built-in rules do not match, queue is selected based on frame priority field, as in Nv2-qos=frame-priority mode.
