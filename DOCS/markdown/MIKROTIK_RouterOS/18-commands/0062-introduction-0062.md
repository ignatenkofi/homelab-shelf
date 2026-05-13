## Introduction 

RouterOS uses data from the TZ database, Most of the time zones from this database are included, and have the same names. Because local time on the router is used mostly for timestamping and time-dependent configuration, and not for historical date calculations, time zone information about past years is not included. Currently, only information starting from 2005 is included. 

Following settings are available in the /system clock console path and in the "Time" tab of the "System > Clock" WinBox window. 

Startup date and time is jan/02/1970 00:00:00 [+|-]gmt-offset.
