
hbase setup in local environment:
-------------------------------------
Download the hbase tar from hbase site as below 
Example: hbase-2.0.2-bin.tar.gz 

1.In hbase-cmd.config (C:\Hadoop\hadoop_binary\hbase\bin\), set java_home as below  set JAVA_HOME="C:\Program Files (x86)\Java\jre1.8"

2.In hbase-site.xml (C:\Hadoop\hadoop_binary\hbase\conf\), set the below properties in configuration.
<configuration>
	<property>
		<name>hbase.rootdir</name>
		<value>C:\Hadoop\hadoop_binary\HBase\HFiles</value>
	</property>
	<property>
		<name>hbase.zookeeper.property.dataDir</name>
		<value>C:\Hadoop\hadoop_binary\zookeeper</value>
	</property>
	<property>
		<name>hbase.cluster.distributed</name>
		<value>false</value>
	</property>
</configuration>

3.Now, start habse service using below command
C:\Hadoop\hadoop_binary\hbase\bin\start-hbase.cmd

(If any errors, verify them and resolve)
Note: Make sure you place all files in 'C' drive else will get permission related issues like region server start 

4. Once hbase -service up and running run hbase shell commnads to verify as below,
  > hbase shell
  > create 'table1',cf1'
  > put 'table1','emp01','cf:fn','First Name'  
  > scan 'table1'



steps to configure Phoenix in local machine (windows 10)
-----------------------------------------------------------
Prerequisites:
- Java_home path as well as jdk setup were set properly in environment variables
  java_home:- C:\Program Files (x86)\Java\jre1.8.0_231\bin 
  jdk_path:- C:\ProgramData\redhat\java-1.8.0-openjdk-1.8.0.201-2.b09.redhat.windows.x86_64\bin\java)
- If you have spaces in path variable (It will through un related errors) hence try to avoid spaces in the path variable
- Download the phoenix jar files for windows10 
  apache-phoenix-5.0.0-HBase-2.0-bin.tar

1. phoenix setup: copy the two jars(phoenix-4.15.0-HBase-1.4-server,phoenix-core-4.15.0-HBase-1.4) to hbase lib and start the phoenix as below 
C:\Hadoop\hadoop_binary\apache-phoenix-5.0.0-HBase-2.0-bin>
python sqlline.py
Note: Remove the ' $PHOENIX_OPTS ' from both files sqlline.py & sqlline-thin.py

verify whether phoenix working as expected by running few commands: 
- !tables
- CREATE TABLE IF NOT EXISTS table1 (
    time1 TIME, name1 VARCHAR, id1 INTEGER, id2 INTEGER, Status VARCHAR
    CONSTRAINT pk PRIMARY KEY (time1) )
- UPSERT INTO ob_reporting VALUES ('2019-06-23 00:00:00','Customer',1111,1111,'202');
- select * from ob_reporting;	

2.start query server using below command to connect via program using JDBC server
C:\Hadoop\hadoop_binary\apache-phoenix-5.0.0-HBase-2.0-bin>
python queryserver.py

3.Connect to query server using phoenix thin client 
C:\Hadoop\hadoop_binary\apache-phoenix-5.0.0-HBase-2.0-bin\bin>
python sqlline-thin.py http://localhost:8765 

- execute queries and verify 
- select * from ob_reporting;
