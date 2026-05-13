## Token rate selection (Black part of the diagram) 

The maximal token rate at any given time is equal to the highest activity of these values: 

706 

limit-at (NUMBER/NUMBER): guaranteed upload/download data rate to a target max-limit (NUMBER/NUMBER): maximal upload/download data rate that is allowed for a target burst-limit (NUMBER/NUMBER): maximal upload/download data rate that is allowed for a target while the 'burst' is active 

burst-limit is active only when 'burst' is in the allowed state - more info here: Queue Burst 

In a case where limit-at is the highest value, extra tokens need to be issued to compensate for all missing tokens that were not borrowed from its parent queue.
