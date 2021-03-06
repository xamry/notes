# Map Reduce
SSH with maria_dev/maria_dev  

## Find Occurances of each rating

    vi RatingsBreakdown.py
    
    from mrjob.job import MRJob
    from mrjob.step import MRStep
    
    class RatingsBreakdown(MRJob):
        def steps(self):
            return [
                MRStep(mapper=self.mapper_get_ratings,
                       reducer=self.reducer_count_ratings)
            ]
    
        def mapper_get_ratings(self, _, line):
            (userID, movieID, rating, timestamp) = line.split('\t')
            yield rating, 1
    
        def reducer_count_ratings(self, key, values):
            yield key, sum(values)
        
    
    if __name__ == '__main__':
        RatingsBreakdown.run()

#### For running command locally  

    python RatingsBreakdown.py u.data  

#### For running command on cluster. (In real env, you would provide hdfs path of u.data instead of local path)  

    python RatingsBreakdown.py -r hadoop --hadoop-streaming-jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar u.data
    
    python TopMovies.py u.data

### Set Admin User and set its password

    SSH with maria_dev/maria_dev  
    su root  (Default root password is hadoop)  
    ambari-admin-password-reset   (will restart ambari)  

# Sqoop

    mysql -u root -p   (password=hortonworks1)  
    create database movielens;  

### To handle international characters in movielens dataset

    set NAMES 'utf8';  
    SET CHARACTER SET utf8;  
    use movielens;  

### Load dataset into mysql

    wget http://media.sundog-soft.com/hadoop/movielens.sql  
    source movielens.sql; 

 
### Find most popular movies

    SELECT movies.title, COUNT(ratings.movie_id) AS ratingCount FROM movies INNER JOIN ratings ON movies.id = ratings.movie_id GROUP BY movies.id ORDER BY ratingCount;  

### Grant all privileges to sqoop to read mysql data

    CREATE USER 'sqoop'@'localhost' IDENTIFIED WITH mysql_native_password by 'p4ssw0rd';  
    GRANT ALL PRIVILEGES ON movielens.* TO 'sqoop'@'localhost';  

### Import directly to HDFS

    sqoop import --connect jdbc:mysql://localhost/movielens --driver com.mysql.jdbc.Driver --table movies --username sqoop -P -m 1 

 

### Import to Hive

    sqoop import --connect jdbc:mysql://localhost/movielens --driver com.mysql.jdbc.Driver --table movies --username sqoop -P -m 1 --hive-import  

### Export from Hive to Mysql

    CREATE TABLE exported_movies(id INTEGER, title VARCHAR(255), releaseDate DATE);  
    sqoop export --connect jdbc:mysql://localhost/movielens --username sqoop -P -m 1 --driver com.mysql.jdbc.Driver --table exported_movies --export-dir /apps/hive/warehouse/movies --input-fields-terminated-by '\0001'  

# HBase
## HBase REST
Setup port forwarding on VM Settings -> Network -> Advanced -> Port forwarding  

    HBase Rest - 127.0.0.1 8000 8000  

Login to Ambari as admin and start hbase  
SSH to VM, login as maria_dev. su root  

    /usr/hdp/current/hbase-master/bin/hbase-daemon.sh start rest -p 8000 --infoport 8001  
    /usr/hdp/current/hbase-master/bin/hbase-daemon.sh stop rest  


## HBase commands

    hbase shell  //takes you to hbase shell (Press Ctrl+C to exit)  
    list  //lists all tables  
    create 'users','userinfo'   //Create table users with column family userinfo  
    scan 'users'  
    disable 'users'  
    drop 'users'  

