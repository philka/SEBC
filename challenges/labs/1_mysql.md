# Install MySQL

## Installation
In Version 7 Red Hat changed MySql to MariaDB. As noted in the Installation Lab (`If you have chosen RHEL/CentOS 7.x, use MariaDB instead.`) and since I installed OS `RHEL-7.2` I therefore choose MariaDB as Database Server. Furthermore I had some issues with MySQL and RHEL7 in previous installation and therefore choosing MariDB for compability.

* http://www.cloudera.com/downloads/manager/5-7-4.html
* https://mariadb.com/resources/blog/rhel7-transition-mysql-mariadb-first-look

**install server**
```
yum install mariadb-server
```

**edit `vi /etc/my.cnf`**
...

**start mariadb**
```
service mariadb start
```

**add to start**
```
systemctl enable mariadb
```

**set root password**
```
sudo /usr/bin/mysql_secure_installation
```

**install jdbc drivers on all nodes**
```
tar zxvf mysql-connector-java-5.1.40.tar.gz
sudo su
mkdir -p /usr/share/java/
cp /home/ec2-user/mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/mysql-connector-java.jar
```

---

## Delete the test database

Test database alread deleted within `/usr/bin/mysql_secure_installation`:
```
Remove test database and access to it? [Y/n] Y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!
```

---

## Create Databases
Create the following databases:
* scm
* 
* rman
* hive
* oozie
* hue
* sentry

**create databases and rights**
```
create database scm DEFAULT CHARACTER SET utf8;
create database rman DEFAULT CHARACTER SET utf8;
create database hive DEFAULT CHARACTER SET utf8;
create database oozie DEFAULT CHARACTER SET utf8;
create database hue DEFAULT CHARACTER SET utf8;
create database sentry DEFAULT CHARACTER SET utf8;
grant all on scm.* TO 'scm'@'%' IDENTIFIED BY 'admin';
grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'admin';
grant all on hive.* TO 'hive'@'%' IDENTIFIED BY 'admin';
grant all on oozie.* TO 'oozie'@'%' IDENTIFIED BY 'admin';
grant all on hue.* TO 'hue'@'%' IDENTIFIED BY 'admin';
grant all on sentry.* TO 'sentry'@'%' IDENTIFIED BY 'admin';
```

---

## The command and output of mysql --version
```
[root@ip-10-0-215-17 ec2-user]# mysql --version
mysql  Ver 15.1 Distrib 5.5.52-MariaDB, for Linux (x86_64) using readline 5.1
```

---

## The command and output for a list of databases in MySQL
```
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| hue                |
| mysql              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
+--------------------+
9 rows in set (0.01 sec)
```

---

## The command and output for a list of grants in MySQL
```
MariaDB [(none)]> show grants for 'scm'@'%';
+----------------------------------------------------------------------------------------------------+
| Grants for scm@%                                                                                   |
+----------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'scm'@'%' IDENTIFIED BY PASSWORD '*4ACFE3202A5FF5CF467898FC58AAB1D615029441' |
| GRANT ALL PRIVILEGES ON `scm`.* TO 'scm'@'%'                                                       |
+----------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

MariaDB [(none)]> show grants for 'rman'@'%';
+-----------------------------------------------------------------------------------------------------+
| Grants for rman@%                                                                                   |
+-----------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'rman'@'%' IDENTIFIED BY PASSWORD '*4ACFE3202A5FF5CF467898FC58AAB1D615029441' |
| GRANT ALL PRIVILEGES ON `rman`.* TO 'rman'@'%'                                                      |
+-----------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

MariaDB [(none)]> show grants for 'hive'@'%';
+-----------------------------------------------------------------------------------------------------+
| Grants for hive@%                                                                                   |
+-----------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'hive'@'%' IDENTIFIED BY PASSWORD '*4ACFE3202A5FF5CF467898FC58AAB1D615029441' |
| GRANT ALL PRIVILEGES ON `hive`.* TO 'hive'@'%'                                                      |
+-----------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

MariaDB [(none)]> show grants for 'oozie'@'%';
+------------------------------------------------------------------------------------------------------+
| Grants for oozie@%                                                                                   |
+------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'oozie'@'%' IDENTIFIED BY PASSWORD '*4ACFE3202A5FF5CF467898FC58AAB1D615029441' |
| GRANT ALL PRIVILEGES ON `oozie`.* TO 'oozie'@'%'                                                     |
+------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

MariaDB [(none)]> show grants for 'hue'@'%';
+----------------------------------------------------------------------------------------------------+
| Grants for hue@%                                                                                   |
+----------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'hue'@'%' IDENTIFIED BY PASSWORD '*4ACFE3202A5FF5CF467898FC58AAB1D615029441' |
| GRANT ALL PRIVILEGES ON `hue`.* TO 'hue'@'%'                                                       |
+----------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

MariaDB [(none)]> show grants for 'sentry'@'%';
+-------------------------------------------------------------------------------------------------------+
| Grants for sentry@%                                                                                   |
+-------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'sentry'@'%' IDENTIFIED BY PASSWORD '*4ACFE3202A5FF5CF467898FC58AAB1D615029441' |
| GRANT ALL PRIVILEGES ON `sentry`.* TO 'sentry'@'%'                                                    |
+-------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)
```
