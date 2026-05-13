## BGP Configuration 

There is a complete redesign of the BGP configuration compared to ROSv6. The first biggest difference is that there is no more **`instance`** and **`peer`** conf iguration menus. Instead, we have **`connection`** , **`template`** and **`session`** menus. The reason for such a structure is to strictly split parameters that are responsible for connection and parameters that are BGP protocol specific. 

Let's start with the Template. It contains all BGP protocol-related configuration options. It can be used as a template for dynamic peers and apply a similar config to a group of peers. Note that this is not the same as peer groups on Cisco devices, where the group is more than just a common configuration. 

By default, there is a default template that requires you to set your own AS. 

```
/routing/bgp/template set default as=65533
```

**==> picture [13 x 13] intentionally omitted <==**

Starting from v7.1beta4 template parameters are exposed in the "connection" configuration. This means that the template is not mandatory anymore, allowing for an easier basic BGP connection setup, similar to what it was in ROSv6. 

Most of the parameters are similar to ROSv6 except that some are grouped in the output and input section making the config more readable and easier to understand whether the option is applied on input or output. If you are familiar with CapsMan then the syntax is the same, for example, to specify the output selection chain you set `output.filter-chain=myBgpChain` . 

You can even inherit template parameters from another template, for example: 

```
/routing/bgp/template
add name=myAsTemplate as=65500 output.filter-chain=myAsFilter
set default template=myAsTemplate
```

Another important aspect of the new routing configuration is the global Router ID, which sets router-id and group peers in one instance. RouterOS adds a default ID which picks instance-id from any interface's highest IP. The default BGP template by default is set to use the "default" ID. If for any reason you need to tweak or add new instances it can be done in `/routing id` menu. 

Very interesting parameters are **`input.affinity`** `and` **`output.affinity`** , they allow control in which process input and output of active session will be processed: 

1076 

alone - input and output of each session are processed in its own process, most likely the best option when there are a lot of cores and a lot of peers 

afi, instance, vrf, remote-as - try to run input/output of new session in process with similar parameters 

- main - run input/output in the main process (could potentially increase performance on single-core even possibly on multicore devices with small amount of cores) 

input - run output in the same process as input (can be set only for output affinity) 

Now that we have parameters set for the template we can add BGP connections. A minimal set of parameters are `remote.address` , `template, conne ct` , `listen` and `local.role` 

Connect and listen to parameters specify whether peers will try to connect and listen to a remote address or just connect or just listen. It is possible that in setups where peer uses the multi-hop connection `local.address` must be configured too (similar as it was with `update-source` in ROSv6). 

**==> picture [13 x 13] intentionally omitted <==**

It is not mandatory to specify a remote AS number. ROS v7 can determine remote ASN from an open message. You should specify the remote AS only when you want to accept a connection from that specific AS. 

Peer role is now a mandatory parameter, for basic setups, you can just use ibgp, ebgp (more information on available roles can be found in the corresponding RFC draft https://datatracker.ietf.org/doc/draft-ietf-idr-bgp-open-policy/?include_text=1), keep in mind that at the moment capabilities, communities, and filtering described in the draft is not implemented. 

Very basic iBGP set up to listen on the whole local network for connections:
