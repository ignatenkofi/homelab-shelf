## HTB Properties 

- parent (Name of parent simple queue, or none) : assigns this queue as a child queue for selected target {{{...}}}. Target queue can be HTB queue or any other previously created simple queue. In order for traffic to reach child queues, parent queues must capture all necessary traffic. priority (1..8) : Prioritize one child queue over other child queue. Does not work on parent queues (if queue has at least one child). One is the highest, eight is the lowest priority. Child queue with higher priority will have chance to reach its max-limit before child with lower priority. Priority have nothing to do with bursts. 

- queue (SOMETHING/SOMETHING) : Choose the type of the upload/download queue. Queue types can be created in /queue type . limit-at (NUMBER/NUMBER) : normal upload/download data rate that is guaranteed to a target max-limit (NUMBER/NUMBER) : maximal upload/download data rate that is allowed for a target to reach to reach what burst-limit (NUMBER/NUMBER) : maximal upload/download data rate which can be reached while the burst is active burst-time (TIME/TIME) : period of time, in seconds, over which the average upload/download data rate is calculated. (This is NOT the time of actual burst) burst-threshold (NUMBER/NUMBER) : when average data rate is below this value - burst is allowed, as soon as average data rate reach this value - burst is denied. (basically this is burst on/off switch). For optimal burst behavior this value should above limit-at value and below max-limit value 

And corresponding options for global-total HTB queue: 

- total-queue (SOMETHING/SOMETHING): corresponds to queue total-limit-at (NUMBER/NUMBER): corresponds to limit-at total-max-limit (NUMBER/NUMBER): corresponds to max-limit total-burst-limit (NUMBER/NUMBER): corresponds to burst-limit total-burst-time (TIME/TIME): corresponds to burst-time total-burst-threshold (NUMBER/NUMBER): corresponds to burst-threshold 

Good practice suggests that: 

Sum of children's limit-at values must be less or equal to max-limit of the parent.Every child's max-limit must be less than max-limit of the parent. This way you will leave some traffic for the other child queues, and they will be able to get traffic without fighting for it with other child queues.
