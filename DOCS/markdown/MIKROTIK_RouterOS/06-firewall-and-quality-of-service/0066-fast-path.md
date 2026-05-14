## Fast Path 

From what we learned so far, it is quite obvious that such packet processing takes a lot of CPU resources. To fast things up FastPath was introduced in the first RouterOS v6. What it does is it skips processing in the Linux kernel, basically trading some RouterOS functionality for performance. For FastPath to work, interface driver support and specific configuration conditions are required.
