[DEFAULT]
plugin_id=900026

[config]
type=detector
enable=yes

source=log
location=/var/log/devices/devicename.0-fim_off.log,/var/log/devices/devicename.0-fim_on.log
create_file=true

process=
start=no
stop=no
restart=no  ; restart plugin process after each interval
startup=
shutdown=

[110]
event_type=event
regexp="^(?P<date>\w+\s+\d+\s+\d+:\d+:\d+)\s+(?P<device>\S+)\s+.*?INFORMATION\((?P<sid>\d+)\).*?CCHIDS\:\s+Previous\s+SHA256\:\s+\'(?P<sha1>.*?)\'.*?Current\s+SHA256:\s+\'(?P<sha2>.*?)\'.*?for:\s+'(?P<filename>.*?)\s+\(\S+\s+time\)\'$"
date={normalize_date($date)}
#device={resolv($device)}
plugin_sid={$sid}
src_ip={resolv($device)}
userdata1={$sha1}
userdata2={$sha2}
filename={$filename}


event_type=event
regexp="^(?P<date>\w+\s+\d+\s+\d+:\d+:\d+)\s+(?P<device>\S+)\s+.*?INFORMATION\((?P<sid>\d+)\).*?$"
date={normalize_date($date)}
#device={resolv($device)}
plugin_sid={$sid}
src_ip={resolv($device)}