# Cassandra
## Install Cassandra

    vi /etc/yum.repos.d/datastax.repo  
    
    [datastax]  
    name = DataStax Repo for Apache Cassandra  
    baseurl = http://rpm.datastax.com/community  
    enabled = 1  
    gpgcheck = 0  
    
    su root  
    yum install dsc30  
    
    python --version (should be >=2.7, if not, upgrade)  
    yum install python-pip   (needed for running cqlsh)  
    pip --version  
    
    service cassandra start  
    cqlsh --cqlversion="3.4.0"   (version optional, provide only if you see version mismatch error)  


## Put some data into cassandra

    create KEYSPACE movielens WITH replication  = {'class' : 'SimpleStrategy', 'replication_factor' : '1'} AND durable_writes=true;  
    USE movielens;  
    CREATE TABLE users(user_id int, age int, gender text, occupation text, zip text, PRIMARY KEY(user_id));  
    
    spark-submit --packages datastax:spark-cassandra-connector:2.4.0-s_2.11 CassandraSpark.py  (To be able to use org.apache.spark.sql.cassandra, u need to specify this connector, viz Spark 2 connector for Spark 2)       

## Clean up

    cqlsh>exit
    service cassandra stop

# MongoDB
## Install MongoDB

    su root  
    cd /var/lib/ambari-server/resources/stacks/HDP/2.6/services  
    git clone http://github.com/nikunjness/mongo-ambari.git    (Mongo Ambari connector)  
    sudo service ambari-server restart  
    sudo service ambari-agent restart  

(Login to Ambari as admin and add MongoDB from Action-> Add Service->MongoDB, accept defaults and Deploy)  

    exit   (exit from root account, was only needed for installation)  

## Writing to and reading data from MongoDB using Spark

    pip install pymongo  
    wget http://media.sundog-soft.com/hadoop/MongoSpark.py  
    spark-submit --packages org.mongodb.spark:mongo-spark-connector_2.11:2.3.0 MongoSpark.py  

## Using Mongo Shell

    mongo (takes you to mongo shell)  
    use movielens;  
    db.users.find();  
    db.users.find({user_id:100});  

### Explain plan for the above query

    db.users.explain().find({user_id:100});  

### Create index on user_id for faster queries (Unlike cassandra, mongodb will not create index on your PK by default)

    db.users.createIndex({user_id : 1});  

### Now check again the explain plan to see the fetch is from index

    db.users.explain().find({user_id:100});  


### Find Average age of users for each occupation

    db.users.aggregate([  
    {$group:  {_id : {occupaton : "$occupation"}, avgAge: {$avg : "$age"}  }}  
    ]);  

### Find number of users

    db.users.count();

### See all collections

    db.getCollectionInfos();

### Drop table

    db.users.drop();

### Exit

    exit

#### Do remember to shutdown mongodb in Ambari


# Apache Drill
## Load ratings data in Hive using Hive view

    CREATE DATABASE movielens;  

#### Then Upload rating data (u.data) using Hive View

## Load data into MongoDB
### SSH via admin

    su root  
    spark-submit --packages org.mongodb.spark:mongo-spark-connector_2.11:2.3.0 MongoSpark.py  

## Install drill

    wget http://archive.apache.org/dist/drill/drill-1.12.0/apache-drill-1.12.0.tar.gz  
    tar -zxvf apache-drill-1.12.0.tar.gz  

