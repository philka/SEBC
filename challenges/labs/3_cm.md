# Install CDH

## Copy the statement `SHOW GRANTS FOR <database>` and the output for each of `rman`, `hive`, and `scm` into the file

```
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

MariaDB [(none)]> show grants for 'scm'@'%';
+----------------------------------------------------------------------------------------------------+
| Grants for scm@%                                                                                   |
+----------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'scm'@'%' IDENTIFIED BY PASSWORD '*4ACFE3202A5FF5CF467898FC58AAB1D615029441' |
| GRANT ALL PRIVILEGES ON `scm`.* TO 'scm'@'%'                                                       |
+----------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)
```

## Create user directories in HDFS for `bavaria` and `saxony`

**Command and output for `hdfs dfs -ls /user`**

```
[root@ip-10-0-215-18 ec2-user]# su hdfs
[hdfs@ip-10-0-215-18 ec2-user]$ hdfs dfs -mkdir /user/bavaria
[hdfs@ip-10-0-215-18 ec2-user]$ hdfs dfs -chown bavaria:bavaria /user/bavaria
[hdfs@ip-10-0-215-18 ec2-user]$ hdfs dfs -mkdir /user/saxony
[hdfs@ip-10-0-215-18 ec2-user]$ hdfs dfs -chown saxony:saxony /user/saxony
[hdfs@ip-10-0-215-18 ec2-user]$ hdfs dfs -ls /user
Found 8 items
drwxr-xr-x   - admin   admin               0 2016-11-18 05:38 /user/admin
drwxr-xr-x   - bavaria bavaria             0 2016-11-18 05:40 /user/bavaria
drwxr-xr-x   - hdfs    supergroup          0 2016-11-18 05:38 /user/hdfs
drwxrwxrwx   - mapred  hadoop              0 2016-11-18 05:33 /user/history
drwxrwxr-t   - hive    hive                0 2016-11-18 05:34 /user/hive
drwxrwxr-x   - hue     hue                 0 2016-11-18 05:35 /user/hue
drwxrwxr-x   - oozie   oozie               0 2016-11-18 05:35 /user/oozie
drwxr-xr-x   - saxony  saxony              0 2016-11-18 05:41 /user/saxony
```

**The output from the CM API call `../api/v12/hosts`**
```
[hdfs@ip-10-0-215-18 ec2-user]$ curl -X GET -u "admin:admin" http://54.201.57.117:7180/api/v12/hosts
{
  "items" : [ {
    "hostId" : "53803b69-448b-4e86-85aa-ce086c458ef8",
    "ipAddress" : "10.0.215.17",
    "hostname" : "ip-10-0-215-17.us-west-2.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-10-0-215-18.us-west-2.compute.internal:7180/cmf/hostRedirect/53803b69-448b-4e86-85aa-ce086c458ef8",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332311040
  }, {
    "hostId" : "d00d99e7-d997-4b25-9359-256ea0e72dff",
    "ipAddress" : "10.0.215.18",
    "hostname" : "ip-10-0-215-18.us-west-2.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-10-0-215-18.us-west-2.compute.internal:7180/cmf/hostRedirect/d00d99e7-d997-4b25-9359-256ea0e72dff",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332311040
  }, {
    "hostId" : "82d2eacb-43fb-4fdd-bf0c-ec068a2019ca",
    "ipAddress" : "10.0.215.19",
    "hostname" : "ip-10-0-215-19.us-west-2.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-10-0-215-18.us-west-2.compute.internal:7180/cmf/hostRedirect/82d2eacb-43fb-4fdd-bf0c-ec068a2019ca",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332311040
  }, {
    "hostId" : "84fd339c-af3c-4638-9d65-88c429fd7207",
    "ipAddress" : "10.0.215.20",
    "hostname" : "ip-10-0-215-20.us-west-2.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-10-0-215-18.us-west-2.compute.internal:7180/cmf/hostRedirect/84fd339c-af3c-4638-9d65-88c429fd7207",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332311040
  }, {
    "hostId" : "132b7cd9-70c5-46e3-88b6-a785fed14b7d",
    "ipAddress" : "10.0.215.21",
    "hostname" : "ip-10-0-215-21.us-west-2.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-10-0-215-18.us-west-2.compute.internal:7180/cmf/hostRedirect/132b7cd9-70c5-46e3-88b6-a785fed14b7d",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 15332311040
  } ]
```

## Login to the Hue console and install the Hive sample data

    * Save a screenshot of the Hue home page into `challenges/labs/3_hue_installed.png`