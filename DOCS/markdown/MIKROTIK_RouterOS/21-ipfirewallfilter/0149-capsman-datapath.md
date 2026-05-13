## CAPSMAN Datapath 

Datapath settings control data forwarding related aspects. On CAPsMAN datapath settings are configured in the datapath profile menu /interface/wifi /datapath/ or directly in a configuration profile or interface menu as settings with datapath. prefix. 

There are 2 major forwarding/traffic-processing modes: 

local forwarding mode ( `traffic-processing=on-cap` ), where CAP is locally forwarding data to and from wireless interface; CAPsMAN forwarding mode ( `traffic-processing=on-capsman` ), where CAP sends to CAPsMAN all data received over wireless and only sends out the wireless data received from CAPsMAN. 

**==> picture [13 x 13] intentionally omitted <==**

CAPsMAN forwarding is only possible starting with 7.21beta2 version. On older versions, only CAP forwarding is supported. 

CAPsMAN forwarding is not supported by wifi-qcom-ac devices (wifi-qcom-ac drivers only support local forwarding ).
