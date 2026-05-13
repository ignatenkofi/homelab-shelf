## What is CCQ and how are the values determined? 

Client Connection Quality (CCQ) is a value in percent that shows how effective the bandwidth is used regarding the theoretically maximum available bandwidth. CCQ is weighted average of values Tmin/Treal, that get calculated for every transmitted frame, where Tmin is time it would take to transmit given frame at highest rate with no retries and Treal is time it took to transmit frame in real life (taking into account necessary retries it took to transmit frame and transmit rate). 

What is hw-retries setting? 

1541 

Number of times sending frame is retried without considering it a transmission failure. The data rate is decreased upon failure and frame is sent again. Three sequential failures on lowest supported rate suspend transmission to this destination for the duration of on-fail-retry-time. After that, the frame is sent again. The frame is being retransmitted until transmission success, or until the client is disconnected after disconnect-timeout. The frame can be discarded during this time if frame-lifetime is exceeded. In case of Nstreme "on-fail-retry-time", "disconnect-timeout" and "frame-lifetime" settings are not used. So after three sequential failures on the lowest supported rate, the wireless link is disconnected with "extensive data loss" message.
