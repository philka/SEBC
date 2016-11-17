# System Configuration Checks

## 1. Check `vm.swappiness` on all your nodes
---

```bash
[ec2-user@ip-10-0-38-250 ~]$ cat /proc/sys/vm/swappiness
30
[ec2-user@ip-10-0-38-250 ~]$ sysctl vm.swappiness=1
add vm.swappiness = 1 to /etc/sysctl.conf
[ec2-user@ip-10-0-38-250 ~]$ cat /proc/sys/vm/swappiness
1
```

## 2. Show the mount attributes of all volumes
---

```
[root@ip-10-0-212-152 ec2-user]# mount -l
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=7599292k,nr_inodes=1899823,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,seclabel,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/net_cls type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/xvda2 on / type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=31,pgrp=1,timeout=300,minproto=5,maxproto=5,direct)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
tmpfs on /run/user/0 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=1497296k,mode=700)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=1497296k,mode=700,uid=1000,gid=1000)
binfmt_misc on /proc/sys/fs/binfmt_misc type binfmt_misc (rw,relatime)
```

## 3. Show the reserve space of any non-root, ext-based volumes
---

```
[ec2-user@ip-10-0-212-152 ~]$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2       20G  1.3G   19G   7% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/0
tmpfs           1.5G     0  1.5G   0% /run/user/1000
```

## 4. Show that transparent hugepages is disabled
---

```
[root@ip-10-0-212-152 ec2-user]# touch /sys/kernel/mm/transparent_hugepage/defrag
[root@ip-10-0-212-152 ec2-user]# echo never > /sys/kernel/mm/transparent_hugepage/defrag
[root@ip-10-0-212-152 ec2-user]# grep -i HugePages_Total /proc/meminfo
HugePages_Total:       0
[root@ip-10-0-212-152 bin]# vi /etc/rc.local
(add: echo never > /sys/kernel/mm/transparent_hugepage/defrag)
```

## 4. Report the network interface attributes
---

```
[root@ip-10-0-212-152 ec2-user]# ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 10.0.212.152  netmask 255.255.0.0  broadcast 10.0.255.255
        inet6 fe80::d6:3bff:fe31:e77f  prefixlen 64  scopeid 0x20<link>
        ether 02:d6:3b:31:e7:7f  txqueuelen 1000  (Ethernet)
        RX packets 1908  bytes 169907 (165.9 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1434  bytes 226788 (221.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 0  (Local Loopback)
        RX packets 4  bytes 340 (340.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 4  bytes 340 (340.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

## 5. Show forward and reverse host lookups using `getent` and `nslookup`
---

### getent
```
[root@ip-10-0-212-152 ec2-user]# getent hosts
127.0.0.1       localhost localhost.localdomain localhost4 localhost4.localdomain4
127.0.0.1       localhost localhost.localdomain localhost6 localhost6.localdomain6
10.0.38.250     node1
10.0.38.249     node2
10.0.38.248     node3
10.0.38.247     edge1
```


**forward and backward dns lookup**
```
getent hosts 54.218.60.190
getent hosts ec2-54-218-60-190.us-west-2.compute.amazonaws.com
```


### ping
```
[root@ip-10-0-212-152 ec2-user]# ping -c5 node1
PING node1 (10.0.38.250) 56(84) bytes of data.
64 bytes from node1 (10.0.38.250): icmp_seq=1 ttl=64 time=1.09 ms
64 bytes from node1 (10.0.38.250): icmp_seq=2 ttl=64 time=0.358 ms
64 bytes from node1 (10.0.38.250): icmp_seq=3 ttl=64 time=0.317 ms
64 bytes from node1 (10.0.38.250): icmp_seq=4 ttl=64 time=0.292 ms
64 bytes from node1 (10.0.38.250): icmp_seq=5 ttl=64 time=0.298 ms

