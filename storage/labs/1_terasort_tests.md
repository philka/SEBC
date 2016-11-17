# teragen & terasort
## add new user
```
[root@ip-10-0-38-250 ec2-user]# useradd philka
```

## add hdfs directory and set permissions
```
[root@ip-10-0-38-250 ec2-user]# su hdfs
bash-4.2$ hdfs dfs -mkdir /user/philka
bash-4.2$ hdfs dfs -chown philka:philka /user/philka
bash-4.2$ hdfs dfs -ls /user
Found 5 items
drwx------   - hdfs   supergroup          0 2016-11-16 09:33 /user/hdfs
drwxrwxrwx   - mapred hadoop              0 2016-11-16 05:23 /user/history
drwxrwxr-t   - hive   hive                0 2016-11-16 05:31 /user/hive
drwxrwxr-x   - hue    hue                 0 2016-11-16 05:32 /user/hue
drwxr-xr-x   - philka philka              0 2016-11-16 11:01 /user/philka
```

## teragen: generate 10 gb file
```
[root@ip-10-0-38-250 ec2-user]# su philka
[philka@ip-10-0-38-250 ec2-user]$ time hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Dmapred.map.tasks=4 -D dfs.blocksize=32m -Dmapred.map.tasks.speculative.execution=false 100000000 /user/philka/terasort-input
...
    File System Counters
        FILE: Number of bytes read=0
        FILE: Number of bytes written=488304
        FILE: Number of read operations=0
        FILE: Number of large read operations=0
        FILE: Number of write operations=0
        HDFS: Number of bytes read=344
        HDFS: Number of bytes written=10000000000
        HDFS: Number of read operations=16
        HDFS: Number of large read operations=0
        HDFS: Number of write operations=8
    Job Counters 
        Launched map tasks=4
        Other local map tasks=4
        Total time spent by all maps in occupied slots (ms)=602806
        Total time spent by all reduces in occupied slots (ms)=0
        Total time spent by all map tasks (ms)=602806
        Total vcore-seconds taken by all map tasks=602806
        Total megabyte-seconds taken by all map tasks=617273344
    Map-Reduce Framework
        Map input records=100000000
        Map output records=100000000
        Input split bytes=344
        Spilled Records=0
        Failed Shuffles=0
        Merged Map outputs=0
        GC time elapsed (ms)=1694
        CPU time spent (ms)=161390
        Physical memory (bytes) snapshot=794607616
        Virtual memory (bytes) snapshot=6348951552
        Total committed heap usage (bytes)=840957952
    org.apache.hadoop.examples.terasort.TeraGen$Counters
        CHECKSUM=214760662691937609
    File Input Format Counters 
        Bytes Read=0
    File Output Format Counters 
        Bytes Written=10000000000

real    2m47.640s
user    0m6.059s
sys 0m0.268s
```

## ls generated files
```
[philka@ip-10-0-38-250 ec2-user]$ hdfs dfs -ls -h /user/philka/terasort-input
Found 5 items
-rw-r--r--   3 philka philka          0 2016-11-16 15:12 /user/philka/terasort-input/_SUCCESS
-rw-r--r--   3 philka philka      2.3 G 2016-11-16 15:12 /user/philka/terasort-input/part-m-00000
-rw-r--r--   3 philka philka      2.3 G 2016-11-16 15:11 /user/philka/terasort-input/part-m-00001
-rw-r--r--   3 philka philka      2.3 G 2016-11-16 15:11 /user/philka/terasort-input/part-m-00002
-rw-r--r--   3 philka philka      2.3 G 2016-11-16 15:12 /user/philka/terasort-input/part-m-00003
```

## terasort
```
[philka@ip-10-0-38-250 ec2-user]$ time hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar terasort /user/philka/terasort-input /user/philka/terasort-output
...
    File System Counters
        FILE: Number of bytes read=4446148477
        FILE: Number of bytes written=8826746274
        FILE: Number of read operations=0
        FILE: Number of large read operations=0
        FILE: Number of write operations=0
        HDFS: Number of bytes read=10000047400
        HDFS: Number of bytes written=10000000000
        HDFS: Number of read operations=918
        HDFS: Number of large read operations=0
        HDFS: Number of write operations=12
    Job Counters 
        Launched map tasks=300
        Launched reduce tasks=6
        Data-local map tasks=300
        Total time spent by all maps in occupied slots (ms)=2812650
        Total time spent by all reduces in occupied slots (ms)=614407
        Total time spent by all map tasks (ms)=2812650
        Total time spent by all reduce tasks (ms)=614407
        Total vcore-seconds taken by all map tasks=2812650
        Total vcore-seconds taken by all reduce tasks=614407
        Total megabyte-seconds taken by all map tasks=2880153600
        Total megabyte-seconds taken by all reduce tasks=629152768
    Map-Reduce Framework
        Map input records=100000000
        Map output records=100000000
        Map output bytes=10200000000
        Map output materialized bytes=4342784689
        Input split bytes=47400
        Combine input records=0
        Combine output records=0
        Reduce input groups=100000000
        Reduce shuffle bytes=4342784689
        Reduce input records=100000000
        Reduce output records=100000000
        Spilled Records=200000000
        Shuffled Maps =1800
        Failed Shuffles=0
        Merged Map outputs=1800
        GC time elapsed (ms)=42495
        CPU time spent (ms)=1435660
        Physical memory (bytes) snapshot=149707333632
        Virtual memory (bytes) snapshot=483755630592
        Total committed heap usage (bytes)=171944968192
    Shuffle Errors
        BAD_ID=0
        CONNECTION=0
        IO_ERROR=0
        WRONG_LENGTH=0
        WRONG_MAP=0
        WRONG_REDUCE=0
    File Input Format Counters 
        Bytes Read=10000000000
    File Output Format Counters 
        Bytes Written=10000000000
16/11/16 15:27:41 INFO terasort.TeraSort: done

real    6m33.830s
user    0m9.184s
sys 0m0.396s
```

---

## Links
https://www.michael-noll.com/blog/2011/04/09/benchmarking-and-stress-testing-an-hadoop-cluster-with-terasort-testdfsio-nnbench-mrbench/#terasort-benchmark-suite
