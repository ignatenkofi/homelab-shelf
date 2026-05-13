## Introduction 

Burst is a feature that allows satisfying queue requirements for additional bandwidth even if the required rate is bigger than MIR ( max-limit ) for a limited period of time. 

Burst can occur only if average-rate of the queue for the last burst-time seconds is smaller than burst-threshold . Burst will stop if average-rate of the queue for the last burst-time seconds is bigger or equal to burst-threshold. 

The burst mechanism is simple - if a burst is allowed max-limit value is replaced by the burst-limit value. When the burst is disallowed max-limit value remains unchanged. 

1. burst-limit (NUMBER) : maximal upload/download data rate which can be reached while the burst is allowed; 

2. burst-time (TIME) : period of time, in seconds, over which the average data rate is calculated. (This is NOT the time of actual burst); 3. burst-threshold (NUMBER) : this is value of burst on/off switch; 

4. average-rate (read-only) : Every 1/16 part of the burst-time , the router calculates the average data rate of each class over the last burst-time secon ds; 

5. actual-rate (read-only) : actual traffic transfer rate of the queue;
