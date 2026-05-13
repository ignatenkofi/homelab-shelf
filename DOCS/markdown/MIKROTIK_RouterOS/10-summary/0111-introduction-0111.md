## Introduction 

Queues in RouterOS are processed using CPU resources, so limiting traffic with queues on devices with relatively weak CPUs is not an effective configuration. In other words, switch-based units will be overloaded very fast, because they are meant to process layer 2 traffic by using a switch-chip, not CPU. To avoid such inefficiency, RouterOS allows limiting traffic using switch chips.
