# Install Cloudera Manager

## installation

**Configure the CM repo to install the `5.7.4` release**
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

```
[root@ip-10-0-215-18 ec2-user]# ls /etc/yum.repos.d
cloudera-manager.repo  redhat.repo  redhat-rhui-client-config.repo  redhat-rhui.repo  rhui-load-balancers.conf
```

**List the command and output of `ls /etc/yum.repos.d`**
```
ls /etc/yum.repos.d
cloudera-manager.repo  redhat.repo  redhat-rhui-client-config.repo  redhat-rhui.repo  rhui-load-balancers.conf
```

---

## Configure Cloudera Manager

**Grant `temp` access to your MySQL server _only_ from the CM node (no host wildcard)**
```
grant all on *.* TO 'temp'@'ec2-54-201-57-118.us-west-2.compute.amazonaws.com' IDENTIFIED BY 'temp' with grant option;
```

**Copy your full `scm_prepare_database.sh` command and output into the same file**
```
[root@ip-10-0-215-18 ec2-user]# /usr/share/cmf/schema/scm_prepare_database.sh mysql -h ip-10-0-215-17.us-west-2.compute.internal -utemp -ptemp --scm-host ip-10-0-215-18.us-west-2.compute.internal scm scm scm
JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.7.0_67-cloudera/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!
```

---

## Start the Cloudera Manager server

```
service cloudera-scm-server start
```
