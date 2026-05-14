## Script permissions 

There are four ways a script can be run: using script permissions, user permissions, scheduler permissions or on-event permissions (such as `/system routerboard mode-button` settings). 

Depending on how a script is called, it may inherit different permissions or use its own. 

When using `/system script run` , a script can inherit the permissions of the caller. 

In this example, we use an admin user with full permissions and test running a script both with and without the `use-script-permissions` parameter. 

1111
