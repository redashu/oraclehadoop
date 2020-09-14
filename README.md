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

## For better performance setting up swap memory  migration value 

```
[root@ip-172-31-78-46 etc]# cat  /etc/sysctl.conf 
# sysctl settings are defined through files in
# /usr/lib/sysctl.d/, /run/sysctl.d/, and /etc/sysctl.d/.
#
# Vendors settings live in /usr/lib/sysctl.d/.
# To override a whole file, create a new file with the same in
# /etc/sysctl.d/ and put new settings there. To override
# only specific settings, add a file with a lexically later
# name in /etc/sysctl.d/ and put new settings there.
#
# For more information, see sysctl.conf(5) and sysctl.d(5).
vm.swappiness=10  
#  here 10 value means out  of 100 % how much is left

```

## Disable pagging 

```
[root@ip-172-31-78-46 etc]# cat  /etc/rc.local
#!/bin/bash
# THIS FILE IS ADDED FOR COMPATIBILITY PURPOSES
#
# It is highly advisable to create own systemd services or udev rules
# to run scripts during boot instead of using this file.
#
# In contrast to previous versions due to parallel execution during boot
# this script will NOT be run after all other services.
#
# Please note that you must run 'chmod +x /etc/rc.d/rc.local' to ensure
# that this script will be executed during boot.

chmod +x /etc/aws114_bootlog.sh
/etc/aws114_bootlog.sh
touch /var/lock/subsys/local
echo never >/sys/kernel/mm/transparent_hugepage/defrag
echo never >/sys/kernel/mm/transparent_hugepage/enabled


[root@ip-172-31-78-46 etc]# chmod +x   /etc/rc.local

```


## updating NTP client in all the system 

```
 yum  install  ntp
  systemctl enable  --now  ntpd 
  
  ```
  
  # Setup HDFS  
  
  ## Install jdk 8 in centos 7.5 
  
  ```
  yum  install  java-1.8.0-openjdk
  
  ```
  
  ## support for HDP platform 
  
  ```
  [root@ashunamenode ~]# yum  install  libtirpc-devel -y
  ```
  
  ## to check java version 
  
  ```
  [root@ashunamenode ~]# java -version 
openjdk version "1.8.0_262"
OpenJDK Runtime Environment (build 1.8.0_262-b10)
OpenJDK 64-Bit Server VM (build 25.262-b10, mixed mode)
```


# Hardware verfication 

##  Check RAM and CPU 

```
[root@ashunamenode ~]# free  -m 
              total        used        free      shared  buff/cache   available
Mem:           3788          88        3196           8         503        3463
Swap:           819           0         819


===
[root@ashunamenode ~]# lscpu 
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                2
On-line CPU(s) list:   0,1
Thread(s) per core:    1
Core(s) per socket:    2
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 79
Model name:            Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz
Stepping:              1
CPU MHz:               2300.123
BogoMIPS:              4600.12

```

## checking storage 

```
[root@ashunamenode ~]# df  -h 
Filesystem               Size  Used Avail Use% Mounted on
/dev/mapper/centos-root  6.7G  1.6G  5.1G  24% /


```

## Increasing storage with LVM 

```
[root@ashunamenode ~]# fdisk  -l   /dev/xvda 

Disk /dev/xvda: 107.4 GB, 107374182400 bytes, 209715200 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x000a2a6d

    Device Boot      Start         End      Blocks   Id  System
/dev/xvda1   *        2048     1026047      512000   83  Linux
/dev/xvda2         1026048    16777215     7875584   8e  Linux LVM


```

## entering into storage
```
[root@ashunamenode ~]# fdisk   /dev/xvda 
Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help): 



Command (m for help): p

Disk /dev/xvda: 107.4 GB, 107374182400 bytes, 209715200 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x000a2a6d

    Device Boot      Start         End      Blocks   Id  System
/dev/xvda1   *        2048     1026047      512000   83  Linux
/dev/xvda2         1026048    16777215     7875584   8e  Linux LVM

Command (m for help): n
Partition type:
   p   primary (2 primary, 0 extended, 2 free)
   e   extended
Select (default p): 
Using default response p
Partition number (3,4, default 3): 
First sector (16777216-209715199, default 16777216): 
Using default value 16777216
Last sector, +sectors or +size{K,M,G} (16777216-209715199, default 209715199): 
Using default value 209715199
Partition 3 of type Linux and of size 92 GiB is set

Command (m for help): 
Command (m for help): p

Disk /dev/xvda: 107.4 GB, 107374182400 bytes, 209715200 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x000a2a6d

    Device Boot      Start         End      Blocks   Id  System
/dev/xvda1   *        2048     1026047      512000   83  Linux
/dev/xvda2         1026048    16777215     7875584   8e  Linux LVM
/dev/xvda3        16777216   209715199    96468992   83  Linux

```

## TO update partition table in Linux 
WARNING: Re-reading the partition table failed with error 16: Device or resource busy.
The kernel still uses the old table. The new table will be used at
the next reboot or after you run partprobe(8) or kpartx(8)
Syncing disks.
[root@ashunamenode ~]# 
[root@ashunamenode ~]# 
[root@ashunamenode ~]# 
[root@ashunamenode ~]# partprobe 
[root@ashunamenode ~]# 
[root@ashunamenode ~]# 



```

## adding storage to Volume group

```
 86  pvcreate /dev/xvda3
 vgextend   centos   /dev/xvda3 
 vgdisplay 
 ```
