1. From the accounts table, import only the primary key, along with the first name, last name to
HDFS directory /loudacre/accounts/user_info. Please save the file in text format with tab
delimiters.

```
sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training \
--table accounts  --target-dir /loudacre/accounts/user_info \
--columns "acct_num, first_name, last_name" --fields-terminated-by "\t"
```

2. This time save the same in parquet format with snappy compression. Save it in
/loudacre/accounts/user_compressed. Provide.a screenshot of HUE with the new directory
created.
```
sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training \
--table accounts  --target-dir /loudacre/accounts/user_compressed_1 \
--columns "acct_num, first_name, last_name" --fields-terminated-by "\t" \
--compression-codec \
org.apache.hadoop.io.compress.SnappyCodec
```


19/03/10 22:37:39 INFO mapreduce.Job: Job job_1552272159047_0005 running in uber mode : false
19/03/10 22:37:39 INFO mapreduce.Job:  map 0% reduce 0%
19/03/10 22:38:06 INFO mapreduce.Job:  map 25% reduce 0%
19/03/10 22:38:30 INFO mapreduce.Job:  map 50% reduce 0%
19/03/10 22:38:54 INFO mapreduce.Job:  map 75% reduce 0%
19/03/10 22:39:15 INFO mapreduce.Job:  map 100% reduce 0%
19/03/10 22:39:16 INFO mapreduce.Job: Job job_1552272159047_0005 completed successfully
19/03/10 22:39:17 INFO mapreduce.Job: Counters: 30
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=561192
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=470
                HDFS: Number of bytes written=1839111
                HDFS: Number of read operations=16
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=8
        Job Counters
                Launched map tasks=4
                Other local map tasks=4
                Total time spent by all maps in occupied slots (ms)=0
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=88628
                Total vcore-seconds taken by all map tasks=88628
                Total megabyte-seconds taken by all map tasks=22688768
        Map-Reduce Framework
                Map input records=129761
                Map output records=129761
                Input split bytes=470
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=549
                CPU time spent (ms)=21480
                Physical memory (bytes) snapshot=509874176
                Virtual memory (bytes) snapshot=8283578368
                Total committed heap usage (bytes)=251920384
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=1839111
                




3.Finally save in /loudacre/accounts/CA only clients whose state is from California. Save the file
in parquet format and compressed using gzip. From the terminal, display some of the records
that you just imported. Take a screenshot and save it as CA_only

```
sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training \
--table accounts  --target-dir /loudacre/accounts/CA \
--columns "acct_num, first_name, last_name" --fields-terminated-by "\t" \
--where "state = 'CA' "
```

19/03/10 22:41:17 INFO mapreduce.Job: Running job: job_1552272159047_0006
19/03/10 22:41:52 INFO mapreduce.Job: Job job_1552272159047_0006 running in uber mode : false
19/03/10 22:41:52 INFO mapreduce.Job:  map 0% reduce 0%
19/03/10 22:42:19 INFO mapreduce.Job:  map 25% reduce 0%
19/03/10 22:42:44 INFO mapreduce.Job:  map 50% reduce 0%
19/03/10 22:43:08 INFO mapreduce.Job:  map 75% reduce 0%
19/03/10 22:43:34 INFO mapreduce.Job:  map 100% reduce 0%
19/03/10 22:43:35 INFO mapreduce.Job: Job job_1552272159047_0006 completed successfully
19/03/10 22:43:36 INFO mapreduce.Job: Counters: 30
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=561600
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=470
                HDFS: Number of bytes written=1859432
                HDFS: Number of read operations=16
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=8
        Job Counters
                Launched map tasks=4
                Other local map tasks=4
                Total time spent by all maps in occupied slots (ms)=0
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=95776
                Total vcore-seconds taken by all map tasks=95776
                Total megabyte-seconds taken by all map tasks=24518656
        Map-Reduce Framework
                Map input records=92416
                Map output records=92416
                Input split bytes=470
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=424
                CPU time spent (ms)=20330
                Physical memory (bytes) snapshot=508575744
                Virtual memory (bytes) snapshot=8262348800
                Total committed heap usage (bytes)=251920384
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=1859432
19/03/10 22:43:36 INFO mapreduce.ImportJobBase: Transferred 1.7733 MB in 151.3564 seconds (11.9972 KB/sec)
19/03/10 22:43:36 INFO mapreduce.ImportJobBase: Retrieved 92416 records.
