## Manual time zone configuration 

These settings are available in /system clock manual console path and in the "Manual Time Zone" tab of the "System > Clock" WinBox window. These settings have an effect only when time-zone-name =manual. It is only possible to manually configure single daylight saving time period. 

- time-zone , dst-delta + - HH:MM ([ | ] - time offset in hours and minutes, leading plus sign is optional; default value: +00:00) : While DST is not active use GMT offset time-zone . While DST is active use GMT offset time-zone + dst-delta . dst-start , dst-end mmm/DD/YYYY HH:MM: SS ( - date and time, either date or time can be omitted in the set command; default value: jan/01/1970 00:00:00): Local time when DST starts and ends. 

1130
