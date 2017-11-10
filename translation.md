[DEFAULT]
plugin_id=934014

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
DNS request=1
Packet dropped=2
strict TCP state=3
Authentication successful=4
web request blocked, forbidden category detected=5
http access=6
UDP flood detected=7
OTP verification did not succeed, failing authentication.=8
Authentication failed=9
object changed=10
_DEFAULT_=99999


[100]
#Mar  1 00:01:01 192.168.10.1 2017: 03:01-02:30:05 devicename-hq-sg135 ulogd[4824]: id="2001" severity="info" sys="SecureNet" sub="packetfilter" name="Packet dropped" action="drop" fwrule="60001" initf="eth0" mark="0x3441" app="1089" srcmac="08:94:ef:2d:94:87" dstmac="00:1a:8c:4b:4e:e8" srcip="192.168.12.10" dstip="192.168.12.255" proto="17" length="78" tos="0x00" prec="0x00" ttl="128" srcport="137" dstport="137"
event_type=event
regexp='^(?P<date>\w+\s+\d+\s+\d+:\d+:\d+).*?(?P<device>\S+).*\d+:\d+:\d+\s+\S+.*?\s+name="(?P<sid>.*?)".*?\s+srcip="(?P<src_ip>\d+.\d+.\d+.\d+)".*?\s+dstip="(?P<dst_ip>\d+.\d+.\d+.\d+)".*?\s+srcport="(?P<src_port>\d+)".*?\s+dstport="(?P<dst_port>\d+)".*'
date={normalize_date($date)}
device={resolv($device)}
plugin_sid={translate($sid)}
src_ip={resolv($src_ip)}
dst_ip={resolv($dst_ip)}
src_port=($src_port)
dst_port={($dst_port)}


[998] #generic 
event_type=event
regexp='^(?P<date>\w+\s+\d+\s+\d+:\d+:\d+).*?(?P<device>\S+)'   
date={normalize_date($date)}
device={resolv($device)}
plugin_sid=9999
