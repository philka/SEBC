# Challenge Setup

## List the region, AMI ID, and OS you are using
* **region**
```
us-west-2a (Oregon)
```

* **ami_id**
```
RHEL-7.2_HVM-20161025-x86_64-1-Hourly2-GP2 (ami-5dd3743d)
```

* **os**
```
root@ip-10-0-215-17 ec2-user]# cat /proc/version
Linux version 3.10.0-327.36.3.el7.x86_64 (mockbuild@x86-037.build.eng.bos.redhat.com) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-4) (GCC) ) #1 SMP Thu Oct 20 04:56:07 EDT 2016
```

---

## List the volume space you have available on each node

**master1**
```
[root@ip-10-0-215-17 ec2-user]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2       40G  1.1G   39G   3% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000
```

**edge1**
```
[root@ip-10-0-215-18 ec2-user]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2       40G  929M   40G   3% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000
```

**node1**
```
[root@ip-10-0-215-19 ec2-user]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2       40G  928M   40G   3% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/0
tmpfs           1.5G     0  1.5G   0% /run/user/1000
```

**node2**
```
[root@ip-10-0-215-20 ec2-user]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2       40G  928M   40G   3% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/0
tmpfs           1.5G     0  1.5G   0% /run/user/1000
```

**node3**
```
[root@ip-10-0-215-21 ec2-user]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2       40G  928M   40G   3% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/0
tmpfs           1.5G     0  1.5G   0% /run/user/1000
```

---

## The command and output for yum repolist enabled
```
[root@ip-10-0-215-17 ec2-user]# yum repolist enabled
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
rhui-REGION-client-config-server-7                                                                                                                        | 2.9 kB  00:00:00     
rhui-REGION-rhel-server-releases                                                                                                                          | 3.5 kB  00:00:00     
rhui-REGION-rhel-server-rh-common                                                                                                                         | 3.8 kB  00:00:00     
(1/7): rhui-REGION-rhel-server-releases/7Server/x86_64/group                                                                                              | 701 kB  00:00:00     
(2/7): rhui-REGION-rhel-server-releases/7Server/x86_64/updateinfo                                                                                         | 1.7 MB  00:00:00     
(3/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/group                                                                                             |  104 B  00:00:00     
(4/7): rhui-REGION-client-config-server-7/x86_64/primary_db                                                                                               | 5.4 kB  00:00:00     
(5/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/updateinfo                                                                                        |  29 kB  00:00:00     
(6/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/primary_db                                                                                        | 110 kB  00:00:00     
(7/7): rhui-REGION-rhel-server-releases/7Server/x86_64/primary_db                                                                                         |  31 MB  00:00:00     
repo id                                                                       repo name                                                                                    status
rhui-REGION-client-config-server-7/x86_64                                     Red Hat Update Infrastructure 2.0 Client Configuration Server 7                                   6
rhui-REGION-rhel-server-releases/7Server/x86_64                               Red Hat Enterprise Linux Server 7 (RPMs)                                                     13,390
rhui-REGION-rhel-server-rh-common/7Server/x86_64                              Red Hat Enterprise Linux Server 7 RH Common (RPMs)                                              209
repolist: 13,605
```

---

## Add the following Linux accounts to all nodes
* User bavaria with a UID of 2700
* User saxony with a UID of 2800
* Create the group democratic and add saxony to it
* Create the group social and add bavaria to it

```
groupadd democratic
groupadd social
useradd -u 2700 -G social bavaria
useradd -u 2800 -G democratic saxony
passwd bavaria
passwd saxony
```

---

## List the `/etc/passwd` entries for bavaria and saxony in your setup file
```
cat /etc/passwd
bavaria:x:2700:2700::/home/bavaria:/bin/bash
saxony:x:2800:2800::/home/saxony:/bin/bash
```

---

## List the `/etc/group` entries for democratic and social in your setup file

```
cat /etc/group
democratic:x:1001:saxony
social:x:1002:bavaria
bavaria:x:2700:
saxony:x:2800:
```