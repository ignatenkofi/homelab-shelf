## Properties 

**==> picture [516 x 424] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>auto-restart-interval  Specify an interval at which Container will be restarted on Container failure. Example: 10s<br>(string; Default: )<br>cmd   (string;  The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, or they<br>Default: ) can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.<br>comment  (string;  Short description<br>Default: )<br>dns  (string; Default:  If container needs different DNS, it can be configured here<br>)<br>domain-name  (string<br>; Default: )<br>entrypoint ( string;  An ENTRYPOINT allows to specify executable to run when starting container. Example: /bin/sh<br>Default:  )<br>envlist  (string;  list of environmental variables (configured under /container envs ) to be used with container<br>Default: )<br>file  (string; Default: ) container *tar.gz tarball if the container is imported from a file<br>hostname  (string;  Assigning a hostname to a container helps in identifying and managing the container more easily<br>Default: )<br>interface  (string;  veth interface to be used with the container<br>Default: )<br>logging  (string;  if set to yes, all container-generated output will be shown in the RouterOS log<br>Default: )<br>start-on-boot  (string; if set to yes, the container will be started automatically on device start-up.<br>Default: )<br>mounts  (string;  mounts from /container/mounts/ sub-menu to be used with this container<br>Default: )<br>remote-image  (strin the container image name to be installed if an external registry is used (configured under /container/config set registry-url=...)<br>g; Default: )<br>**----- End of picture text -----**<br>


1846 

**==> picture [516 x 207] intentionally omitted <==**

**----- Start of picture text -----**<br>
root-dir  (string;  used to save container store outside main memory<br>Default: )<br>stop-signal  (string;  Type of Linux signal to send when container was not stopped after 10 seconds<br>Default: 15)<br>workdir  (string;  the working directory for cmd entrypoint<br>Default: )<br>devices  (string;  passes through physical device to the container<br>Default: )<br>cpu-list  (string;  specifies which CPU cores the container is allowed to run on<br>Default: )<br>user  (string;  sets the user and group the container process runs as before execution.<br>Default: )<br>memory-high  (int;  RAM usage limit in bytes for a specific container<br>Default: )<br>**----- End of picture text -----**<br>
