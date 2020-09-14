# HDFS cluster setup

## Pre requisite 

### OS centos 7.5
### RAM 4 GB 
### CPU 2 core each 
### Storage 50GB each

# Pre Hadoop setup needs to done on all the systems

## Disable Selinux permanently 

```
[centos@ip-172-31-78-46 ~]$ whoami
centos
[centos@ip-172-31-78-46 ~]$ sudo  -i
[root@ip-172-31-78-46 ~]# whoami
root
[root@ip-172-31-78-46 ~]# 
```

### doing it permanently 

```
[root@ip-172-31-78-46 ~]# cat  /etc/selinux/config 

# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
#SELINUX=enforcing
SELINUX=disabled # changing enforcing. to disabled 
# SELINUXTYPE= can take one of three two values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected. 
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted 

```

### Disable Firewall of OS 

```
[root@ip-172-31-78-46 ~]# systemctl stop  firewalld
[root@ip-172-31-78-46 ~]# systemctl disable   firewalld

```
### setting hostname 

```
[root@ip-172-31-78-46 ~]# hostnamectl   set-hostname   ashunamenode.hadoop.com

```

## configure Local DNS 

```
[root@ip-172-31-78-46 ~]# cat  /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6


172.31.78.46       ashunamenode.hadoop.com
[root@ip-172-31-78-46 ~]# ping  ashunamenode.hadoop.com
PING ashunamenode.hadoop.com (172.31.78.46) 56(84) bytes of data.
64 bytes from ashunamenode.hadoop.com (172.31.78.46): icmp_seq=1 ttl=64 time=0.019 ms
64 bytes from ashunamenode.hadoop.com (172.31.78.46): icmp_seq=2 ttl=64 time=0.027 ms
64 bytes from ashunamenode.hadoop.com (172.31.78.46): icmp_seq=3 ttl=64 time=0.027 ms
^C
--- ashunamenode.hadoop.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1999ms
rtt min/avg/max/mdev = 0.019/0.024/0.027/0.005 ms

```

## Now we have to update all DNS local to every system 

```
[root@ip-172-31-78-46 etc]# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6


172.31.78.46       ashunamenode.hadoop.com
172.31.67.129   durgadatanode.hadoop.com
172.31.64.193 pradeepdatanode.hadoop.com
172.31.70.187 rohitkdatanode.hadoop.com
172.31.71.161	deepakdatanode.hadoop.com
172.31.71.245   rajkumardatanode.hadoop.com
172.31.67.9 girishdatanode.hadoop.com
172.31.64.44    ashisdatanode.hadoop.com
172.31.65.241       srinidatanode.hadoop.com
172.31.72.107 rokudatanode.hadoop.com
172.31.69.12   dineshdatanode.hadoop.com
172.31.74.78	   banudatanode.hadoop.com
172.31.76.121    vishaldatanode.hadoop.com
172.31.69.68  madhudatanode.hadoop.com
172.31.69.245  nikithdatanode.hadoop.com

```
