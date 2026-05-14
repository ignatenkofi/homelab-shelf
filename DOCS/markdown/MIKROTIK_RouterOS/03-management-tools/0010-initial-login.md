## Initial login 

Note: that each command and response ends with an empty word. 

Login method post-v6.43: 

/login =name=admin =password= !done 

Now the client sends a username and password in the first message. Password is sent in plain text. in case of an error, the reply contains =message=error message. In case of a successful login, the client can start to issue commands.
