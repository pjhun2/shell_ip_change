# shell_ip_change.
#!/bin/bash. 
while [ 1 ]   
do   
bondIP= ifconfig enp0s25 | grep 'inet ' | awk '{print $2}'   
webIP= cat /etc/lighttpd/lighttpd.conf | grep server.bind | awk '{print $3}' | sed 's/[""]//g'  
mdIP= arp -a | grep 9c:5c:8e:c2:98:cd | awk '{print $2}' | sed 's/[()]//g'  
if [ "$bondIP" -ne "$webIP" ].  
    sed "s/$webIP/$bondIP/" /etc/lighttpd/lighttpd.conf  
    echo "update Solution_IP set IP = '$mdIP' where no='1'" > /db.sql  
    echo "update Solution_IP set IP = '$bondIP' where no='2'" >> /db.sql   
    sleep 60;    
   fi   
done.  
