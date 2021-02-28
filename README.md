# shell_ip_change. 
  1 #!/bin/bash. 
  2. 
  3. 
  4 while [ 1 ]. 
  5 do. 
  6         bondIP= ifconfig enp0s25 | grep 'inet ' | awk '{print $2}'. 
  7         webIP= cat /etc/lighttpd/lighttpd.conf | grep server.bind | awk '{print $3}' | sed 's/[""]//g'. 
  8         mdIP= arp -a | grep 9c:5c:8e:c2:98:cd | awk '{print $2}' | sed 's/[()]//g'. 
  9         if [ "$bondIP" -ne "$webIP" ]. 
 10                 sed "s/$webIP/$bondIP/" /etc/lighttpd/lighttpd.conf. 
 11                 echo "update Solution_IP set IP = '$mdIP' where no='1'" > /db.sql. 
 12                 echo "update Solution_IP set IP = '$bondIP' where no='2'" >> /db.sql. 
 13                 sleep 60;  
 14         fi. 
 15 done. 
