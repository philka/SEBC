# HDFS Testing

## `teragen`

**generate files**

```
[bavaria@ip-10-0-215-18 ec2-user]$ time hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Dmapred.map.tasks=8 -D dfs.blocksize=16m -Dmapred.map.tasks.speculative.execution=false 51200000 /user/bavaria/tgen512m
16/11/18 05:49:30 INFO client.RMProxy: Connecting to ResourceManager at ip-10-0-215-18.us-west-2.compute.internal/10.0.215.18:8032
..
16/11/18 05:50:45 INFO mapreduce.Job: Job job_1479465246240_0002 completed successfully
16/11/18 05:50:45 INFO mapreduce.Job: Counters: 31
    File System Counters
        FILE: Number of bytes read=0
        FILE: Number of bytes written=956680
        FILE: Number of read operations=0
        FILE: Number of large read operations=0
        FILE: Number of write operations=0
        HDFS: Number of bytes read=682
        HDFS: Number of bytes written=5120000000
        HDFS: Number of read operations=32
        HDFS: Number of large read operations=0
        HDFS: Number of write operations=16
    Job Counters 
        Launched map tasks=8
        Other local map tasks=8
        Total time spent by all maps in occupied slots (ms)=505074
        Total time spent by all reduces in occupied slots (ms)=0
        Total time spent by all map tasks (ms)=505074
        Total vcore-seconds taken by all map tasks=505074
        Total megabyte-seconds taken by all map tasks=517195776
    Map-Reduce Framework
        Map input records=51200000
        Map output records=51200000
        Input split bytes=682
        Spilled Records=0
        Failed Shuffles=0
        Merged Map outputs=0
        GC time elapsed (ms)=1579
        CPU time spent (ms)=110050
        Physical memory (bytes) snapshot=2779574272
        Virtual memory (bytes) snapshot=12628910080
        Total committed heap usage (bytes)=2902982656
    org.apache.hadoop.examples.terasort.TeraGen$Counters
        CHECKSUM=109963291816450258
    File Input Format Counters 
        Bytes Read=0
    File Output Format Counters 
        Bytes Written=5120000000

real    1m16.817s
user    0m6.091s
sys 0m0.276s
```

**`hdfs dfs -ls /user/bavaria/tgen512m`**

```
[bavaria@ip-10-0-215-18 ec2-user]$ hdfs dfs -ls /user/bavaria/tgen512m
Found 9 items
-rw-r--r--   3 bavaria bavaria          0 2016-11-18 05:50 /user/bavaria/tgen512m/_SUCCESS
-rw-r--r--   3 bavaria bavaria  640000000 2016-11-18 05:50 /user/bavaria/tgen512m/part-m-00000
-rw-r--r--   3 bavaria bavaria  640000000 2016-11-18 05:50 /user/bavaria/tgen512m/part-m-00001
-rw-r--r--   3 bavaria bavaria  640000000 2016-11-18 05:50 /user/bavaria/tgen512m/part-m-00002
-rw-r--r--   3 bavaria bavaria  640000000 2016-11-18 05:50 /user/bavaria/tgen512m/part-m-00003
-rw-r--r--   3 bavaria bavaria  640000000 2016-11-18 05:50 /user/bavaria/tgen512m/part-m-00004
-rw-r--r--   3 bavaria bavaria  640000000 2016-11-18 05:50 /user/bavaria/tgen512m/part-m-00005
-rw-r--r--   3 bavaria bavaria  640000000 2016-11-18 05:50 /user/bavaria/tgen512m/part-m-00006
-rw-r--r--   3 bavaria bavaria  640000000 2016-11-18 05:50 /user/bavaria/tgen512m/part-m-00007
```

**Show how many blocks are linked to this directory**
```
[bavaria@ip-10-0-215-18 ec2-user]$ hdfs fsck /user/bavaria/tgen512m -blocks
Connecting to namenode via http://ip-10-0-215-18.us-west-2.compute.internal:50070
FSCK started by bavaria (auth:SIMPLE) from /10.0.215.18 for path /user/bavaria/tgen512m at Fri Nov 18 05:54:05 EST 2016
.........Status: HEALTHY
 Total size:    5120000000 B
 Total dirs:    1
 Total files:   9
 Total symlinks:        0
 Total blocks (validated):  312 (avg. block size 16410256 B)
 Minimally replicated blocks:   312 (100.0 %)
 Over-replicated blocks:    0 (0.0 %)
 Under-replicated blocks:   0 (0.0 %)
 Mis-replicated blocks:     0 (0.0 %)
 Default replication factor:    3
 Average block replication: 3.0
 Corrupt blocks:        0
 Missing replicas:      0 (0.0 %)
 Number of data-nodes:      3
 Number of racks:       1
FSCK ended at Fri Nov 18 05:54:05 EST 2016 in 10 milliseconds


The filesystem under path '/user/bavaria/tgen512m' is HEALTHY
```
