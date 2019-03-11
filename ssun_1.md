1. From the accounts table, import only the primary key, along with the first name, last name to
HDFS directory /loudacre/accounts/user_info. Please save the file in text format with tab
delimiters.

```
sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training \
--table accounts  --target-dir /loudacre/accounts/user_info \
--columns "acct_num, first_name, last_name" --fields-terminated-by "\t"
```
```
1	Donald	Becton
2	Donna	Jones
3	Dorthy	Chalmers
4	Leila	Spencer
5	Anita	Laughlin
6	Stevie	Bridge
7	David	Eggers
8	Dorothy	Koopman
9	Kara	Kohl
10	Diane	Nelson
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
```
0000000: 	00 03 55 32 00 02 71 3e b2 aa 0d 40 31 09 44 6f	  ..U2..q>...@1.Do
0000010: 	6e 61 6c 64 09 42 65 63 74 6f 6e 0a 32 01 10 f0	  nald.Becton.2...
0000020: 	56 6e 61 09 4a 6f 6e 65 73 0a 33 09 44 6f 72 74	  Vna.Jones.3.Dort
0000030: 	68 79 09 43 68 61 6c 6d 65 72 73 0a 34 09 4c 65	  hy.Chalmers.4.Le
0000040: 	69 6c 61 09 53 70 65 6e 63 65 72 0a 35 09 41 6e	  ila.Spencer.5.An
0000050: 	69 74 61 09 4c 61 75 67 68 6c 69 6e 0a 36 09 53	  ita.Laughlin.6.S
0000060: 	74 65 76 69 65 09 42 72 69 64 67 65 0a 37 09 44	  tevie.Bridge.7.D
```
19/03/10 22:37:39 INFO mapreduce.Job: Job job_1552272159047_0005 running in uber mode : false     \
19/03/10 22:37:39 INFO mapreduce.Job:  map 0% reduce 0%                                           \
19/03/10 22:38:06 INFO mapreduce.Job:  map 25% reduce 0%                                          \
19/03/10 22:38:30 INFO mapreduce.Job:  map 50% reduce 0%                                          \
19/03/10 22:38:54 INFO mapreduce.Job:  map 75% reduce 0%                                          \
19/03/10 22:39:15 INFO mapreduce.Job:  map 100% reduce 0%                                         \
19/03/10 22:39:16 INFO mapreduce.Job: Job job_1552272159047_0005 completed successfully           \
19/03/10 22:39:17 INFO mapreduce.Job: Counters: 30                                                \
        File System Counters                                                                      \
                FILE: Number of bytes read=0                                                      \
                FILE: Number of bytes written=561192                                              \
                FILE: Number of read operations=0                                                 \
                FILE: Number of large read operations=0                                           \
                FILE: Number of write operations=0                                                \
                HDFS: Number of bytes read=470                                                    \
                HDFS: Number of bytes written=1839111                                             \
                HDFS: Number of read operations=16                                                \
                HDFS: Number of large read operations=0                                           \
                HDFS: Number of write operations=8                                                \
        Job Counters                                                                              \
                Launched map tasks=4                                                              \
                Other local map tasks=4                                                           \
                Total time spent by all maps in occupied slots (ms)=0                             \
                Total time spent by all reduces in occupied slots (ms)=0                          \
                Total time spent by all map tasks (ms)=88628                                      \
                Total vcore-seconds taken by all map tasks=88628                                  \
                Total megabyte-seconds taken by all map tasks=22688768                            \
        Map-Reduce Framework                                                                      \
                Map input records=129761                                                          \
                Map output records=129761                                                         \
                Input split bytes=470                                                             \
                Spilled Records=0                                                                 \
                Failed Shuffles=0                                                                 \
                Merged Map outputs=0                                                              \
                GC time elapsed (ms)=549                                                          \
                CPU time spent (ms)=21480                                                         \
                Physical memory (bytes) snapshot=509874176                                        \
                Virtual memory (bytes) snapshot=8283578368                                        \
                Total committed heap usage (bytes)=251920384                                      \
        File Input Format Counters                                                                \
                Bytes Read=0                                                                      \
        File Output Format Counters                                                               \
                Bytes Written=1839111
                




3.Finally save in /loudacre/accounts/CA only clients whose state is from California. Save the file
in parquet format and compressed using gzip. From the terminal, display some of the records
that you just imported. Take a screenshot and save it as CA_only

```
sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training \
--table accounts  --target-dir /loudacre/accounts/CA_1 \
--columns "acct_num, first_name, last_name, state" --fields-terminated-by "\t" \
--where "state = 'CA' " 
```
```
1	Donald	Becton	CA
2	Donna	Jones	CA
3	Dorthy	Chalmers	CA
4	Leila	Spencer	CA
5	Anita	Laughlin	CA
6	Stevie	Bridge	CA
7	David	Eggers	CA
8	Dorothy	Koopman	CA
9	Kara	Kohl	CA
10	Diane	Nelson	CA
```
                                                                                                   \
19/03/10 22:41:17 INFO mapreduce.Job: Running job: job_1552272159047_0006                          \
19/03/10 22:41:52 INFO mapreduce.Job: Job job_1552272159047_0006 running in uber mode : false      \
19/03/10 22:41:52 INFO mapreduce.Job:  map 0% reduce 0%                                            \
19/03/10 22:42:19 INFO mapreduce.Job:  map 25% reduce 0%                                           \
19/03/10 22:42:44 INFO mapreduce.Job:  map 50% reduce 0%                                           \
19/03/10 22:43:08 INFO mapreduce.Job:  map 75% reduce 0%                                           \
19/03/10 22:43:34 INFO mapreduce.Job:  map 100% reduce 0%                                          \
19/03/10 22:43:35 INFO mapreduce.Job: Job job_1552272159047_0006 completed successfully            \
19/03/10 22:43:36 INFO mapreduce.Job: Counters: 30                                                 \
        File System Counters                                                                       \
                FILE: Number of bytes read=0                                                       \
                FILE: Number of bytes written=561600                                               \
                FILE: Number of read operations=0                                                  \
                FILE: Number of large read operations=0                                            \
                FILE: Number of write operations=0                                                 \
                HDFS: Number of bytes read=470                                                     \
                HDFS: Number of bytes written=1859432                                              \
                HDFS: Number of read operations=16                                                 \
                HDFS: Number of large read operations=0                                            \
                HDFS: Number of write operations=8                                                 \
        Job Counters                                                                               \
                Launched map tasks=4                                                               \
                Other local map tasks=4                                                            \
                Total time spent by all maps in occupied slots (ms)=0                              \
                Total time spent by all reduces in occupied slots (ms)=0                           \
                Total time spent by all map tasks (ms)=95776                                       \
                Total vcore-seconds taken by all map tasks=95776                                   \
                Total megabyte-seconds taken by all map tasks=24518656                             \
        Map-Reduce Framework                                                                       \
                Map input records=92416                                                            \
                Map output records=92416                                                           \
                Input split bytes=470                                                              \
                Spilled Records=0                                                                  \
                Failed Shuffles=0                                                                  \
                Merged Map outputs=0                                                               \
                GC time elapsed (ms)=424                                                           \
                CPU time spent (ms)=20330                                                          \
                Physical memory (bytes) snapshot=508575744                                         \
                Virtual memory (bytes) snapshot=8262348800                                         \
                Total committed heap usage (bytes)=251920384                                       \
        File Input Format Counters                                                                 \
                Bytes Read=0                                                                       \
        File Output Format Counters                                                                \
                Bytes Written=1859432\
19/03/10 22:43:36 INFO mapreduce.ImportJobBase: Transferred 1.7733 MB in 151.3564 seconds (11.9972 KB/sec)\
19/03/10 22:43:36 INFO mapreduce.ImportJobBase: Retrieved 92416 records.\


```
sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training \
--table accounts  --target-dir /loudacre/accounts/CA_1 \
--columns "acct_num, first_name, last_name, state" --fields-terminated-by "\t" \
--where "state = 'CA' "   --z
```
                                                                                                          \
19/03/10 23:10:24 INFO mapreduce.Job: Running job: job_1552272159047_0007                                 \
19/03/10 23:11:10 INFO mapreduce.Job: Job job_1552272159047_0007 running in uber mode : false             \
19/03/10 23:11:11 INFO mapreduce.Job:  map 0% reduce 0%                                                   \
19/03/10 23:11:45 INFO mapreduce.Job:  map 25% reduce 0%                                                  \
19/03/10 23:12:04 INFO mapreduce.Job:  map 50% reduce 0%                                                  \
19/03/10 23:12:27 INFO mapreduce.Job:  map 75% reduce 0%                                                  \
19/03/10 23:12:43 INFO mapreduce.Job:  map 100% reduce 0%                                                 \
19/03/10 23:12:44 INFO mapreduce.Job: Job job_1552272159047_0007 completed successfully                   \
19/03/10 23:12:45 INFO mapreduce.Job: Counters: 30                                                        \
        File System Counters                                                                              \
                FILE: Number of bytes read=0                                                              \
                FILE: Number of bytes written=561628                                                      \
                FILE: Number of read operations=0                                                         \
                FILE: Number of large read operations=0                                                   \
                FILE: Number of write operations=0                                                        \
                HDFS: Number of bytes read=470                                                            \
                HDFS: Number of bytes written=801692                                                      \
                HDFS: Number of read operations=16                                                        \
                HDFS: Number of large read operations=0                                                   \
                HDFS: Number of write operations=8                                                        \
        Job Counters                                                                                      \
                Launched map tasks=4                                                                      \
                Other local map tasks=4                                                                   \
                Total time spent by all maps in occupied slots (ms)=0                                     \
                Total time spent by all reduces in occupied slots (ms)=0                                  \
                Total time spent by all map tasks (ms)=83657                                              \
                Total vcore-seconds taken by all map tasks=83657                                          \
                Total megabyte-seconds taken by all map tasks=21416192                                    \
        Map-Reduce Framework                                                                              \
                Map input records=92416                                                                   \
                Map output records=92416                                                                  \
                Input split bytes=470                                                                     \
                Spilled Records=0                                                                         \
                Failed Shuffles=0                                                                         \
                Merged Map outputs=0                                                                      \
                GC time elapsed (ms)=491                                                                  \
                CPU time spent (ms)=17800                                                                 \
                Physical memory (bytes) snapshot=507895808                                                \
                Virtual memory (bytes) snapshot=8271130624                                                \
                Total committed heap usage (bytes)=251920384                                              \
        File Input Format Counters                                                                        \
                Bytes Read=0                                                                              \
        File Output Format Counters                                                                       \
                Bytes Written=801692                                                                      \
                                                                                                          \

```
sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training \
--table accounts  --target-dir /loudacre/accounts/CA_Gzip \
--columns "acct_num, first_name, last_name, state" --fields-terminated-by "\t" \
--where "state = 'CA' " \
--compression-codec org.apache.hadoop.io.compress.GzipCodec
```
19/03/10 23:13:54 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0\
19/03/10 23:13:54 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using\                                  d.
19/03/10 23:13:55 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.                      \
19/03/10 23:13:55 INFO tool.CodeGenTool: Beginning code generation                                              \
19/03/10 23:13:56 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `accounts` AS t LIMIT 1     \
19/03/10 23:13:56 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `accounts` AS t LIMIT 1     \
19/03/10 23:13:56 INFO orm.CompilationManager: HADOOP_MAPRED_HOME is /usr/lib/hadoop-mapreduce                  \
Note: /tmp/sqoop-training/compile/69d1b694e82cbd7dd1eb752ff7b564f0/accounts.java uses or overrides a deprecated \
Note: Recompile with -Xlint:deprecation for details.                                                            \
19/03/10 23:14:06 INFO orm.CompilationManager: Writing jar file: /tmp/sqoop-training/compile/69d1b694e82cbd7dd1e\                                 4f0/accounts.jar
19/03/10 23:14:06 WARN manager.MySQLManager: It looks like you are importing from mysql.                        \
19/03/10 23:14:06 WARN manager.MySQLManager: This transfer can be faster! Use the --direct                      \
19/03/10 23:14:06 WARN manager.MySQLManager: option to exercise a MySQL-specific fast path.                     \
19/03/10 23:14:06 INFO manager.MySQLManager: Setting zero DATETIME behavior to convertToNull (mysql)            \
19/03/10 23:14:06 INFO mapreduce.ImportJobBase: Beginning import of accounts                                    \
19/03/10 23:14:06 INFO Configuration.deprecation: mapred.job.tracker is deprecated. Instead, use mapreduce.jobtr\                                 ess
19/03/10 23:14:07 INFO Configuration.deprecation: mapred.jar is deprecated. Instead, use mapreduce.job.jar      \
19/03/10 23:14:11 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.map\
19/03/10 23:14:12 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032                           \
19/03/10 23:14:22 INFO db.DBInputFormat: Using read commited transaction isolation                              \
19/03/10 23:14:22 INFO db.DataDrivenDBInputFormat: BoundingValsQuery: SELECT MIN(`acct_num`), MAX(`acct_num`) FR\                                 ts` WHERE ( state = 'CA'  )
19/03/10 23:14:22 INFO db.IntegerSplitter: Split size: 32439; Num splits: 4 from: 1 to: 129760                  \
19/03/10 23:14:22 INFO mapreduce.JobSubmitter: number of splits:4                                               \
19/03/10 23:14:22 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1552272159047_0008                \
19/03/10 23:14:24 INFO impl.YarnClientImpl: Submitted application application_1552272159047_0008                \
19/03/10 23:14:25 INFO mapreduce.Job: The url to track the job: http://localhost:8088/proxy/application_15522721\                                 /
19/03/10 23:14:25 INFO mapreduce.Job: Running job: job_1552272159047_0008                                       \
19/03/10 23:14:57 INFO mapreduce.Job: Job job_1552272159047_0008 running in uber mode : false                   \
19/03/10 23:14:57 INFO mapreduce.Job:  map 0% reduce 0%                                                         \
19/03/10 23:15:24 INFO mapreduce.Job:  map 25% reduce 0%                                                        \
19/03/10 23:15:47 INFO mapreduce.Job:  map 50% reduce 0%                                                        \
19/03/10 23:16:03 INFO mapreduce.Job:  map 75% reduce 0%                                                        \
19/03/10 23:16:25 INFO mapreduce.Job:  map 100% reduce 0%                                                       \
19/03/10 23:16:26 INFO mapreduce.Job: Job job_1552272159047_0008 completed successfully                         \
19/03/10 23:16:27 INFO mapreduce.Job: Counters: 30                                                              \
        File System Counters                                                                                    \
                FILE: Number of bytes read=0                                                                    \
                FILE: Number of bytes written=562344                                                            \
                FILE: Number of read operations=0                                                               \
                FILE: Number of large read operations=0                                                         \
                FILE: Number of write operations=0                                                              \
                HDFS: Number of bytes read=470                                                                  \
                HDFS: Number of bytes written=801692                                                            \
                HDFS: Number of read operations=16                                                              \
                HDFS: Number of large read operations=0                                                         \
                HDFS: Number of write operations=8                                                              \
        Job Counters                                                                                            \
                Launched map tasks=4                                                                            \
                Other local map tasks=4                                                                         \
                Total time spent by all maps in occupied slots (ms)=0                                           \
                Total time spent by all reduces in occupied slots (ms)=0                                        \
                Total time spent by all map tasks (ms)=80133                                                    \
                Total vcore-seconds taken by all map tasks=80133                                                \
                Total megabyte-seconds taken by all map tasks=20514048                                          \
        Map-Reduce Framework                                                                                    \
                Map input records=92416                                                                         \
                Map output records=92416                                                                        \
                Input split bytes=470                                                                           \
                Spilled Records=0                                                                               \
                Failed Shuffles=0                                                                               \
                Merged Map outputs=0                                                                            \
                GC time elapsed (ms)=439                                                                        \
                CPU time spent (ms)=17450                                                                       \
                Physical memory (bytes) snapshot=508981248                                                      \
                Virtual memory (bytes) snapshot=8271118336                                                      \
                Total committed heap usage (bytes)=251920384                                                    \
        File Input Format Counters                                                                              \
                Bytes Read=0                                                                                    \
        File Output Format Counters                                                                             \
                Bytes Written=801692                                                                            \
19/03/10 23:16:27 INFO mapreduce.ImportJobBase: Transferred 782.9023 KB in 135.7907 seconds (5.7655 KB/sec)     \
19/03/10 23:16:27 INFO mapreduce.ImportJobBase: Retrieved 92416 records.
