# zabbix-proxy

====安裝zabbix release 及zabbix-proxy zabbix-agent==========================  
  3.4 Centos6  
  http://repo.zabbix.com/zabbix/3.4/rhel/6/x86_64/zabbix-release-3.4-1.el6.noarch.rpm  
  
  3.4 centos 7  
  http://repo.zabbix.com/zabbix/3.4/rhel/7/x86_64/zabbix-release-3.4-2.el7.noarch.rpm  

  yum clean all  
  yum install zabbix-proxy-mysql zabbix-agent -y  

====安裝zabbix release 及zabbix-proxy  zabbix-agent==========================  

  yum install mariadb ## for centos 7  
  yum install mysql-server  ## for centos 6  
  mysql -u root -p  
  drop database zabbix_proxy;  
  create database zabbix_proxy character set utf8 collate utf8_bin;  
  grant all privileges on zabbix_proxy.* to zabbix@localhost identified by 'zabbix';  
  quit  
  
  zcat /usr/share/doc/zabbix-proxy-mysql-3.4.1/schema.sql.gz | mysql -uroot zabbix_proxy  
  service zabbix-proxy restart  

rpm -e zabbix-agent

rpm -Uvh http://repo.zabbix.com/zabbix/3.2/rhel/7/x86_64/zabbix-agent-3.2.8-1.el7.x86_64.rpm
rpm -Uvh http://repo.zabbix.com/zabbix/3.2/rhel/6/x86_64/zabbix-agent-3.2.7-1.el6.x86_64.rpm

cp /etc/zabbix/zabbix_agentd.conf.rpmsave /etc/zabbix/zabbix_agentd.conf

service zabbix-agent restart


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
