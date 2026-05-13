## Method 

This approach uses HTTP POST capability of RouterOS Fetch tool. It allows you to POST any kind of data to a webserver, right from the RouterOS command line. Of course, you can use scripting, to fill the POST data with variables. The posted data will be written to an SQLITE3 database (file is created, if it doesn't exist) and then, read from the database and fed into a Leaflet.js PolyLine array. This is a proof of concept example, there is no authentication, security, or error handling.
