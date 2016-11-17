## MariaDB

https://www.cloudera.com/documentation/enterprise/latest/topics/install_cm_mariadb.html

```
[root@ip-10-0-212-152 ec2-user]# sudo yum install mariadb-server
...

Installed:
  mariadb-server.x86_64 1:5.5.52-1.el7                                                                                                                

Dependency Installed:
  libaio.x86_64 0:0.3.109-13.el7                 mariadb.x86_64 1:5.5.52-1.el7                 perl.x86_64 4:5.16.3-291.el7           perl-Carp.noarch 0:1.26-244.el7           
  perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7   perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7   perl-DBD-MySQL.x86_64 0:4.023-5.el7    perl-DBI.x86_64 0:1.627-4.el7             
  perl-Data-Dumper.x86_64 0:2.145-3.el7          perl-Encode.x86_64 0:2.51-7.el7               perl-Exporter.noarch 0:5.68-3.el7      perl-File-Path.noarch 0:2.09-2.el7        
  perl-File-Temp.noarch 0:0.23.01-3.el7          perl-Filter.x86_64 0:1.49-3.el7               perl-Getopt-Long.noarch 0:2.40-2.el7   perl-HTTP-Tiny.noarch 0:0.033-3.el7       
  perl-IO-Compress.noarch 0:2.061-2.el7          perl-Net-Daemon.noarch 0:0.48-5.el7           perl-PathTools.x86_64 0:3.40-5.el7     perl-PlRPC.noarch 0:0.2020-14.el7         
  perl-Pod-Escapes.noarch 1:1.04-291.el7         perl-Pod-Perldoc.noarch 0:3.20-4.el7          perl-Pod-Simple.noarch 1:3.28-4.el7    perl-Pod-Usage.noarch 0:1.63-3.el7        
  perl-Scalar-List-Utils.x86_64 0:1.27-248.el7   perl-Socket.x86_64 0:2.010-4.el7              perl-Storable.x86_64 0:2.45-3.el7      perl-Text-ParseWords.noarch 0:3.29-4.el7  
  perl-Time-HiRes.x86_64 4:1.9725-3.el7          perl-Time-Local.noarch 0:1.2300-2.el7         perl-constant.noarch 0:1.27-2.el7      perl-libs.x86_64 4:5.16.3-291.el7         
  perl-macros.x86_64 4:5.16.3-291.el7            perl-parent.noarch 1:0.225-244.el7            perl-podlators.noarch 0:2.5.1-3.el7    perl-threads.x86_64 0:1.87-4.el7          
  perl-threads-shared.x86_64 0:1.43-6.el7       

Dependency Updated:
  mariadb-libs.x86_64 1:5.5.52-1.el7                                                                                                                                             
---
Complete!
```

**add to start**
```
systemctl enable mariadb
```

**set root password**
```
sudo /usr/bin/mysql_secure_installation
```

**jdbc driver**
```
scp ~/Downloads/mysql-connector-java-5.1.40.tar.gz pkarg_master1:.
scp ~/Downloads/mysql-connector-java-5.1.40.tar.gz pkarg_node1:.
scp ~/Downloads/mysql-connector-java-5.1.40.tar.gz pkarg_node2:.
scp ~/Downloads/mysql-connector-java-5.1.40.tar.gz pkarg_node3:.
scp ~/Downloads/mysql-connector-java-5.1.40.tar.gz pkarg_edge1:.

---

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
```

**start services**
```
sudo service cloudera-scm-agent start
```

## Cloudera Manager

**add cloudera repo**
```
vi /etc/yum.repos.d/cloudera-manager.repo
---
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.8.2/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1

```

**install cloudera deamons + server**
```
yum clean all
yum install cloudera-manager-daemons cloudera-manager-server
```

**initialize manger database**
```
create database cm DEFAULT CHARACTER SET utf8;
grant all on cm.* TO 'cm'@'%' IDENTIFIED BY 'admin';
/usr/share/cmf/schema/scm_prepare_database.sh mysql cm root
```

**start clouder manager**
```
sudo service cloudera-scm-agent start
http://54.218.115.182:7180/cmf
tail -f /var/log/cloudera-scm-server/cloudera-scm-server.log
```

**allow root ssh**
```
sudo vi /etc/ssh/sshd_config
---
PermitRootLogin without-password
---
sudo service sshd reload
```


---
## Troubleshooting
**troubleshooting repo**
```
yum repoinfo
```

