## 17.  Press "Save pipeline" 

18.  Go to "Stack Management" on the main menu, then select "Index Management" and then select "Component templates" 

19.  Create a new template by pressing "Create component template". 

20.  Set the "Name" to "logs-routeros@custom" 21.  Under "Index settings" section, paste the following: 

```
{
  "index": {
    "lifecycle": {
      "name": "logs"
    },
    "default_pipeline": "logs-routeros@custom"
  }
}
```

**==> picture [13 x 13] intentionally omitted <==**

Change the ILM policy to your required policy name. The "logs" is the default policy that might be in use for other logs.
