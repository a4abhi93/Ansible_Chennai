####To view the list of modules
ansible-doc -l | more

####o view the description of a particular modules
ansible-doc -s ping

####To ping the target servers
ansible all -m ping

####To Ping a particular host group
ansible linuxservers -i hosts -m ping

####To ping a children host group 
ansible app -i hosts -m ping 

####To use shell module 
ansible all -m shell -a "uname -a"

####To use shell module with multiple commands
ansible all -m shell -a "uname -a;df -h"
#### Apply patches and updates via yum, apt, and other package managers.
1. ansible linuxservers -b -m yum -a "name=ntp state=present"
2. ansible linuxservers -b -m service -a "name=ntpd state=started enabled=yes"
3. ansible linuxservers -b -a "service ntpd stop"
4. ansible linuxservers -b -a "ntpdate -q 0.rhel.pool.ntp.org"
5. ansible linuxservers -b -a "service ntpd start"
6. ansible app -b -m package -a "name=git state=present"
#### Check resource usage (disk space, memory, CPU, swap space, network). 
1. ansible linuxservers -a "df -h"
2. ansible linuxservers -a "free -m"
3. ansible linuxservers -a "date"
#### Manage system users and groups.
1. ansible app -b -m group -a "name=admin state=present"
2. ansible app -b -m user -a "name=ansible-hyd group=admin createhome=yes"
3. ansible app -b -m user -a "name=johndoe state=absent remove=yes"
#### Check log files.
1. ansible linuxservers -b -a "tail /var/log/messages"
2. ansible linuxservers -b -m shell -a "tail /var/log/messages | grep ansible-command | wc -l"
#### Copy files to and from servers.
1. ansible linuxservers -m stat -a "path=/etc/environment"
2. ansible linuxservers -m copy -a "src=/etc/hosts dest=/tmp/hosts"
3. ansible linuxservers -b -m fetch -a "src=/etc/hosts dest=/tmp"
4. ansible linuxservers -m file -a "dest=/tmp/test mode=644 state=directory"
5. ansible linuxservers -m file -a "src=/src/symlink dest=/dest/symlink owner=root group=root state=link"
6. ansible linuxservers -m file -a "dest=/tmp/test state=absent"
#### Deploy applications or run application maintenance.
1. ansible app -b -m yum -a "name=MySQL-python state=present"
2. ansible app -b -m yum -a "name=python-setuptools state=present"
5. ansible db -b -m yum -a "name=mariadb-server state=present"
6. ansible db -b -m service -a "name=mariadb state=started enabled=yes"
7. ansible db -b -a "iptables -F"
8. ansible db -b -a "iptables -A INPUT -s 192.168.60.0/24 -p tcp -m tcp --dport 3306 -j ACCEPT"
#### Manage cron jobs.
1. ansible linuxservers -b -m cron -a "name='daily-cron-all-servers' hour=4 job='/path/to/daily-script.sh'"
2. ansible linuxservers -b -m cron -a "name='daily-cron-all-servers' state=absent"
#### Async or Fire and forget or Background jobs
1. ansible linuxservers -b -B 3600 -a "yum -y update"
2. ansible linuxservers -b -m async_status -a "jid=763350539037"
3. ansible linuxservers -B 3600 -P 0 -a "yum install tree -y"
