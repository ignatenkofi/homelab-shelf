## Notes 

By looking at the packet flow diagram you can see that traffic flow is at the end of the input, forward, and output chain stack. It means that traffic flow will count only traffic that reaches one of those chains. 

For example, you set up a mirror port on a switch, connect the mirror port to a router, and set traffic flow to count mirrored packets. Unfortunately, such a setup will not work, because mirrored packets are dropped before they reach the input chain. 

Other interfaces will appear in the report if traffic is passing through them and the monitoring interface.
