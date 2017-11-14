# zabbix-proxy

====本地端dns服務安裝設定==========================

   yum install dnsmasq -y 
   cp /etc/resolv.conf /etc/resolv.dnsmasq.conf 
   cp /etc/hosts /etc/dnsmasq.hosts 
   cp /etc/dnsmasq.conf /etc/dnsmasq.conf.bak 
   echo 'resolv-file=/etc/resolv.dnsmasq.conf' >> /etc/dnsmasq.conf 
   echo 'addn-hosts=/etc/dnsmasq.hosts' >> /etc/dnsmasq.conf 
   echo 'cache-size=10000' >> /etc/dnsmasq.conf 

   service dnsmasq start 
   echo 'nameserver 127.0.0.1' > /etc/resolv.conf 
   systemctl enable dnsmasq 
   chkconfig dnsmasq on 
   netstat -tunlp|grep 53 
   dig www.google.com.tw 

====本地端dns服務安裝設定==========================
