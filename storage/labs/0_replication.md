## generate files with teragen
```
bash-4.2$ hadoop jar /opt/cloudera/parcels/CDH-5.8.3-1.cdh5.8.3.p0.2/jars/hadoop-examples.jar teragen -Dmapred.map.tasks=50 -Dmapred.map.tasks.speculative.execution=false 10000000 terasort
16/11/16 07:39:56 INFO client.RMProxy: Connecting to ResourceManager at ip-10-0-38-247.us-west-2.compute.internal/10.0.38.247:8032
16/11/16 07:39:56 INFO terasort.TeraSort: Generating 10000000 using 50
16/11/16 07:39:56 INFO mapreduce.JobSubmitter: number of splits:50
16/11/16 07:39:56 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
16/11/16 07:39:56 INFO Configuration.deprecation: mapred.map.tasks.speculative.execution is deprecated. Instead, use mapreduce.map.speculative
16/11/16 07:39:57 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1479291819276_0001
16/11/16 07:39:57 INFO impl.YarnClientImpl: Submitted application application_1479291819276_0001
16/11/16 07:39:57 INFO mapreduce.Job: The url to track the job: http://ip-10-0-38-247.us-west-2.compute.internal:8088/proxy/application_1479291819276_0001/
16/11/16 07:39:57 INFO mapreduce.Job: Running job: job_1479291819276_0001
16/11/16 07:40:03 INFO mapreduce.Job: Job job_1479291819276_0001 running in uber mode : false
16/11/16 07:40:03 INFO mapreduce.Job:  map 0% reduce 0%
16/11/16 07:40:13 INFO mapreduce.Job:  map 4% reduce 0%
16/11/16 07:40:14 INFO mapreduce.Job:  map 6% reduce 0%
16/11/16 07:40:18 INFO mapreduce.Job:  map 18% reduce 0%
16/11/16 07:40:19 INFO mapreduce.Job:  map 22% reduce 0%
16/11/16 07:40:23 INFO mapreduce.Job:  map 26% reduce 0%
16/11/16 07:40:24 INFO mapreduce.Job:  map 28% reduce 0%
16/11/16 07:40:29 INFO mapreduce.Job:  map 32% reduce 0%
16/11/16 07:40:30 INFO mapreduce.Job:  map 44% reduce 0%
16/11/16 07:40:32 INFO mapreduce.Job:  map 48% reduce 0%
16/11/16 07:40:33 INFO mapreduce.Job:  map 50% reduce 0%
16/11/16 07:40:41 INFO mapreduce.Job:  map 54% reduce 0%
16/11/16 07:40:42 INFO mapreduce.Job:  map 72% reduce 0%
16/11/16 07:40:49 INFO mapreduce.Job:  map 74% reduce 0%
16/11/16 07:40:50 INFO mapreduce.Job:  map 78% reduce 0%
16/11/16 07:40:53 INFO mapreduce.Job:  map 80% reduce 0%
16/11/16 07:40:54 INFO mapreduce.Job:  map 86% reduce 0%
16/11/16 07:40:55 INFO mapreduce.Job:  map 94% reduce 0%
16/11/16 07:40:58 INFO mapreduce.Job:  map 98% reduce 0%
16/11/16 07:40:59 INFO mapreduce.Job:  map 100% reduce 0%
16/11/16 07:40:59 INFO mapreduce.Job: Job job_1479291819276_0001 completed successfully
16/11/16 07:40:59 INFO mapreduce.Job: Counters: 31
    File System Counters
        FILE: Number of bytes read=0
        FILE: Number of bytes written=6102940
        FILE: Number of read operations=0
        FILE: Number of large read operations=0
        FILE: Number of write operations=0
        HDFS: Number of bytes read=4247
        HDFS: Number of bytes written=1000000000
        HDFS: Number of read operations=200
        HDFS: Number of large read operations=0
        HDFS: Number of write operations=100
    Job Counters 
        Launched map tasks=50
        Other local map tasks=50
        Total time spent by all maps in occupied slots (ms)=499891
        Total time spent by all reduces in occupied slots (ms)=0
        Total time spent by all map tasks (ms)=499891
        Total vcore-seconds taken by all map tasks=499891
        Total megabyte-seconds taken by all map tasks=511888384
    Map-Reduce Framework
        Map input records=10000000
        Map output records=10000000
        Input split bytes=4247
        Spilled Records=0
        Failed Shuffles=0
        Merged Map outputs=0
        GC time elapsed (ms)=6703
        CPU time spent (ms)=129200
        Physical memory (bytes) snapshot=10824597504
        Virtual memory (bytes) snapshot=78889463808
        Total committed heap usage (bytes)=14496563200
    org.apache.hadoop.examples.terasort.TeraGen$Counters
        CHECKSUM=21472776955442690
    File Input Format Counters 
        Bytes Read=0
    File Output Format Counters 
        Bytes Written=1000000000
```
```
hadoop jar /opt/cloudera/parcels/CDH-5.8.3-1.cdh5.8.3.p0.2/jars/hadoop-examples.jar teragen -Dmapred.map.tasks=50 10000000 terasort
```

