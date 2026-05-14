## IPSec Policies 

Let's take a look at another tunnel type - IPSec. This type of VPN does not have logical interfaces but is processed in a similar manner. 

Instead of logical interfaces packets are processed through IPSec policies. After routing decision (2) and input firewall processing (3), the router tries to match the source and 

688 

destination to the IPsec policy. When policy matches the packet it is sent to decryption (5). After the decryption packet enters PREROUTING processing again (6) and starts another processing loop, but now with the decapsulated packet. 

**==> picture [504 x 424] intentionally omitted <==**

The same process is with encapsulation but in reverse order. The first IP packet gets processed through facilities, then matched against IPsec policies (5), encapsulated (6), and then sent to processing on the second loop (7-10). 

**==> picture [504 x 146] intentionally omitted <==**

689 

**==> picture [504 x 277] intentionally omitted <==**