**huge pages**
```
echo never > /sys/kernel/mm/transparent_hugepage/defrag
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


*set correct rights*
```
chown -R hdfs:hadoop current
```



---

**restart cloudera agent**
```
sudo service cloudera-scm-agent restart
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
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
rhui-REGION-client-config-server-7                                                                                                  | 2.9 kB  00:00:00     
rhui-REGION-rhel-server-releases                                                                                                    | 3.5 kB  00:00:00     
rhui-REGION-rhel-server-rh-common                                                                                                   | 3.8 kB  00:00:00     
(1/2): rhui-REGION-rhel-server-releases/7Server/x86_64/updateinfo                                                                   | 1.7 MB  00:00:00     
(2/2): rhui-REGION-rhel-server-releases/7Server/x86_64/primary_db                                                                   |  31 MB  00:00:00     
Resolving Dependencies
--> Running transaction check
---> Package bind-utils.x86_64 32:9.9.4-38.el7_3 will be installed
--> Processing Dependency: bind-libs = 32:9.9.4-38.el7_3 for package: 32:bind-utils-9.9.4-38.el7_3.x86_64
--> Processing Dependency: libGeoIP.so.1()(64bit) for package: 32:bind-utils-9.9.4-38.el7_3.x86_64
--> Processing Dependency: libbind9.so.90()(64bit) for package: 32:bind-utils-9.9.4-38.el7_3.x86_64
--> Processing Dependency: libdns.so.100()(64bit) for package: 32:bind-utils-9.9.4-38.el7_3.x86_64
--> Processing Dependency: libisc.so.95()(64bit) for package: 32:bind-utils-9.9.4-38.el7_3.x86_64
--> Processing Dependency: libisccc.so.90()(64bit) for package: 32:bind-utils-9.9.4-38.el7_3.x86_64
--> Processing Dependency: libisccfg.so.90()(64bit) for package: 32:bind-utils-9.9.4-38.el7_3.x86_64
--> Processing Dependency: liblwres.so.90()(64bit) for package: 32:bind-utils-9.9.4-38.el7_3.x86_64
--> Running transaction check
---> Package GeoIP.x86_64 0:1.5.0-11.el7 will be installed
---> Package bind-libs.x86_64 32:9.9.4-38.el7_3 will be installed
--> Processing Dependency: bind-license = 32:9.9.4-38.el7_3 for package: 32:bind-libs-9.9.4-38.el7_3.x86_64
--> Running transaction check
---> Package bind-license.noarch 32:9.9.4-29.el7_2.4 will be updated
--> Processing Dependency: bind-license = 32:9.9.4-29.el7_2.4 for package: 32:bind-libs-lite-9.9.4-29.el7_2.4.x86_64
---> Package bind-license.noarch 32:9.9.4-38.el7_3 will be an update
--> Running transaction check
---> Package bind-libs-lite.x86_64 32:9.9.4-29.el7_2.4 will be updated
---> Package bind-libs-lite.x86_64 32:9.9.4-38.el7_3 will be an update
--> Finished Dependency Resolution

Dependencies Resolved

===========================================================================================================================================================
 Package                          Arch                     Version                                Repository                                          Size
===========================================================================================================================================================
Installing:
 bind-utils                       x86_64                   32:9.9.4-38.el7_3                      rhui-REGION-rhel-server-releases                   201 k
Installing for dependencies:
 GeoIP                            x86_64                   1.5.0-11.el7                           rhui-REGION-rhel-server-releases                   1.1 M
 bind-libs                        x86_64                   32:9.9.4-38.el7_3                      rhui-REGION-rhel-server-releases                   1.0 M
Updating for dependencies:
 bind-libs-lite                   x86_64                   32:9.9.4-38.el7_3                      rhui-REGION-rhel-server-releases                   729 k
 bind-license                     noarch                   32:9.9.4-38.el7_3                      rhui-REGION-rhel-server-releases                    83 k

Transaction Summary
===========================================================================================================================================================
Install  1 Package  (+2 Dependent packages)
Upgrade             ( 2 Dependent packages)

Total download size: 3.0 M
Is this ok [y/d/N]: y
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/5): GeoIP-1.5.0-11.el7.x86_64.rpm                                                                                                | 1.1 MB  00:00:00     
(2/5): bind-libs-9.9.4-38.el7_3.x86_64.rpm                                                                                          | 1.0 MB  00:00:00     
(3/5): bind-libs-lite-9.9.4-38.el7_3.x86_64.rpm                                                                                     | 729 kB  00:00:00     
(4/5): bind-license-9.9.4-38.el7_3.noarch.rpm                                                                                       |  83 kB  00:00:00     
(5/5): bind-utils-9.9.4-38.el7_3.x86_64.rpm                                                                                         | 201 kB  00:00:00     
-----------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                      7.9 MB/s | 3.0 MB  00:00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : GeoIP-1.5.0-11.el7.x86_64                                                                                                               1/7 
  Updating   : 32:bind-license-9.9.4-38.el7_3.noarch                                                                                                   2/7 
  Installing : 32:bind-libs-9.9.4-38.el7_3.x86_64                                                                                                      3/7 
  Installing : 32:bind-utils-9.9.4-38.el7_3.x86_64                                                                                                     4/7 
  Updating   : 32:bind-libs-lite-9.9.4-38.el7_3.x86_64                                                                                                 5/7 
  Cleanup    : 32:bind-libs-lite-9.9.4-29.el7_2.4.x86_64                                                                                               6/7 
  Cleanup    : 32:bind-license-9.9.4-29.el7_2.4.noarch                                                                                                 7/7 
  Verifying  : 32:bind-libs-9.9.4-38.el7_3.x86_64                                                                                                      1/7 
  Verifying  : 32:bind-utils-9.9.4-38.el7_3.x86_64                                                                                                     2/7 
  Verifying  : GeoIP-1.5.0-11.el7.x86_64                                                                                                               3/7 
  Verifying  : 32:bind-libs-lite-9.9.4-38.el7_3.x86_64                                                                                                 4/7 
  Verifying  : 32:bind-license-9.9.4-38.el7_3.noarch                                                                                                   5/7 
  Verifying  : 32:bind-license-9.9.4-29.el7_2.4.noarch                                                                                                 6/7 
  Verifying  : 32:bind-libs-lite-9.9.4-29.el7_2.4.x86_64                                                                                               7/7 

Installed:
  bind-utils.x86_64 32:9.9.4-38.el7_3                                                                                                                      

Dependency Installed:
  GeoIP.x86_64 0:1.5.0-11.el7                                              bind-libs.x86_64 32:9.9.4-38.el7_3                                             

Dependency Updated:
  bind-libs-lite.x86_64 32:9.9.4-38.el7_3                                       bind-license.noarch 32:9.9.4-38.el7_3                                      

Complete!

```