## Start drill
`bin/drillbit.sh start -Ddrill.exec.http.port=8765`    (Open this port to be used to access this from your host. HDP has this port unused, so we can use this pretty easily. use drill.exec.port if it doesn't work)  

## Access Drill from your web browser

    http://localhost:8765/ 

 

#### Connect drill to MongoDB and Hive (Click Storage menu and enable both. Also make sure ap and dfs are enabled to access Json files on local/hdfs)

#### Update hive.metastore.uris for Hive. (Click Update, change hive.metastore.uris from "" to "thrift://localhost:9083")

#### Explore Drill Query menu, hit few SQL queries. SHOW DATABASES  will show hive.movielens and mongo.movielens)

    select * from mongo.movielens.users limit 10;  
    select * from hive.movielens.ratings limit 10;  

## Find total number of ratings given by users for each occupation

    SELECT u.occupation, COUNT(*) FROM hive.movielens.ratings r JOIN mongo.movielens.users u ON r.user_id = u.user_id  GROUP BY u.occupation;  

## Clean up the mess

    bin/drillbit.sh stop  

(Stop mongoDB from Ambari)  


# Phoenix
## Ensure HBase is started

## Install Phoenix

    su root  
    yum install phoenix  
    cd /usr/hdp/current/phoenix-client/bin  
    python sqlline.py  -- kick off phoenix and launch command line interface  

## List tables

    !tables  

    CREATE TABLE IF NOT EXISTS us_population(  
     state CHAR(2) NOT NULL,  
     city VARCHAR NOT NULL,  
     population BIGINT  
    CONSTRAINT my_pk PRIMARY KEY(state,city)  
    );  
    
    !tables  
    select * from us_population;  

## INSERT won't work in Phoenix, use UPSERT instead

    UPSERT INTO us_population VALUES('NY', 'Ney York', 34241221);  
    UPSERT INTO us_population VALUES('CA', 'Los Angeles', 845452424); 
 

## Clean up the mess

    DROP TABLE us_population;  
    !quit  


## Use pig to load data into HBase using Phoenix

    cd /usr/hdp/current/phoenix-client/bin  
    python sqlline.py  

### First create the users table

    CREATE TABLE users(USERID INTEGER NOT NULL, AGE INTEGER, GENDER CHAR(1), OCCUPATION VARCHAR, ZIP VARCHAR CONSTRAINT pk PRIMARY KEY(USERID));  
    !tables  
    !quit  
     

    cd /home/maria_dev  
    wget http://media.sundog-soft.com/hadoop/phoenix.pig  
    pig phoenix.pig  

## Clean up the mess

    cd /usr/hdp/current/phoenix-client/bin  
    python sqlline.py  
    SELECT * from USERS LIMIT 10;  
    DROP TABLE users;  
    !quit  

### Shut down HBase

# Presto
## Install Presto

    su root  
    Goto prestodb.io, find the link to tarball under Docs -> Deploying Presto  
    wget https://repo1.maven.org/maven2/com/facebook/presto/presto-server/0.240/presto-server-0.240.tar.gz  
    tar -zxvf presto-server-0.240.tar.gz  
    cd presto-server-0.240  

##### Create an etc directory and put configuration into it as described at https://prestodb.io/docs/current/installation/deployment.html
##### OR download one from sundog-soft for demo purpose

    wget http://media.sundog-soft.com/hadoop/presto-hdp-config.tgz  
    tar -zxvf presto-hdp-config.tgz  

## Install Presto CLI

    Goto https://prestodb.io/docs/current/installation/cli.html and copy the path of presto-cli  
    cd bin  
    wget https://repo1.maven.org/maven2/com/facebook/presto/presto-cli/0.240/presto-cli-0.240-executable.jar

  
### Rename it to a convenient name and make it executable

    mv presto-cli-0.240-executable.jar presto  
    chmod +x presto  

## Start Presto

    bin/launcher start  

## Open Presto dashboard

    http://localhost:8090/ 

 

## Open CLI (Make sure ratings table is already there in hive)

    bin/presto --server localhost:8090 --catalog hive  

## Browse data on presto CLI

    show tables from movielens;  
    select * from movielens.ratings limit 10;  

### Observe the queries ran on browser console by unchecking Finished

## Exit Presto CLI and stop presto

    quit  
    bin/launcher stop  

## Use presto to Query both Cassandra and Hive at once
### Start cassandra

    service cassandra start 

 

### Enable thrift on cassandra (in order for presto to talk to cassandra)

    nodetool enablethrift  

### Check the users table in cassandra

    cqlsh  
    describe keyspaces;  
    use movielens;  
    select * from users limit 10;  
    quit  

### Goto presto and configure cassandra catalog

    cd presto-server-0.240/etc/catalog  
    vi cassandra.properties  
    connector.name=cassandra  
    cassandra.contact-points=127.0.0.1  

## Start Presto

    cd ../..  
    bin/launcher start  

## Goto Presto CLI

    bin/presto --server localhost:8090 --catalog hive,cassandra  

## Check cassandra and hive tables

    show tables from cassandra.movielens;  
    show tables from hive.movielens;  
    describe cassandra.movielens.users;  
    describe hive.movielens.ratings;  
    
    select * from cassandra.movielens.users limit 10;  
    select * from hive.movielens.ratings limit 10;  

## Count ratings given by users in each occupation

    select u.occupation, count(*) from hive.movielens.ratings r join cassandra.movielens.users u on r.user_id = u.user_id group by u.occupation;  

## Clean up the mess

    quit  
    bin/launcher stop --Stop presto  
    service cassandra stop  

# Compare MapReduce and Tez Perormance
## Run below query on Hive view

    DROP VIEW IF EXISTS topMovieIDs;  
    
    CREATE VIEW topMovieIDs AS  
    SELECT movie_id, count(movie_id) as ratingCount  
    FROM movielens.ratings  
    GROUP BY movie_id  
    ORDER BY ratingCount DESC;  
    
    SELECT n.name, ratingCount  
    FROM topMovieIDs t JOIN movielens.names n on t.movie_id = n.movie_id;  

#### Click gear icon and set hive.execution.engine to either mr or tez before executing the query. Compare the time using a stop watch


# Zookeeper

    su root  
    cd /usr/hdp/current/zookeeper-client/bin  

## Use ZK CLI to connect to ZK server (which starts automatically with sandbox)

    ./zkCli.sh 

 

## See what's at root level

    ls /  

## Create an ephemeral znode named testmaster with some data (ephemeral and persistent and two types of znodes)

    create -e /testmaster "127.0.0.1:2223" 

 

## Trying to create the same znode again will throw an error since it's locked.

## Inspect/get a znode

    get /testmaster  
    
    ##Quit, this will delete the testmaster since it was ephemeral, and the client (ZK-CLI) that created it has died
    quit  
    
    ##Now another client can create the znode /testmaster since there is no lock on it.


# Oozie
### Install extjs on sandbox. Oozie won't work without this.

    su root  
    wget http://public-repo-1.hortonworks.com/HDP-UTILS-GPL-1.1.0.22/repos/centos6/extjs/extjs-2.2-1.noarch.rpm  
    rpm -ivh extjs-2.2-1.noarch.rpm  

### Now restart oozie in Ambari, you'e done.

### Creating an oozie workflow
#### Create workflow.xml and put in your HDFS folder.
#### Create job.properties for any configuration your workflow might want to read

### Run oozie job

    oozie job --oozie http://localhost:11000/oozie --config /home/maria_dev/job.properties -run  

### Monitor progress at localhost:10000/oozie
### Oozie coordinators schedules the Oozie workflow execution
### Oozie bundle is collection of coordinatiors that can be managed together

## Oozie Labs
### Sqoop data from mysql and analyze into Hive

#### Setup Mysql and scoop as per sqoop section

### Get hive script

    wget http://media.sundog-soft.com/hadoop/oldmovies.sql  

### Get workflow.xml

    wget http://media.sundog-soft.com/hadoop/workflow.xml   (remember to edit sqoop command by adding --username sqoop)  

### Get job.properties

    wget http://media.sundog-soft.com/hadoop/job.properties  

### Upload workflow.xml into HDFS

    hadoop fs -put workflow.xml /user/maria_dev 

 

### Upload hive script at required place

    hadoop fs -put oldmovies.sql /user/maria_dev  

### Install sqoop mysql connector (not installed in HDP by default)

    hadoop fs -put /usr/share/java/mysql-connector-java.jar /user/oozie/share/lib/lib_20180618160835/sqoop  

### Restart oozie beause configuration has changed
#### Restart from Ambari

### Execute the oozie workflow

    oozie job -oozie http://localhost:11000/oozie -config /home/maria_dev/job.properties -run  

### Observe oozie web console and see the output under /user/maria_dev/oldmovies using Ambari Files View

### To kill a running oozie job

    oozie job -oozie http://localhost:11000/oozie -kill 0000000-200915155855519-oozie-oozi-W  


# Zeppelin
- Open Zeppelin at localhost:9995  
- Create new note (give it a name)  
- Set default interpreter (1st) to spark. md should be next (2nd) - by clicking on gear icon  

### Write some markdown paragraph text and press shift+enter

    %md 

 

### Let's make sure Spark 2 is working first!

Let's see what version we're working with.  

### Print Spark version

    sc.version 

 

### Download dataset to /tmp using shell interpreter

    %sh  
    wget http://media.sundog-soft.com/hadoop/ml-100k/u.data -O /tmp/u.data   
    wget http://media.sundog-soft.com/hadoop/ml-100k/u.item -O /tmp/u.item  
    echo "Dataset downloaded!"  

### Copy the dataset into HDFS

    %sh  
    hadoop fs -rm -r -f /tmp/ml-100k/  
    hadoop fs -mkdir /tmp/ml-100k/  
    hadoop fs -put /tmp/u.data /tmp/ml-100k/  
    hadoop fs -put /tmp/u.item /tmp/ml-100k/  
    echo "Dataset loaded into HDFS."  

### List the dataset from HDFS

    %sh  

    hadoop fs -ls /tmp/ml-100k/  

### Analyze data using scala code

    final case class Rating(movieID: Int, rating: Int)  
    val lines = sc.textFile("hdfs:///tmp/ml-100k/u.data").map(x => {val fields = x.split("\t"); Rating(fields(1).toInt, fields(2).toInt)})  

### Convert RDD to Data Frame (DF)

    import sqlContext.implicits._  
    val ratingsDF = lines.toDF()  

### Print top movies

    val topMovieIDs = ratingsDF.groupBy("movieID").count().orderBy(desc("count")).cache()  
    topMovieIDs.show()  

### Use SparkSQL to perform queries on DF
#### Create SparkSQL table from DF

    ratingsDF.registerTempTable("ratings")  

### Run SparkSQL query

    %sql  
    SELECT * FROM ratings LIMIT 10  

### Find how many have rated each ratings

    SELECT rating, COUNT(*) as count FROM ratings GROUP BY rating  

### Create DF for Movie titles

    final case class Movie(movieID: Int, title: String)  
    val lines = sc.textFile("hdfs:///tmp/ml-100k/u.item").map(x => {val fields = x.split('|'); Movie(fields(0).toInt, fields(1))})  
    import sqlContext.implicits._  
    val moviesDF = lines.toDF()  
    moviesDF.show()  

### Create SparkSQL table from DF

    moviesDF.registerTempTable("titles")  

### Run Join query (Find popular movie titles)

    %sql  
    SELECT t.title, count(*) cnt FROM ratings r JOIN titles t ON r.movieID = t.movieID GROUP BY t.title ORDER BY cnt DESC LIMIT 20  

# Hue (Hadoop User Experience)
### gethue.com -> Try Hue now -> un/pw: demo/demo

# Kafka
Kafka is a general purpose publish/ subscribe messaging system.

## Setup and publish some data
Kafka comes preinstalled with HDP.

 - Log in to Ambari with admin user, click on Kafka and start it (if not
   already started) 
 - SSH to Sandbox with Maria_dev/maria_dev
 
### Navigate to Kafka directory

    cd /usr/hdp/current/kafka-broker
    ls
    cd bin
    ls

### Create a topic
(Kafka needs zookeeper to keep track of it)

    ./kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic my-topic

### List all topics created on this instance

    ./kafka-topics.sh --list --zookeeper localhost:2181

### Produce some data into this topic
//Open Kafka port is 6667. The shell script is a command line producer that listens to lines of input from standard input 

     ./kafka-console-producer.sh --broker-list sandbox-hdp.hortonworks.com:6667 --topic my-topic
    This is a line of data
    I am sending this to topic my-topic

### Consume the data from topic

    cd /usr/hdp/current/kafka-broker/bin/
    //In absence of from-beginning, only new messages would be consumed
    ./kafka-console-consumer.sh --bootstrap-server sandbox-hdp.hortonworks.com:6667 --topic my-topic --from-beginning
    //Try producing and consuming messages from both producer and consumer windows, and close them (Ctrl+C) when you're done.

## Publish weblogs with Kafka
We'll use in-built File Connector that comes with Kafka

### Configure

    cd /usr/hdp/current/kafka-broker/conf
    ls
#### Create backup first

    cp connect-standalone.properties ~/
    cp connect-file-sink.properties ~/
    cp connect-file-source.properties ~/
    
#### Modify config files    

	    cd ~   
	    
        vi connect-standalone.properties
        bootstrap-servers=sandbox-hdp.hortonworks.com:6667
    	
    	vi connect-file-sink.properties
    	file=/home/maria_dev/logout.txt
    	topics=log-test
    	
    	vi connect-file-source.properties
    	file=/home/maria_dev/access_log_small.txt
    	topic=log-test
	
### Download access log file
	cd ~
    wget http://media.sundog-soft.com/hadoop/access_log_small.txt

### Start a consumer to print the messages
(In a new window)

    cd /usr/hdp/current/kafka-broker/bin/   
    ./kafka-console-consumer.sh --bootstrap-server sandbox-hdp.hortonworks.com:6667 --topic log-test --from-beginning
    
### Listen to changes in weblog and publish
(In a new window)

     cd /usr/hdp/current/kafka-broker/bin/
     ./connect-standalone.sh ~/connect-standalone.properties ~/connect-file-source.properties ~/connect-file-sink.properties
(Observe the ~/logout.txt)

### Check changes in real time
(Open a new window)

    cd ~
    echo "This is a new line" >> access_log_small.txt

(Observe the consumer window and logout.txt)

### Cleanup the mess
Close all windows, shutdown kafka from Ambari

# Flume
(For streaming data into cluster, just like Kafka. Originally made to handle log aggregation. Made from start with Hadoop in mind. Built in sinks for HDFS and HBase.)
## Flume Agent
Components of Flume Agent:
 - Source   (Where data is coming from, can optionally have channel selectors and interceptors)
 - Channel   (How the data is transferred (via memory or files)
 - Sink (where data is going, can be organized into sink groups, A sink can be connected to only one channel. Channel is notified to delete the message once sink processes it.)

Example:  Web servers => Source => Channel => Sink => HBase

### Built in Source types
Spooling directory, Avro, Kafka, Exec, Thrift, Netcat, HTTP, Custom, and more!
### Built in Sink types
HDFS, Hive, HBase, Avro, Thrift, Elasticsearch, Kafka, Custom, and more!

Using Avro, Agents can connect to other Agents as well. Avro acts as Glue that can bind different Flume agents together.
Flume acts as a buffer between your data and your cluster.

## Set up Flume
Source (netcat) => Channel (Memory) => Sink (logger)
SSH to sandbox with maria_dev user

    cd ~
    vi example.conf
    # example.conf: A single-node Flume configuration
        
    # Name the components on this agent (Agent 1 or a1. r1, k1, c1 are source1, sink1 and channel1 respectively.)
    a1.sources = r1
    a1.sinks = k1
    a1.channels = c1
    
    # Describe/configure the source
    a1.sources.r1.type = netcat
    a1.sources.r1.bind = localhost
    a1.sources.r1.port = 44444
    
    # Describe the sink
    a1.sinks.k1.type = logger
    
    # Use a channel which buffers events in memory
    a1.channels.c1.type = memory
    a1.channels.c1.capacity = 1000
    a1.channels.c1.transactionCapacity = 100
    
    # Bind the source and sink to the channel
    a1.sources.r1.channels = c1
    a1.sinks.k1.channel = c1
    
## Start Flume Agent

	sudo su
    cd /usr/hdp/current/flume-server
    bin/flume-ng agent --conf conf --conf-file /home/maria_dev/example.conf --name a1 -Dflume.root.logger=INFO,console

## Test the Flume agent
Send a message from source and observe it getting printed into Flume logs.
netcat is a unix utility that monitors the network traffic.
See the content in /var/log/flume/flume.log if it's not available on console for some reason.

    sudo yum install telnet
    telnet localhost 44444
    Hello, How are you doing today!  

Ctrl+] to get out of telnet, Ctrl+C to stop the flume agent.

## Monitor a directory and store its data in HDFS
We'll use create a Flume flow to accomplish this real world task.

### Create Flume Conf

    cd ~
    mkdir spool
    vi flumelogs.conf
    # flumelogs.conf: A single-node Flume configuration
    
    # Name the components on this agent
    a1.sources = r1
    a1.sinks = k1
    a1.channels = c1
    
    # Describe/configure the source
    a1.sources.r1.type = spooldir
    a1.sources.r1.spoolDir = /home/maria_dev/spool
    a1.sources.r1.fileHeader = true
    a1.sources.r1.interceptors = timestampInterceptor
    a1.sources.r1.interceptors.timestampInterceptor.type = timestamp
    
    # Describe the sink
    a1.sinks.k1.type = hdfs
    a1.sinks.k1.hdfs.path = /user/maria_dev/flume/%y-%m-%d/%H%M/%S
    a1.sinks.k1.hdfs.filePrefix = events-
    a1.sinks.k1.hdfs.round = true
    a1.sinks.k1.hdfs.roundValue = 10
    a1.sinks.k1.hdfs.roundUnit = minute
    
    # Use a channel which buffers events in memory
    a1.channels.c1.type = memory
    a1.channels.c1.capacity = 1000
    a1.channels.c1.transactionCapacity = 100
    
    # Bind the source and sink to the channel
    a1.sources.r1.channels = c1
    a1.sinks.k1.channel = c1
    
Create a folder flume in /user/maria_dev manually

### Start Flume agent
	sudo su
    cd /usr/hdp/current/flume-server
    bin/flume-ng agent --conf conf --conf-file /home/maria_dev/flumelogs.conf --name a1 -Dflume.root.logger=INFO,console

### Test the Flume flow
Copy some log file into spool directory

    cd /home/maria_dev
    sudo cp access_log_small.txt spool/amresh.txt

Notice that it's picked by Flume, the amresh.txt converted to amresh.txt.COMPLETED, and new files created in /user/maria_dev/flume

<!--stackedit_data:
eyJoaXN0b3J5IjpbNDg5NDQzMjYzLC02MjEwMjQ4MjcsMTI2Mz
g1MzY0MywxMzg3NzA5MDgxLDk3MDI1NDI3MiwxNjI5NjA5OTAy
LC0xODkxMzU4NDE4LDM0MTk1Mjc3Niw2Mzk4MjM4NjIsLTgwMz
Q1NzMxNSwzMDY4OTQ5MTIsLTEyMjAxOTkzMzMsLTE4MjM3OTMz
NDUsMTk0MDM4MjE4OCwxNTk0ODk1MDYsMTk1MDE0ODI3NywtMj
AyOTU0MzU2NywtNzQ0MTYxODQyLC0zOTQ0NzkwMjYsLTIwMTI1
MTUwNjJdfQ==
-->