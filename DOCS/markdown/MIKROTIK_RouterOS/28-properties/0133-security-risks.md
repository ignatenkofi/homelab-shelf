## Security risks: 

When a security expert publishes his exploit research - anyone can apply such an exploit; 

Someone can build a container image that can use the exploit AND provide a Linux root shell; 

- By using a root shell someone may leave a permanent backdoor/vulnerability in your RouterOS system even after the container image is removed and the container feature disabled; 

If a vulnerability is injected into the primary or secondary RouterBOOT (or vendor pre-loader), then even Netinstall may not be able to fix it; 

1845
