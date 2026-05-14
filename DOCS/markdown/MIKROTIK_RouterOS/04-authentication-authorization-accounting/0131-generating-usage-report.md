## Generating usage report 

In cases where presentable network usage information is required by companies billing or legal team an automated session export can be created using the generate-report command. The command requires an input of the report template - an example of the template is available in um5files/PRIVATE /TEMPLATES/reports/report_default.html. Example of the report generation: 

```
/user-manager
```

```
generate-report report-template=report_default.html columns=username,uptime,download,upload
```

The generated report is available by accessing the router using a WEB browser and navigating to /um/PRIVATE/GENERATED/reports/gen_report_default. html 

343 

**==> picture [505 x 378] intentionally omitted <==**