## run fsck
```
bash-4.2$ hdfs fsck /user/hdfs/terasort -files -blocks
Connecting to namenode via http://ip-10-0-38-247.us-west-2.compute.internal:50070
FSCK started by hdfs (auth:SIMPLE) from /10.0.38.250 for path /user/hdfs/terasort at Wed Nov 16 10:47:17 EST 2016
/user/hdfs/terasort <dir>
/user/hdfs/terasort/_SUCCESS 0 bytes, 0 block(s):  OK

/user/hdfs/terasort/part-m-00000 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742050_1226 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00001 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742057_1233 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00002 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742060_1236 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00003 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742051_1227 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00004 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742055_1231 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00005 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742058_1234 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00006 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742049_1225 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00007 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742056_1232 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00008 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742059_1235 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00009 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742054_1230 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00010 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742053_1229 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00011 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742062_1238 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00012 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742061_1237 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00013 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742063_1239 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00014 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742065_1241 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00015 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742064_1240 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00016 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742066_1242 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00017 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742067_1243 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00018 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742068_1244 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00019 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742071_1247 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00020 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742069_1245 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00021 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742070_1246 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00022 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742073_1249 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00023 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742072_1248 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00024 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742074_1250 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00025 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742084_1260 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00026 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742083_1259 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00027 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742077_1253 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00028 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742082_1258 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00029 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742079_1255 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00030 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742081_1257 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00031 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742080_1256 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00032 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742086_1262 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00033 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742076_1252 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00034 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742078_1254 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00035 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742085_1261 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00036 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742087_1263 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00037 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742088_1264 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00038 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742089_1265 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00039 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742090_1266 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00040 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742096_1272 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00041 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742091_1267 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00042 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742095_1271 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00043 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742092_1268 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00044 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742093_1269 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00045 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742097_1273 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00046 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742094_1270 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00047 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742099_1275 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00048 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742098_1274 len=20000000 Live_repl=3

/user/hdfs/terasort/part-m-00049 20000000 bytes, 1 block(s):  OK
0. BP-993951265-10.0.38.247-1479284444919:blk_1073742100_1276 len=20000000 Live_repl=3

Status: HEALTHY
 Total size:    1000000000 B
 Total dirs:    1
 Total files:   51
 Total symlinks:        0
 Total blocks (validated):  50 (avg. block size 20000000 B)
 Minimally replicated blocks:   50 (100.0 %)
 Over-replicated blocks:    0 (0.0 %)
 Under-replicated blocks:   0 (0.0 %)
 Mis-replicated blocks:     0 (0.0 %)
 Default replication factor:    3
 Average block replication: 3.0
 Corrupt blocks:        0
 Missing replicas:      0 (0.0 %)
 Number of data-nodes:      3
 Number of racks:       1
FSCK ended at Wed Nov 16 10:47:17 EST 2016 in 15 milliseconds


The filesystem under path '/user/hdfs/terasort' is HEALTHY
```