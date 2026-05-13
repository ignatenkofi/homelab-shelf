## Diffserv RFC2474 and RFC2475 

Diffserv (Differentiated Services) is a mechanism used to prioritize and classify network traffic based on the Diffserv field in the IP packet header. CAKE (Common Applications Kept Enhanced) provides Diffserv support, allowing traffic to be divided into "tins" (traffic classes) and applying different treatment to each tin. Here's a breakdown of the Diffserv presets in CAKE along with real-world examples: 

besteffort -The "besteffort" preset in CAKE disables priority queuing and places all traffic into a single tin. This means that all traffic is treated equally without any specific prioritization. This preset can be suitable for non-critical or low-priority traffic, such as general web browsing or background file downloads, where equal treatment is sufficient. 

precedence - The "precedence" preset enables the legacy interpretation of the TOS (Type of Service) "Precedence" field. However, its usage on the modern internet is discouraged, as it is an outdated mechanism. In the past, this field was used to indicate different levels of priority, such as high, medium, or low, but it is no longer widely used or recommended. 

diffserv4 - The "diffserv4" preset provides a general-purpose Diffserv implementation with four tins: 

1. Bulk : This tin corresponds to CS1 (Class Selector 1) or LE (Low Extra), and it has a threshold of 6.25%. Traffic in this tin typically has a low priority. 

2. Best Effort : This tin is for general traffic that doesn't fall into any specific Diffserv class. It has a threshold of 100%, meaning it receives all remaining bandwidth. 

3. Video : This tin encompasses AF4x, AF3x, CS3, AF2x, CS2, TOS4, and TOS1. It has a threshold of 50%, providing a moderate priority for video traffic. 

4. Voice : This tin covers CS7, CS6, EF (Expedited Forwarding), VA (Voice Admit), CS5, and CS4. It has a threshold of 25%, giving high priority to voice traffic. 

In a network where video streaming, voice over IP (VoIP), and general internet traffic coexist, this preset can ensure that video and voice traffic receive appropriate priority, while bulk and best-effort traffic are handled accordingly. 

diffserv3 

(default) - The "diffserv3" preset is the default Diffserv implementation in CAKE, providing three tins: 

1. Bulk : Similar to the "diffserv4" preset, this tin represents CS1 or LE with a 6.25% threshold, serving as a low-priority traffic class. 

2. Best Effort: This tin is for general traffic and has a threshold of 100%, treating all remaining traffic equally. 

3. Voice : This tin covers CS7, CS6, EF, VA, and TOS4. It has a threshold of 25% and applies a reduced CoDel (Controlled Delay) interval, giving high priority to voice traffic. 

In a network where voice traffic requires high priority, such as a VoIP system, while other traffic falls into a general category, the "diffserv3" preset can ensure appropriate priority for voice packets while maintaining fairness for other traffic. 

diffserv8 - is an more advances purpuse diffserver with 8 tins: 

The 8 classes in DiffServ8 are mapped to different types of network traffic based on their importance, using decimal values for Differentiated Services Code Point (DSCP): 

1. Network Control (48-63): Highest priority, often used for critical network traffic like routing information. 

2. Telephony (46): Traffic sensitive to latency, such as VoIP. 3. Signaling (32-47): Control signals for real-time applications. 4. Multimedia Conferencing (24-31): Video conferencing traffic. 5. Real-time Interactive (40): Interactive applications, such as gaming. 6. Multimedia Streaming (16-23): Streaming video and audio. 7. Low Latency Data (8-15): Traffic requiring low latency, like financial transactions. 8. Best Effort (0): Default traffic class with no special priority. 

729
