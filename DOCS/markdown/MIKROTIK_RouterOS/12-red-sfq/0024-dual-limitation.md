## Dual Limitation 

Each queue in HTB has two rate limits: 

CIR (Committed Information Rate) – ( limit-at in RouterOS) worst case scenario, the flow will get this amount of traffic no matter what (assuming we can actually send so much data); MIR (Maximal Information Rate) – ( max-limit in RouterOS) best case scenario, a rate that flow can get up to if their queue's parent has spare bandwidth; 

In other words, at first limit-at ( CIR ) of all queues will be satisfied, only then child queues will try to borrow the necessary data rate from their parents in order to reach their max-limit ( MIR ). 

**==> picture [13 x 13] intentionally omitted <==**

CIR will be assigned to the corresponding queue no matter what. (even if max-limit of the parent is exceeded) 

That is why, to ensure optimal (as designed) usage of the dual limitation feature, we suggest sticking to these rules: 

The Sum of committed rates of all children must be less or equal to the amount of traffic that is available to parents; 

CIR(parent)* ≥ CIR(child1) +...+ CIR(childN)*in case if parent is main parent CIR(parent)=MIR(parent) 

The maximal rate of any child must be less or equal to the maximal rate of the parent 

MIR (parent) ≥ MIR(child1) & MIR (parent) ≥ MIR(child2) & ... & MIR (parent) ≥ MIR(childN) 

Queue colors in Winbox: 

0% - 50% available traffic used - green 

51% - 75% available traffic used - yellow 

76% - 100% available traffic used - red
