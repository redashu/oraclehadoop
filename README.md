# Apache spark 

## Distributed IN memory processing superfast framework for Bigdata 

<img hdfsspark.png>

## More info 

<img sparkinfo.png>

## Admin points

## Downoading tar ball from apache spark 

```
wget http://apachemirror.wuchna.com/spark/spark-2.4.7/spark-2.4.7-bin-hadoop2.7.tgz
 tar xzvf spark-2.4.7-bin-hadoop2.7.tgz 
 
 ```
 ## moving spark to opt and do some env var configure 
 
 ```
 [root@ip-172-31-70-87 ~]# cd /opt/spark2/
[root@ip-172-31-70-87 spark2]# ls
LICENSE  R          RELEASE  conf  examples  kubernetes  python  yarn
NOTICE   README.md  bin      data  jars      licenses    sbin
[root@ip-172-31-70-87 spark2]# export  SPARK_HOME=/opt/spark2/
[root@ip-172-31-70-87 spark2]# export PATH=$PATH:$SPARK_HOME:$SPARK_HOME/bin:$SPARK_HOME/sbin

```

## staring spark master

```
[root@ip-172-31-70-87 spark2]# echo $SPARK_HOME
/opt/spark2/
[root@ip-172-31-70-87 spark2]# start-master.sh  
starting org.apache.spark.deploy.master.Master, logging to /opt/spark2//logs/spark-root-org.apache.spark.deploy.master.Master-1-ip-172-31-70-87.ec2.internal.out
[root@ip-172-31-70-87 spark2]# netstat -nlpt
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:8670            0.0.0.0:*               LISTEN      2932/python         
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1116/sshd           
tcp6       0      0 172.31.70.87:7077       :::*                    LISTEN      10872/java          
tcp6       0      0 :::8080                 :::*                    LISTEN      10872/java          
tcp6       0      0 :::22                   :::*                    LISTEN      1116/sshd    

```


