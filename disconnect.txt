#!/bin/bash
. /etc/openvpn/login/config.sh
tm="$(date +%s)"
dt="$(date +'%Y-%m-%d %H:%M:%S')"
timestamp="$(date +'%FT%TZ')"

##mysql -u $USER -p$PASS -D $DB -h $HOST -sN -e "UPDATE bandwidth_logs SET bytes_received='$bytes_received',bytes_sent='$bytes_sent',time_out='$dt', status='offline' WHERE username='$common_name' AND status='online' AND category='vip' "

mysql -u $USER -p$PASS -D $DB -h $HOST -sN -e "UPDATE users SET is_connected=0 WHERE user_name='$common_name' ";
mysql -u $USER -p$PASS -D $DB -h $HOST -sN -e "UPDATE users SET bandwidth_premium=bandwidth_premium +'$bytes_received' WHERE user_name='$common_name'";
