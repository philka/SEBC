## yarn test

**preparation**
```
su hdfs
hdfs dfs -mkdir /user/results
```

**yarntest.sh**
```
#!/bin/sh
# Confirm the path values given below correspond to your installation

HADOOP_MR=/opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce
HADOOP_PATH=/opt/cloudera/parcels/CDH/bin

# Mark start of the loop
echo Testing loop started on `date`

# Mapper containers
for i in 32 8 2
do
   # Reducer containers
   for j in 32 8 2
   do                 
      # Container memory
      for k in 2048 512
      do
         # Set mapper JVM heap 
         MAP_MB=`echo "($k*0.8)/1" | bc` 

         # Set reducer JVM heap 
         RED_MB=`echo "($k*0.8)/1" | bc` 

        time $HADOOP_PATH/hadoop jar $HADOOP_MR/hadoop-examples.jar teragen \
                     -Dmapreduce.map.tasks=$i \
                     -Dmapreduce.map.memory.mb=$k \
                     -Dmapreduce.map.java.opts.max.heap=$MAP_MB \
                     100000000 /tmp/results/tg-10GB-${i}-${j}-${k} 1>tera_${i}_${j}_${k}.out 2>tera_${i}_${j}_${k}.err                       

       time $HADOOP_PATH/hadoop jar $HADOOP_MR/hadoop-examples.jar terasort \
                     -Dmapreduce.map.tasks=$i \
                     -Dmapreduce.reduce.tasks=$j \
                     -Dmapreduce.map.memory.mb=$k \
                     -Dmapreduce.map.java.opts.max.heap=$MAP_MB \
                     -Dmapreduce.reduce.memory.mb=$k \
                     -Dmapreduce.reduce.java.opts.max.heap=$RED_MB \
                 /tmp/results/tg-10GB-${i}-${j}-${k}  \
                     /tmp/results/ts-10GB-${i}-${j}-${k} 1>>tera_${i}_${j}_${k}.out 2>>tera_${i}_${j}_${k}.err                         

        echo "Loop i=$i, j=$j, k=$k ended on `date --rfc-3339=seconds`"

        $HADOOP_PATH/hadoop fs -rm -r -skipTrash /tmp/results/tg-10GB-${i}-${j}-${k}                         
        $HADOOP_PATH/hadoop fs -rm -r -skipTrash /tmp/results/ts-10GB-${i}-${j}-${k}                 
      done
   done
done

echo Testing loop ended on `date`
```

**execute**
```
./yarntest.sh 2>&1 yarntest.log
hdfs dfs -rm -r -skipTrash /tmp/results

```