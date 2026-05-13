## Properties 

**==> picture [516 x 152] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>time  (HH:MM:SS); where HH - hour 00..24, MM - minutes 00..59, SS - seconds 00..59).<br>date  (mmm/DD/YYYY); where mmm - month, one of jan  feb  mar  apr  may  jun  jul  aug  sep  oct  nov  dec  DD , , , , , , , , , , , , - date, 00..31, YYYY - year, 1970..<br>2037): date and time show current local time on the router. These values can be adjusted using the set command. Local<br>time cannot, however, be exported, and is not stored with the rest of the configuration.<br>time-zone-name  (manual, Name of the time zone. As most of the text values in RouterOS, this value is case sensitive. Special value manual applies m<br>or name of time zone;  anually configured GMT offset, which by default is 00:00 with no daylight saving time.<br>default value: manual);<br>time-zone-autodetect  (yes Feature available from v6.27. If enabled, the time zone will be set automatically.<br>or no; default: yes);<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Time-zone-autodetect by default is enabled on new RouterOS installation and after configuration reset. The time zone is detected depending on the router's public IP address and our Cloud servers database. Since RouterOS v6.43 your device will use cloud2.mikrotik.com to communicate with MikroTik's Cloud server. Older versions will use cloud.mikrotik.com to communicate with the MikroTik's Cloud server. 

Be aware that the router's internal CPU clock is not a reliable time source for precise timing operations, as its frequency may vary due to power management, thermal conditions, and hardware differences, even between identical models. This variation is expected and does not affect normal router performance. For accurate timekeeping, it is recommended to use network-based time synchronisation, such as NTP (Network Time Protocol).
