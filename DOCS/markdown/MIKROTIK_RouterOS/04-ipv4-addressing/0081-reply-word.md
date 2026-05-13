## Reply word 

It is only sent by the router in response to the full sentence received from the client. 

The first word of reply begins with '!'; 

- Each sentence sent generates at least one reply (if a connection does not get terminated); The last reply for every sentence is the reply that has the first word !done; Errors and exceptional conditions begin with !trap; Data replies begin with !re; 

- Replies of commands which do not have any data to reply with, begin with !empty (introduced in RouterOS 7.18); If the API connection is closed, RouterOS sends !fatal with a reason as a reply and then closes the connection;
