## Configuration 

We have to follow three basic steps to create HTB: 

Match and mark traffic – classify traffic for further use. Consists of one or more matching parameters to select packets for the specific class; Create rules (policy) to mark traffic – put specific traffic classes into specific queues and define the actions that are taken for each class; Attach a policy for specific interface(-s) – append policy for all interfaces (global-in, global-out, or global-total), for a specific interface, or for a specific parent queue; 

HTB allows to create of a hierarchical queue structure and determines relations between queues, like "parent-child" or "child-child". 

As soon as the queue has at least one child it becomes an inner queue, all queues without children - are leaf queues. Leaf queues make actual traffic consumption, Inner queues are responsible only for traffic distribution. All leaf queues are treated on an equal basis. 

In RouterOS, it is necessary to specify the parent option to assign a queue as a child to another queue. 

708
