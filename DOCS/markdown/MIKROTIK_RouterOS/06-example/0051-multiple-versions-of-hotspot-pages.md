## Multiple Versions of HotSpot Pages 

300 

Multiple HotSpot page sets for the same HotSpot server are supported. They can be chosen by the user (to select language) or automatically by JavaScript (to select PDA/regular version of HTML pages). 

To utilize this feature, create subdirectories in the HotSpot HTML directory, and place those HTML files, which are different, in that subdirectory. For example, to translate everything in Latvian, the subdirectory "lv" can be created with login.html, logout.html, status.html, alogin.html, radvert.html and errors. txt files, which are translated into Latvian. If the requested HTML page can not be found in the requested subdirectory, the corresponding HTML file from the main directory will be used. Then main login.html file would contain a link to "/lv/login?dst=$(link-orig-esc)", which then displays Latvian version of login page: <a href="/lv/login?dst=$(link-orig-esc)">Latviski</a> . And Latvian version would contain a link to English version: <a href="/login?dst=$(link-origesc)">English</a> 

Another way of referencing directories is to specify 'target' variable: 

```
        <a href="$(link-login-only)?dst=$(link-orig-esc)&target=lv">Latviski</a>
```

```
        <a href="$(link-login-only)?dst=$(link-orig-esc)&target=%2F">English</a>
```

After the preferred directory has been selected (for example, "lv"), all links to local HotSpot pages will contain that path (for example, $(link-status) = "http:// hotspot.mt.lv/lv/status"). So, if all HotSpot pages reference links using "$(link-xxx)" variables, then no more changes are to be made - each client will stay within the selected directory all the time.
