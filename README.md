# Distributed processing using Yarn / MR2

##  all default jar files location 

```
[hdfs@ashumaster ~]$ cd /usr/hdp/
[hdfs@ashumaster hdp]$ ls
2.6.5.1175-1  current  share
[hdfs@ashumaster hdp]$ cd  2.6.5.1175-1/
[hdfs@ashumaster 2.6.5.1175-1]$ ls
etc  hadoop  hadoop-hdfs  hadoop-mapreduce  hadoop-yarn  ranger-hdfs-plugin  ranger-yarn-plugin  spark  spark2  usr  zookeeper
[hdfs@ashumaster 2.6.5.1175-1]$ cd  hadoop-mapreduce/
[hdfs@ashumaster hadoop-mapreduce]$ ls
activation-1.1.jar                      hadoop-auth.jar                                                 jackson-core-asl-1.9.13.jar
apacheds-i18n-2.0.0-M15.jar             hadoop-datajoin-2.7.3.2.6.5.1175-1.jar                          jackson-jaxrs-1.9.13.jar
apacheds-kerberos-codec-2.0.0-M15.jar   hadoop-datajoin.jar                                             jackson-mapper-asl-1.9.13.jar
api-asn1-api-1.0.0-M20.jar              hadoop-distcp-2.7.3.2.6.5.1175-1.jar                            jackson-xc-1.9.13.jar
api-util-1.0.0-M20.jar                  hadoop-distcp.jar                                               java-xmlbuilder-0.4.jar
asm-3.2.jar                             hadoop-extras-2.7.3.2.6.5.1175-1.jar                            jaxb-api-2.2.2.jar
avro-1.7.4.jar                          hadoop-extras.jar                                               jaxb-impl-2.2.3-1.jar
azure-keyvault-core-0.8.0.jar           hadoop-gridmix-2.7.3.2.6.5.1175-1.jar                           jcip-annotations-1.0-1.jar
bin                                     hadoop-gridmix.jar                                              jersey-core-1.9.jar
commons-beanutils-1.7.0.jar             hadoop-mapreduce-client-app-2.7.3.2.6.5


```

## Now time for Execute  a simple MR job using yarn 

### Checking currently active NodeManager

```
[hdfs@ashumaster hadoop-mapreduce]$ yarn node  -list 
20/09/15 06:00:36 INFO client.RMProxy: Connecting to ResourceManager at ashumaster.hadoop.com/172.31.79.79:8050
20/09/15 06:00:36 INFO client.AHSProxy: Connecting to Application History server at ashumaster.hadoop.com/172.31.79.79:10200
Total Nodes:10
         Node-Id	     Node-State	Node-Http-Address	Number-of-Running-Containers
rajkumardatanode.hadoop.com:45454	        RUNNING	rajkumardatanode.hadoop.com:8042	                           0
dineshdatanode.hadoop.com:45454	        RUNNING	dineshdatanode.hadoop.com:8042	                           0
girishdatanode.hadoop.com:45454	        RUNNING	girishdatanode.hadoop.com:8042	                           0
deepakdatanode.hadoop.com:45454	        RUNNING	deepakdatanode.hadoop.com:8042	                           0
banudatanode.hadoop.com:45454	        RUNNING	banudatanode.hadoop.com:8042	                           0
ashisdatanode.hadoop.com:45454	        RUNNING	ashisdatanode.hadoop.com:8042	                           0
rohitkdatanode.hadoop.com:45454	        RUNNING	rohitkdatanode.hadoop.com:8042	                           0
diptidatanode.hadoop.com:45454	        RUNNING	diptidatanode.hadoop.com:8042	                           0
srinidatanode.hadoop.com:45454	        RUNNING	srinidatanode.hadoop.com:8042	                           0
durgadatanode.hadoop.com:45454	        RUNNING	durgadatanode.hadoop.com:8042	                           0

```


### checking existing options in example jar

```
[hdfs@ashumaster hadoop-mapreduce]$ yarn jar  hadoop-mapreduce-examples-2.7.3.2.6.5.1175-1.jar 
An example program must be given as the first argument.
Valid program names are:
  aggregatewordcount: An Aggregate based map/reduce program that counts the words in the input files.
  aggregatewordhist: An Aggregate based map/reduce program that computes the histogram of the words in the input files.
  bbp: A map/reduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.
  dbcount: An example job that count the pageview counts from a database.
  distbbp: A map/reduce program that uses a BBP-type formula to compute exact bits of Pi.
  grep: A map/reduce program that counts the matches of a regex in the input.
  join: A job that effects a join over sorted, equally partitioned datasets
  multifilewc: A job that counts words from several files.
  pentomino: A map/reduce tile laying program to find solutions to pentomino problems.
  pi: A map/reduce program that estimates Pi using a quasi-Monte Carlo method.
  randomtextwriter: A map/reduce program that writes 10GB of random textual data per node.
  randomwriter: A map/reduce program that writes 10GB of random data per node.
  secondarysort: An example defining a secondary sort to the reduce.
  sort: A map/reduce program that sorts the data written by the random writer.
  sudoku: A sudoku solver.
  teragen: Generate data for the terasort
  terasort: Run the terasort
  teravalidate: Checking results of terasort
  wordcount: A map/reduce program that counts the words in the input files.
  wordmean: A map/reduce program that counts the average length of the words in the 
  
  ```
  
  ## Now using wordcount 
  
  ```
  [hdfs@ashumaster hadoop-mapreduce]$ yarn jar  hadoop-mapreduce-examples-2.7.3.2.6.5.1175-1.jar  wordcount  /ashutoshhdata/ashudata.txt   /ashuoutput 
20/09/15 06:06:20 INFO client.RMProxy: Connecting to ResourceManager at ashumaster.hadoop.com/172.31.79.79:8050
20/09/15 06:06:20 INFO client.AHSProxy: Connecting to Application History server at ashumaster.hadoop.com/172.31.79.79:10200
20/09/15 06:06:21 INFO input.FileInputFormat: Total input paths to process : 1
20/09/15 06:06:21 INFO mapreduce.JobSubmitter: number of splits:7
20/09/15 06:06:21 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1600161959082_0011
20/09/15 06:06:21 INFO impl.YarnClientImpl: Submitted application application_1600161959082_0011
20/09/15 06:06:21 INFO mapreduce.Job: The url to track the job: http://ashumaster.hadoop.com:8088/proxy/application_1600161959082_0011/
20/09/15 06:06:21 INFO mapreduce.Job: Running job: job_1600161959082_0011
20/09/15 06:06:34 INFO mapreduce.Job: Job job_1600161959082_0011 running in uber mode : false
20/09/15 06:06:34 INFO mapreduce.Job:  map 0% reduce 0%
20/09/15 06:06:49 INFO mapreduce.Job:  map 4% reduce 0%

```

## check processing 

```
hdfs@ashumaster hadoop-mapreduce]$ hdfs dfs  -cat  /ashuoutput/part-r-00000
hello	34684758
is	34684757
me	34684757
this	34684757
wo	1
world	34684757
[hdfs@ashumaster hadoop-mapreduce]$ 

```

