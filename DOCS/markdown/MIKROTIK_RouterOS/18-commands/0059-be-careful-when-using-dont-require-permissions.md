## Be careful when using dont-require-permissions 

It is possible to set script with dont-require-permissions parameter. Basically it allows anyone without adequate permissions to execute the script. For example, if script has policies "read,write,test,sensitive", but user or application that executes the script has less, for example, "read,write", then by setting `d ont-require-permissions=yes` will allow to run script anyway. 

This could potentially allow to change sensitive information using script even if user doe snot have enough permissions. 

1128
