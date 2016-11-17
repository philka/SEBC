## Snapshots
### file to hdfs
```
bash-4.2$ hdfs dfs -put /tmp/SEBC-master.zip /user/hdfs/precious
bash-4.2$ hdfs dfs -ls /user/hdfs/precious
Found 1 items
-rw-r--r--   3 hdfs supergroup     410158 2016-11-16 09:56 /user/hdfs/precious/SEBC-master.zip
```

### allow snapshot for dir
```
bash-4.2$ hdfs dfsadmin -allowSnapshot /user/hdfs/precious/
Allowing snaphot on /user/hdfs/precious/ succeeded
```

### create snapshot for dir
```
bash-4.2$ hdfs dfs -createSnapshot /user/hdfs/precious/ sebc-hdfs-test
Created snapshot /user/hdfs/precious/.snapshot/sebc-hdfs-test
```

### delete dir does not work
```
bash-4.2$ hdfs dfs -rm -r /user/hdfs/precious
rm: Failed to move to trash: hdfs://ip-10-0-38-247.us-west-2.compute.internal:8020/user/hdfs/precious: The directory /user/hdfs/precious cannot be deleted since /user/hdfs/precious is snapshottable and already has snapshots
```

### delte file does work
```
bash-4.2$ hdfs dfs -rm -r /user/hdfs/precious/SEBC-master.zip
16/11/16 10:03:41 INFO fs.TrashPolicyDefault: Moved: 'hdfs://ip-10-0-38-247.us-west-2.compute.internal:8020/user/hdfs/precious/SEBC-master.zip' to trash at: hdfs://ip-10-0-38-247.us-west-2.compute.internal:8020/user/hdfs/.Trash/Current/user/hdfs/precious/SEBC-master.zip
```

### show snapshot in dir
```
bash-4.2$ hdfs dfs -ls -R /user/hdfs/precious/.snapshot
drwxr-xr-x   - hdfs supergroup          0 2016-11-16 10:00 /user/hdfs/precious/.snapshot/sebc-hdfs-test
-rw-r--r--   3 hdfs supergroup     410158 2016-11-16 09:56 /user/hdfs/precious/.snapshot/sebc-hdfs-test/SEBC-master.zip
```

### backup snapshot file
```
bash-4.2$ hdfs dfs -cp /user/hdfs/precious/.snapshot/sebc-hdfs-test/SEBC-master.zip /user/hdfs/precious
bash-4.2$ hdfs dfs -ls /user/hdfs/precious
Found 1 items
-rw-r--r--   3 hdfs supergroup     410158 2016-11-16 10:06 /user/hdfs/precious/SEBC-master.zip
```