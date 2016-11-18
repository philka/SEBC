## MariaDB
https://www.cloudera.com/documentation/enterprise/latest/topics/install_cm_mariadb.html

**install server**
```
yum install mariadb-server
```

**edit `vi /etc/my.cnf`**
```
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0
# Settings user and group are ignored when systemd is used.
# If you need to run mysqld under a different user or group,
# customize your systemd unit file for mariadb according to the
# instructions in http://fedoraproject.org/wiki/Systemd

#
# recommended cloudera settings
#

transaction-isolation = READ-COMMITTED
# Disabling symbolic-links is recommended to prevent assorted security risks;
# to do so, uncomment this line:
# symbolic-links = 0

key_buffer = 16M
key_buffer_size = 32M
max_allowed_packet = 32M
thread_stack = 256K
thread_cache_size = 64
query_cache_limit = 8M
query_cache_size = 64M
query_cache_type = 1

max_connections = 550
#expire_logs_days = 10
#max_binlog_size = 100M

#log_bin should be on a disk with enough free space. Replace '/var/lib/mysql/mysql_binary_log' with an appropriate path for your system
#and chown the specified folder to the mysql user.
log_bin=/var/lib/mysql/mysql_binary_log

binlog_format = mixed

read_buffer_size = 2M
read_rnd_buffer_size = 16M
sort_buffer_size = 8M
join_buffer_size = 8M

# InnoDB settings
innodb_file_per_table = 1
innodb_flush_log_at_trx_commit  = 2
innodb_log_buffer_size = 64M
innodb_buffer_pool_size = 4G
innodb_thread_concurrency = 8
innodb_flush_method = O_DIRECT
innodb_log_file_size = 512M

[mysqld_safe]
log-error=/var/log/mariadb/mariadb.log
pid-file=/var/run/mariadb/mariadb.pid

#
# include all files from the config directory
#
!includedir /etc/my.cnf.d
```

**start mariadb**
```
service mariadb start
```

**move innodb files (only if they are existing)**
Move old InnoDB log files /var/lib/mysql/ib_logfile0 and /var/lib/mysql/ib_logfile1 out of /var/lib/mysql/ to a backup location.
```
mv /var/lib/mysql/ib_logfile0 /tmp
mv /var/lib/mysql/ib_logfile1 /tmp
```

**add to start**
```
systemctl enable mariadb
```

**set root password**
```
sudo /usr/bin/mysql_secure_installation
```

**login**
```
mysql -u root -p
```

**jdbc driver**
http://dev.mysql.com/downloads/connector/j/5.1.html

```
scp ~/Downloads/mysql-connector-java-5.1.40.tar.gz pkarg_master1:.
scp ~/Downloads/mysql-connector-java-5.1.40.tar.gz pkarg_node1:.
scp ~/Downloads/mysql-connector-java-5.1.40.tar.gz pkarg_node2:.
scp ~/Downloads/mysql-connector-java-5.1.40.tar.gz pkarg_node3:.
scp ~/Downloads/mysql-connector-java-5.1.40.tar.gz pkarg_edge1:.
```

```
tar zxvf mysql-connector-java-5.1.40.tar.gz
sudo su
mkdir -p /usr/share/java/
cp /home/ec2-user/mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/mysql-connector-java.jar
```

**create databases and rights**
```
create database amon DEFAULT CHARACTER SET utf8;
create database rman DEFAULT CHARACTER SET utf8;
create database metastore DEFAULT CHARACTER SET utf8;
create database sentry DEFAULT CHARACTER SET utf8;
create database nav DEFAULT CHARACTER SET utf8;
create database navms DEFAULT CHARACTER SET utf8;
create database hue DEFAULT CHARACTER SET utf8;
create database oozie DEFAULT CHARACTER SET utf8;
create database scm DEFAULT CHARACTER SET utf8;
```

**define user rights**
```
grant all on amon.* TO 'amon'@'%' IDENTIFIED BY 'admin';
grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'admin';
grant all on metastore.* TO 'metastore'@'%' IDENTIFIED BY 'admin';
grant all on sentry.* TO 'sentry'@'%' IDENTIFIED BY 'admin';
grant all on nav.* TO 'nav'@'%' IDENTIFIED BY 'admin';
grant all on navms.* TO 'navms'@'%' IDENTIFIED BY 'admin';
grant all on hue.* TO 'hue'@'%' IDENTIFIED BY 'admin';
grant all on oozie.* TO 'oozie'@'%' IDENTIFIED BY 'admin';
grant all on scm.* TO 'scm'@'%' IDENTIFIED BY 'admin';
```

