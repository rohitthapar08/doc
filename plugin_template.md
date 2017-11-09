[DEFAULT]
plugin_id=

[config]
type=detector
enable=yes

source=log
location=/var/log/devices/devicename.log
create_file=true

process=
start=no
stop=no
restart=no  ; restart plugin process after each interval
startup=
shutdown=

[translation]
_DEFAULT_=99999

[100]
event_type=event
regexp=''
date={normalize_date($date)}
device={resolv($device)}
plugin_sid={translate($sid)}
src_ip={resolv($src_ip)}
dst_ip={resolv($dst_ip)}
src_port=($src_port)
dst_port={($dst_port)}


[999] # Generic 
event_type=event
regexp=''
date={normalize_date($date)}
device={resolv($device_ip)}
plugin_sid=99999
