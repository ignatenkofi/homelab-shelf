## What is disconnect-timeout setting? 

This interval is measured from the third sending failure on the lowest data rate. At this point 3 * (hw-retries + 1) frame transmits on the lowest data rate had failed. During disconnect-timeout packet transmission will be retried with on-fail-retry-time interval. If no frame can be transmitted successfully during discon nect-timeout, the connection is closed, and this event is logged as "extensive data loss". Successful frame transmission resets this timer.