--- node1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4001ms
rtt min/avg/max/mdev = 0.292/0.471/1.090/0.310 ms
[root@ip-10-0-212-152 ec2-user]# ping -c5 node2
PING node2 (10.0.38.249) 56(84) bytes of data.
64 bytes from node2 (10.0.38.249): icmp_seq=1 ttl=64 time=1.25 ms
64 bytes from node2 (10.0.38.249): icmp_seq=2 ttl=64 time=0.388 ms
64 bytes from node2 (10.0.38.249): icmp_seq=3 ttl=64 time=0.400 ms
64 bytes from node2 (10.0.38.249): icmp_seq=4 ttl=64 time=0.367 ms
64 bytes from node2 (10.0.38.249): icmp_seq=5 ttl=64 time=0.389 ms

--- node2 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4001ms
rtt min/avg/max/mdev = 0.367/0.560/1.257/0.348 ms
[root@ip-10-0-212-152 ec2-user]# ping -c5 node3
PING node3 (10.0.38.248) 56(84) bytes of data.
64 bytes from node3 (10.0.38.248): icmp_seq=1 ttl=64 time=1.01 ms
64 bytes from node3 (10.0.38.248): icmp_seq=2 ttl=64 time=0.332 ms
64 bytes from node3 (10.0.38.248): icmp_seq=3 ttl=64 time=0.374 ms
64 bytes from node3 (10.0.38.248): icmp_seq=4 ttl=64 time=0.364 ms
64 bytes from node3 (10.0.38.248): icmp_seq=5 ttl=64 time=0.349 ms

--- node3 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4001ms
rtt min/avg/max/mdev = 0.332/0.487/1.017/0.265 ms
[root@ip-10-0-212-152 ec2-user]# ping -c5 edge1
PING edge1 (10.0.38.247) 56(84) bytes of data.
64 bytes from edge1 (10.0.38.247): icmp_seq=1 ttl=64 time=1.32 ms
64 bytes from edge1 (10.0.38.247): icmp_seq=2 ttl=64 time=0.401 ms
64 bytes from edge1 (10.0.38.247): icmp_seq=3 ttl=64 time=0.384 ms
64 bytes from edge1 (10.0.38.247): icmp_seq=4 ttl=64 time=0.369 ms
64 bytes from edge1 (10.0.38.247): icmp_seq=5 ttl=64 time=0.316 ms

--- edge1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4001ms
rtt min/avg/max/mdev = 0.316/0.558/1.324/0.384 ms
```

### nslookup
```
[root@ip-10-0-212-152 ec2-user]# nslookup node1
Server:     10.0.0.2
Address:    10.0.0.2#53

** server can't find node1: NXDOMAIN
```

## 6. Verify the <code>nscd</code> service is running

```
[root@ip-10-0-212-152 ec2-user]# yum install nscd
...
```

```
[root@ip-10-0-212-152 ec2-user]# service nscd status
Redirecting to /bin/systemctl status  nscd.service
● nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
```

```
[root@ip-10-0-212-152 ec2-user]# service nscd start
Redirecting to /bin/systemctl start  nscd.service
[root@ip-10-0-212-152 ec2-user]# service nscd status
Redirecting to /bin/systemctl status  nscd.service
● nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; disabled; vendor preset: disabled)
   Active: active (running) since Tue 2016-11-15 04:10:25 EST; 9s ago
  Process: 12040 ExecStart=/usr/sbin/nscd $NSCD_OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 12041 (nscd)
   CGroup: /system.slice/nscd.service
           └─12041 /usr/sbin/nscd