## Cloudera Manager
### Execute on EVERY NODE
**add hostname with internal dns**
```
hostname
ip-10-0-185-227.us-west-2.compute.internal
ip-10-0-185-225.us-west-2.compute.internal
ip-10-0-185-228.us-west-2.compute.internal
ip-10-0-185-226.us-west-2.compute.internal
ip-10-0-185-224.us-west-2.compute.internal
...
vi /etc/sysconfig/network
HOSTNAME=...

```

**diable selinux**
```
vi /etc/selinux/config
SELINUX=disabled
---
setenforce 0
---
sestatus
```

**deactivate iptables**
```
systemctl stop firewalld
systemctl mask firewalld
```

### Execute on MASTER

**add cloudera repo**
```
vi /etc/yum.repos.d/cloudera-manager.repo
---
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.7.4/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1

```

**install cloudera deamons + server**
```
yum clean all
yum repoinfo cloudera-manager
yum install cloudera-manager-daemons cloudera-manager-server
```

**install jdk**
```
yum install oracle-j2sdk1.7
export JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera; export PATH=$JAVA_HOME/bin:$PATH
```

**install bind-utils**
```
yum install bind-utils
```

**initialize manger database**
```
/usr/share/cmf/schema/scm_prepare_database.sh mysql scm root
---
PASSWORD: admin
```

**start cloudera manager**
```
service cloudera-scm-server start
http://54.218.115.182:7180/cmf
tail -f /var/log/cloudera-scm-server/cloudera-scm-server.log | grep "http://"

http://54.218.60.190:7180/cmf/login
```

**frontend**
```
Benutzerdefiniertes Repository:
https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.8.2/
---
Benutzerdefinierte GPG-Schlüssel-URL:
https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
---
(x) Oracle Java SE Development Kit (JDK) installieren
(x) Java-Dateien für die Verschlüsselungsrichtlinie mit unbegrenzter Stärke installieren (wichtig für kerberos / sentry)
---
Anderer Benutzer:
ec2-user
```

---
## stuff
**troubleshooting repo**
```
yum repoinfo
```

**start services**
```
service cloudera-scm-agent start
service cloudera-scm-server start
```

```
less -S /var/log/hadoop-hdfs/hadoop-cmf-hdfs-NAMENODE-ip-10-0-38-247.us-west-2.compute.internal.log.out
---
2016-11-16 03:26:15,191 ERROR org.apache.hadoop.hdfs.server.namenode.NameNode: Failed to start namenode.
java.io.FileNotFoundException: /dfs/nn/current/VERSION (Permission denied)
        at java.io.RandomAccessFile.open(Native Method)
        at java.io.RandomAccessFile.<init>(RandomAccessFile.java:241)
        at org.apache.hadoop.hdfs.server.common.StorageInfo.readPropertiesFile(StorageInfo.java:245)
        at org.apache.hadoop.hdfs.server.namenode.NNStorage.readProperties(NNStorage.java:627)
        at org.apache.hadoop.hdfs.server.namenode.FSImage.recoverStorageDirs(FSImage.java:337)
        at org.apache.hadoop.hdfs.server.namenode.FSImage.recoverTransitionRead(FSImage.java:213)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.loadFSImage(FSNamesystem.java:1097)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.loadFromDisk(FSNamesystem.java:779)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.loadNamesystem(NameNode.java:613)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.initialize(NameNode.java:675)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.<init>(NameNode.java:843)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.<init>(NameNode.java:822)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.createNameNode(NameNode.java:1543)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.main(NameNode.java:1611)
2016-11-16 03:26:15,193 INFO org.apache.hadoop.util.ExitUtil: Exiting with status 1
2016-11-16 03:26:15,195 INFO org.apache.hadoop.hdfs.server.namenode.NameNode: SHUTDOWN_MSG: 
/************************************************************
SHUTDOWN_MSG: Shutting down NameNode at ip-10-0-38-247.us-west-2.compute.internal/10.0.38.247
************************************************************/
```

**set correct rights**
```
chown -R hdfs:hadoop current
```

**add user / groups**
```
groupadd destroy
groupadd enslave
useradd -u 2500 -G kang enslave
useradd -u 2501 -G kodos destroy
passwd kang
passwd kodos
cat /etc/passwd
cat /etc/groups
groups kang
groups kodos
```

**toubleshooting hearbeat**
https://community.cloudera.com/t5/Cloudera-Manager-Installation/Getting-quot-heartbeat-quot-errors-when-trying-to-install-CDH/ta-p/36843
```
vi /etc/hosts
10.0.212.152    master1
10.0.38.250     node1
10.0.38.249     node2
10.0.38.248     node3
10.0.38.247     edge1
```

**explicit hostname setting**
```
hostname
vi /etc/sysconfig/network
/etc/init.d/network restart
```

# bind-utils
```
[root@ip-10-0-212-152 ec2-user]# yum install bind-utils
```