Nov 15 04:10:25 ip-10-0-212-152.us-west-2.compute.internal nscd[12041]: 12041 monitoring file `/etc/hosts` (4)
Nov 15 04:10:25 ip-10-0-212-152.us-west-2.compute.internal nscd[12041]: 12041 monitoring directory `/etc` (2)
Nov 15 04:10:25 ip-10-0-212-152.us-west-2.compute.internal nscd[12041]: 12041 monitoring file `/etc/resolv.conf` (5)
Nov 15 04:10:25 ip-10-0-212-152.us-west-2.compute.internal nscd[12041]: 12041 monitoring directory `/etc` (2)
Nov 15 04:10:25 ip-10-0-212-152.us-west-2.compute.internal nscd[12041]: 12041 monitoring file `/etc/services` (6)
Nov 15 04:10:25 ip-10-0-212-152.us-west-2.compute.internal nscd[12041]: 12041 monitoring directory `/etc` (2)
Nov 15 04:10:25 ip-10-0-212-152.us-west-2.compute.internal nscd[12041]: 12041 disabled inotify-based monitoring for file `/etc/netgroup': No such file or directory
Nov 15 04:10:25 ip-10-0-212-152.us-west-2.compute.internal nscd[12041]: 12041 stat failed for file `/etc/netgroup'; will try again later: No such file or directory
Nov 15 04:10:25 ip-10-0-212-152.us-west-2.compute.internal nscd[12041]: 12041 Access Vector Cache (AVC) started
Nov 15 04:10:25 ip-10-0-212-152.us-west-2.compute.internal systemd[1]: Started Name Service Cache Daemon.
```

## 7. Verify the <code>ntpd</code> service is running<br>

```
[root@ip-10-0-212-152 ec2-user]# yum install ntp ntpdate ntp-doc
...
[root@ip-10-0-212-152 ec2-user]# chkconfig ntpd on
Note: Forwarding request to 'systemctl enable ntpd.service'.
Created symlink from /etc/systemd/system/multi-user.target.wants/ntpd.service to /usr/lib/systemd/system/ntpd.service.
[root@ip-10-0-212-152 ec2-user]# ntpdate pool.ntp.org
15 Nov 04:31:00 ntpdate[12228]: adjust time server 97.107.129.217 offset -0.003337 sec
[root@ip-10-0-212-152 ec2-user]# service ntpd start
Redirecting to /bin/systemctl start  ntpd.service
[root@ip-10-0-212-152 ec2-user]# service ntpd status
Redirecting to /bin/systemctl status  ntpd.service
● ntpd.service - Network Time Service
   Loaded: loaded (/usr/lib/systemd/system/ntpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Tue 2016-11-15 04:31:15 EST; 3s ago
  Process: 12256 ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 12257 (ntpd)
   CGroup: /system.slice/ntpd.service
           └─12257 /usr/sbin/ntpd -u ntp:ntp -g

Nov 15 04:31:15 ip-10-0-212-152.us-west-2.compute.internal ntpd[12257]: Listen normally on 2 lo 127.0.0.1 UDP 123
Nov 15 04:31:15 ip-10-0-212-152.us-west-2.compute.internal ntpd[12257]: Listen normally on 3 eth0 10.0.212.152 UDP 123
Nov 15 04:31:15 ip-10-0-212-152.us-west-2.compute.internal ntpd[12257]: Listen normally on 4 lo ::1 UDP 123
Nov 15 04:31:15 ip-10-0-212-152.us-west-2.compute.internal ntpd[12257]: Listen normally on 5 eth0 fe80::d6:3bff:fe31:e77f UDP 123
Nov 15 04:31:15 ip-10-0-212-152.us-west-2.compute.internal ntpd[12257]: Listening on routing socket on fd #22 for interface updates
Nov 15 04:31:15 ip-10-0-212-152.us-west-2.compute.internal systemd[1]: Started Network Time Service.
Nov 15 04:31:15 ip-10-0-212-152.us-west-2.compute.internal ntpd[12257]: 0.0.0.0 c016 06 restart
Nov 15 04:31:15 ip-10-0-212-152.us-west-2.compute.internal ntpd[12257]: 0.0.0.0 c012 02 freq_set kernel 0.000 PPM
Nov 15 04:31:15 ip-10-0-212-152.us-west-2.compute.internal ntpd[12257]: 0.0.0.0 c011 01 freq_not_set
Nov 15 04:31:16 ip-10-0-212-152.us-west-2.compute.internal ntpd[12257]: 0.0.0.0 c614 04 freq_mode
```

---

## Links
https://www.cloudera.com/documentation/enterprise/5-5-x/topics/cdh_admin_performance.html
https://blog.cloudera.com/blog/2015/01/how-to-deploy-apache-hadoop-clusters-like-a-boss/
