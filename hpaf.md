## :elephant: Hadoop Platform and Application Framework :elephant:

### Big Data Hadoop Stack

- **Hadoop Stack Basics**
  - Hadoop moves computation to data
  - Hadoop provides reliability because HARDWARE FAILS!!!
  - We can keep all the data that we have, and we can take that data and analyze it in new interesting ways

- **The Apache Framework: Basic Modules**
  - There's 4 basic components in the Apache Framework:
    - Hadoop Common;
    - Hadoop Distributed File System (HDFS);
    - Hadoop MapReduce;
    - Hadoop Yarn;

  - Hadoop Common - contains libraries and utilities needed by other Hadoop modules.

  - HDFS - Hadoop Distributed File System is a distributed file system that stores data on a commodity machine. Providing very high aggregate bandwidth across the entire cluster.

  - Hadoop MapReduce - is a programming model that scales data across a lot of different processes.

  - Hadoop Yarn - is a resource management platform responsible for managing compute resources in the cluster and using them in order to schedule users and applications.

  <p align="center"><img src="images/HadoopEcoSystem.png" width="500px"></p>

- **HDFS - Hadoop Distributed File System**

  - It is a distributed, scalable, and portable file system written in Java in order to support the Hadoop framework.

  - Each node in Hadoop instance typically has a single name node, and a cluster of data nodes that formed this HDFS cluster.

<p align="center"><img src="images/datanodes-overview.png" width="500px"></p>

  - Hadoop can achieve reliability by replicating the cross multiple hosts, and therefore does not require any range storage on hosts.

  - The HDFS file system encodes the so-called secondary NameNode.

  - The secondary NameNode regularly connects to the primary NameNode and builds snapshots of the primary's NameNodes, the rapture information, and remembers which system saves to the local and the remote directories.

  - About every one of the Hadoop based system sits some version of a MapReduce engine.

  - The typical MapReduce engine will consist of a job tracker, to which client applications can submit MapReduce jobs, and this job tracker typically pushes work out to all the available task trackers, now it's in the cluster.

  - YARN was born as a need to enable a broader array of interaction patterns for data stored in HDFS beyond the MapReduce kind of framework.

  - Yarn enhances the power of the Hadoop compute cluster, without being limited by the map produce kind of framework.

  - The processing power and data centers continue to grow quickly, because the YARN research manager focuses exclusively on scheduling. He can manage those very large clusters quite quickly and easily.

  - *YARN == MapReduce 2.0*

  <p align="center"><img src="images/hds-Architecture.jpg" width="500px"></p>

- **The Hadoop Zoo**

  - *How do we scale and distribute and process very large amounts of data?*

  - Linkedin's Hadoop Stack Diagram

  <p align="center"><img src="images/Linkedin.png" width="500px"></p>

  - Cloudera's Hadoop Stack Diagram

  <p align="center"><img src="images/hadoop41.jpg" width="500px"></p>

- **Hadoop Ecosystem Major Components**

  - **Apache Sqoop** - A tool for transforming "SQL to Hadoop". Tool designed for efficiently transferring bulk data between Apache Hadoop and structured datastores such as relational databases.

  - **HBase** - It's a key component of the Hadoop Stack. It's a tool to provide really fast random access to significant data set. It can handle massive data tables combining billions and billions of rows and columns. It's a scalable data warehouse with support for large tables.

  - **Pig** - It's a scripting language, it's really a high level platform for creating MapReduce programs using Hadoop. The language is called Pig Latin. You can execute pig scripts in other languages. It's a high level data-flow language and execution framework for parallel computation.

  - **Apache Hive** - Data Warehouse software facilitates querying and managing large datasets residing in distributed file storage. It actually provides a mechanism to project structure on top of all of this data and allow us to use SQL like queries to access the data that we have stored in this data warehouse. This query language is called HiveQL.

  - **Oozie** - Workflow schedule system to manage Apache Hadoop Jobs.

  - **Zookeper** - A patch Zookeper provides operational services for the Hadoop Cluster.

  - **Flume** - Distributed, reliable and available service for efficiently collecting, aggregating and moving large amounts of log data. Flume is a scalable real-time ingest framework tha allows you to route, filter, aggregate, and do "mini-operations" on data on its way in to the scalable processing platform. Flume is the most common way to ingest web clickstream.

  - *Bonus* - **Spark** - Apache Spark is a fast and general engine for large-scale data processing. It's a fast and general compute engine for Hadoop data. Wide range of applications - ETL, Machine Learning, Stream Processing and graphic analytics.

#

- **[Tutorial] Running Hadoop Jobs**

  - Using Sqoop to export data from relational databases (in SQL format) into the HDFS (in Avro format). Launching the scoop job:

  `$ sqoop import-all-tables \ -m 1 \`

  - Command to confirm that your Avro data files exist in HDFS:

  `$ hadoop fs -ls /user/hive/warehouse`

  - Command to show a folder for each of the tables:

  `$ hadoop fs -ls /user/hive/warehouse/categories/`

  - Command to show the schema files created by Sqoop in your home directory:

  `$ ls -l *.avsc`

  - Apache Hive will need the schema files too, these are the commands to copy them into HDFS, where Hive can easily access them:

  ```     
     $ sudo -u hdfs hadoop fs -mkdir /user/examples
     $ sudo -u hdfs hadoop fs -chmod +rw /user/examples
     $ hadoop fs -copyFromLocal ~/*.avsc /user/examples
  ```

  - The next step is query structured data. We need to use Hue's Impala app to create the metadata for our tables in Hue, and then query then. We can access Hue in port 8888 of your Master Node (Ex: 10.2.5.15:8888).

  - Once we are inside Hue, we must click on Query Editors, and open the Impala Query Editor.

  - After we create and execute our queries, we can see all the tables created executing this query: `show tables;`.

  - The next step is create and execute structured queries in Impala.

  <p align="center"><img src="images/impalastructured.png" width="500px"></p>

  - Now we're gonna correlate structured data with instructured data.

  - Let's move this data from the localsystem, into HDFS, executing the following commands from your Master Node:

  ```
     $ sudo -u hdfs hadoop fs -mkdir /user/hive/warehouse/original_access_logs`
     $ sudo -u hdfs hadoop fs -copyFromLocal /opt/examples/log_files/access.log.2 /user/hive/warehouse/original_access_logs
  ```

  - Verify that your data is in HDFS with the following command:

  `$ hadoop fs -ls /user/hive/warehouse/original_access_logs`

  - Now we can build a table in Hive and query data via Impala and Hue. We'll build this table in 2 steps.

    - 1. We'll query Hive using a command-line JDBC client for Hive called Beeline. We can invoke ir from the terminal with the following command:

    `$ beeline -u jdbc:hive2://quickstart:10000/default -n admin -d org.apache.hive.jdbc.HiveDriver`

    - 2. Once the Beeline shell is connected, run the queries.

    - 3. You can see the newly created tables in Hue/Impala

#

### Overview of the Hadoop Stack

- Hadoop Stack Transition

<p align="center"><img src="images/hadoopstacktransition.png" width="500px"></p>

- Hadoop Stack

<p align="center"><img src="images/stack.png" width="500px"></p>

#

- **HDFS and HDFS2**

  - **Original HDFS Design Goals**

    - Resilience to hardware failure

    - Streaming data access

    - Support for large dataset, scalability to hundreds/thousands of nodes with high aggragate bandwidht

    - Application locality to data

    - Portability across heterogeneous hardware anda software platforms

  - **Original HDFS Design**

    - _Single Namenode:_ a master server that manages the file system namespace and regulates access to files by clients.

    - _Multiple Datanodes:_ tipically one per node in the cluster. Functions:

      - Manage storage

      - Serving read/write requests from client

      - Block creation, deletion, replication based on instructions from NameNode.

  <p align="center"><img src="images/hdfsdesign.png" width="500px"></p>

#

  - **HDFS in Hadoop 2**

    - HDFS Federation

    - Multiple Namenode Servers

    - Multiple Namespaces

    - High Availability - redundant NameNodes

    - heterogeneous Storage and Archival Storage

      - ARCHIVE, DISK, SSD, RAM_DISK

  - **Benefits of Federation**

    - Allows namespace scalling

    - Scales up filesystem read/write throughput

    - Isolation

#

- Federation

  <p align="center"><img src="images/federation.png" width="500px"></p>

- Federation Block Pools

  <p align="center"><img src="images/federationblockpools.png" width="500px"></p>

- Federation brings performance improvements. Since you have multiple namespaces and namenodes, you can isolate essentially particular applications. If something is very intensive in metadata operations, it´s not going to impact everything else on the system.

- In Federation we have multiple namenode servers. We also have multiple namespaces, and the data is stored in block pools. So there is a pool associated with each namenode or namespace. And these pools are essentially spread out over all the data nodes.  

#

- **MapReduce Framework and Yarn**

  - Software Framework - *for writing parallel data processing applications*

  - MapReduce job split data into chunks.

  - Map tasks process data chunks.

  - Framework sorts map output.

  - Reduce tasks use sorted map data as input.

  - Typically compute and storage nodes are the same.

  - MapReduce tasks and HDFS running on the same nodes.

  - Map tasks and HDFS daemons are part of the data nodes.

  - Can schedule tasks on nodes with data already present.

- **Original MapReduce Framework**

  - Single master JobTracker.

  - JobTracker schedules, monitors, and re-executes failed tasks.

  - One slave TaskTracker per cluster node.

  - TaskTracker executes tasks per JobTracker requests.

#

- **Original Hadoop Architecture**

<p align="center"><img src="images/originalhadooparch.png" width="500px"></p>

#

- **Yarn: NextGen MapReduce**

<p align="center"><img src="images/yarn_architecture.gif" width="500px"></p>

  - The Resource Manager basically gets job requests from the clients node status from the Node Manager.

  - They're two components in the Resource Manager. There's a **scheduler** which is essentially responsible for allocating resources to the various applications that are running. So these are essentially with the constraints of capacities and
  the queues and things like that. And there are **policy plugins** that are available for the scheduling aspect effect, so you could have a capacity scheduler or you could have a fair share scheduler, things like that.

#

- **Additional Yarn Features**

  - High Availability ResourceManager;

  - Timeline Server;

  - Use of [Cgroups](http://man7.org/linux/man-pages/man7/cgroups.7.html);

  - Secure Containers;

  - YARN - Web Services / REST APIs.

#

### The Hadoop Execution Environment

- **The Hadoop Execution Environment**

  - **Recall Hadoop Architecture**

    - Data distributed across nodes;

    - Keep compute task on the node with data.

<p align="center"><img src="images/recallhadoop.png" width="500px"></p>

  - **MapReduce Execution Framework**

    - Software Framework;

    - Schedules, monitors and manages tasks;

    - Works with applications that fit MapReduce paradigm.

<p align="center"><img src="images/mapreduceexecution.png" width="500px"></p>

#

- **Yarn, Tez and Spark**

  - **Yarn**

    - Supports the classic MapReduce framework;

    - Supports Open Source/Commercial Applications;

    - Supports user development applications;

    - Works with frameworks like Tez, Spark, Impala, etc.

<p align="center"><img src="images/yarn-tez-spark.png" width="500px"></p>    

  - **Tez**

    - It can handle data flow graphs (Is the main component);

    - It lets you customize data formats;

    - Can run complex DAG (Directed Acyclic Graph) of tasks;

    - Dynamic DAG Changes;

    - Resource usage efficiency. With Tez, you could have essentially one container, and reuse it. This improves efficiency and makes things things much faster.

#    

  _HIVE on Tez Example_

  ```
  SELECT a.vendor, COUNT(*), AVG(c.cost) FROM a
  JOIN b ON (a.id = b.id)
  JOIN c ON (a.itemid = c.itemid)
  GROUP BY a.vendor        
  ```
#

_HIVE Example - Mapreduce **(Not so efficient)**_

<p align="center"><img src="images/hive-mapreduce.png" width="500px"></p>

_HIVE Example - Tez **(Efficiency improved)**_

<p align="center"><img src="images/hive-tez.png" width="500px"></p>

#

  - **Spark**

    - Advanced DAG execution engine;

    - Supports cyclic data flow;

    - In-memory computing;

    - Supports Java, Scala, Python and R;

    - Existing optimized libraries.

    - [_Spark DAG Explanation_](https://www.quora.com/What-are-the-Apache-Spark-concepts-around-its-DAG-Directed-Acyclic-Graph-execution-engine-and-its-overall-architecture)

#

_Spark Example **(Logistic Regression Example - Using Python)**_

  ```
  points = spark.textFile(...).map(parsePoint).cache()
  w = numpy.random.ranf(size = D) # current separating plane
  for i in range(ITERATIONS):
    gradient = points.map(lambda p: (1 / (1 + exp(-p.y*(w.dot(p.x)))) - 1) * p.y * p.x).reduce(lambda a, b: a + b)
    w -= gradient
  print("Final separating plane: %s" %w)
  ```

#  

- **Hadoop Resource Scheduling**

  - What is the motivation for schedulers?

    - Various execution engines/options;

    - Scheduling, Performance;

    - Control of resources between components.

  - Schedulers:

    - Default - First In, First Out (FIFO);

    - Fairshare - In Fairshare, what you do is try to balance out the resource allocation accross applications over time;

    - Capacity - In capacity schedulers, you can have a guaranteed capacity for each application or group, and are safeguards to prevent a user or an application from taking down the whole cluster by running it out the resources.

#

- **Capacity Scheduler**

  - Queues and sub-queues;

  - Capacity guarantee with elasticity;

  - ACLs for security;

  - Runtime changes/draining apps;

  - Resource based scheduling.

<p align="center"><img src="images/capacity-scheduler.png" width="500px"></p>

#

- **Fairshare Scheduler**

  - Balances out resource allocation among apps over time;

  - Can organize into queues/sub-queues;

  - Guarantee minimum shares;

  - Limits per use/app;

  - Weighted app priorities;

<p align="center"><img src="images/fairshare-scheduler.png" width="500px"></p>

#

### Overview of the Hadoop based Applications and Services

- **Hadoop-Based Applications**

  - **Databases/Stores**:

    - **Avro:** Data structures within context of Hadoop MapReduce jobs;

    - **HBase:** Distributed non-relational database;

    - **Cassandra:** Distributed data management system.

  - **Querying**

    - **Pig:** Platform for analyzing large data sets in HDFS;

    - **Hive:** Query and manage large data sets;

    - **Impala:** High-performance, low-latency SQL querying of data in Hadoop file formats;

    - **Spark:** General processing engine for streaming, SQL, machine learning and graph processing.

  - **Machine Learning, Graph Processing**

    - **Giraph:** Iterative graph processing using Hadoop framework;

    - **Mahout:** Framework for machine learning applications using Hadoop and Spark;

    - **Spark:** General processing engine for streaming, SQL, machine learning and graph processing.

#

- **Introduction to Apache Pig**

  - Two components: **Pig Latin** and **Infrastructure Layer**:

    - **Pig Latin:** Pig's high level scripting language;

    - **Infrastructure Layer:** Takes what was written in Pig Latin and transforms it into the backend MapReduce jobs or Tez jobs or other applications that are backend in Pig.

  - It's essentially a platform for data processing;

  - Pig execution environment: Local, MapReduce, Tez, Yarn, etc;

  - Pig has a lot of operators and functions;

  - It is extensible, you can write constant functions if you have complex processing to do;

  - It's a great tool to do _Extract, Transform and Load (ETL)_ operations;

  - It's a good tool to manipulating and analyzing "raw" data;

#

_Pig Example (In Cloudera VM)_

- **Step 1:** Load passwd file and work with data

`$ hdfs dfs -put /etc/passwd /user/cloudera`

- **Step 2:**

`$ pig -x mapreduce` _(This command puts you in "grunt" shell)_

- **Step 3:** Inside the "grunt" shell, load the file:

`grunt> A = load '/user/cloudera/passwd' using PigStorage(':');`

- **Step 4:** Still inside the "grunt" shell, pick subset os values:

```
grunt> B = foreach A generate $0, $4, $5 ;

grunt> dump B;
```

_OBS: These commands outputs username, full name and home directory path_

- **Step 5:** Still inside the "grunt" shell, store this process data in HDFS:

`grunt> store B in 'userinfo.out';`

- **Step 6:** Outside the grunt shell, verify the new data is in HDFS:

`$ hdfs dfs -ls /user/cloudera`

`$ hdfs dfs -ls /user/cloudera/userinfo.out`

#

- **Introduction to Apache HIVE**

  - Data Warehouse software;

  - HiveQL - SQL like language to structure and query data;

  - Execution Environment: MapReduce, Tez, Yarn, Spark, etc;

  - Works with data in HDFS and HBase;

  - Works with custom mappers/reducers;

  - Hive usage areas: Data mining, machine learning, Ad Hoc analysis and others.

#

_HIVE Example (In Cloudera VM)_

- **Step 1:** Copy passwd file to HDFS:

`$ hdfs dfs -put /etc/passwd /tmp/`

`$ hdfs dfs -ls /tmp`

- **Step 2:** Running interactively using beeline:

`$ beeline -u jdbc:hive2://`

- **Step 3:** Run the Create table command:

```
0: jdbc:hive2://> CREATE TABLE userinfo ( uname STRING, pswd STRING, uid INT, gid INT, fullname STRING, hdir STRING, shell STRING ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ':' STORED AS TEXTFILE;
```

- **Step 4:** Load passwd file from HDFS:

`0: jdbc:hive2://> LOAD DATA INPATH '/tmp/passwd' OVERWRITE INTO TABLE userinfo;`

- **Step 5:** Select info - This launches the Hadoop job and outputs once its complete:

`0: jdbc:hive2://> SELECT uname, fullname, hdir FROM userinfo ORDER BY uname ;`

- **OBS:** Completed MapReduce jobs; output shows username, fullname and home directory.

#

- **Introduction to Apache HBase**

  - Scalable data store;

  - It works with non-relational distributed database;

  - It runs on top of HDFS;

  - It supports compression, which basically lets you lower the network traffic and also the size of the disk;

  - In-memory operations: MemStore and BlockCache.

- **Features of the Apache HBase**

  - Consistency (The transition of a table from one valid state to another happens directly without intermediate changes. So, the data won't disappear if you are doing an upgrade. This is important if you are looking at the consistency of what we are reading and what we are processing);

  - High Availability (It provides a lot of mechanisms to make sure that your data is available, doing range partition of keys across servers and spreading out the keys across various regions of your data in HDFS. It keeps read-only copies of data in secondary regions);

  - Automatic Sharding;

  - Replication (You can do different modes of replication with HBase servers);

  - Security;

  - SQL-like access (Hive, Spark, Impala);

#

_HBase Example_

- **Step 1:** Access HBase shell:

`$ hbase shell`

- **Step 2:** Create Table:

`hbase(main):002:0> create 'userinfotable',{NAME=>'username'},{NAME=>'fullname'},{NAME=>'homedir'}`

- **Step 3:** Add data:

```
hbase(main):002:0> put 'userinfotable','r1','username','vcsa'
hbase(main):002:0> put 'userinfotable','r2','username','sasuser'
hbase(main):002:0> put 'userinfotable','r3','username','postfix'
hbase(main):002:0> put 'userinfotable','r1','fullname','VirtualMachine Admin'
hbase(main):002:0> put 'userinfotable','r2','fullname','SAS Admin'
hbase(main):002:0> put 'userinfotable','r3','fullname','Postfix User'
hbase(main):002:0> put 'userinfotable','r1','homedir','/home/vcsa'
hbase(main):002:0> put 'userinfotable','r2','homedir','/var/sasuser'
hbase(main):002:0> put 'userinfotable','r3','homedir','/user/postfix'
```

- **Step 4:** Scan table after data entry:

`hbase(main):002:0> scan 'userinfotable'`

- **Step 5:** Select info from all rows corresponding to column 'fullname'

`hbase(main):002:0> scan 'userinfotable',{COLUMNS=>'fullname'}`

#

### Introduction to Hadoop Distributed File System (HDFS)

- **HDFS Architecture and Configuration**

- **Overview of HDFS Architecture**

  - **HDFS Design Concept**

    - Scalable distributed filesystem;

    - Distribute data on local disks on several nodes;

    - Low cost commodity hardware.

<p align="center"><img src="images/hdfs-design-concept.png" width="500px"></p>


  - **HDFS Design Factors**

    - Hundreds/Thousands of nodes => Need to handle node/disk failures;

    - Portability across heterogeneous hardware/software;

    - Handle large data sets;

    - High throughput.


  - **Aproach to meet HDFS design goals**

    - **Simplified coherency model** - Write once read many. That simplifies the number of operations you have to do to commit the write;

    - **Data replication** - Helps to handle hardware failures. So what you do is try to spread the data, same piece of data on different nodes;

    - **Move computation close to data** - That improves your performance and throughput;

    - **Relax [POSIX](https://whatis.techtarget.com/definition/POSIX-Portable-Operating-System-Interface) requirements** - increase throughput.

#

- **HDFS ARCHITECTURE**

<p align="center"><img src="images/hdfsdesign.png" width="500px"></p>

  - There is a Namenode which essentially carries all the MetaData;

  - The data is spread out over DataNodes;

  - If you have a file that gets broken up into blocks and these blocks are placed on the DataNodes, they're replicated among the DataNodes;

#  

- **Summary of HDFS Architecture**

  - **Single NameNode:** a master server that manages the file system namespace and regulates access to files by clients.

  - **Multiple DataNodes:** tipically one per node in the cluster. Functions:

    - Manage storage;

    - Serving read/write requests from clients;

    - Block creation, deletion, replication based on instructions from NameNode.

#

- **The HDFS Performance Envelope**

  - **HDFS block size**

    - Default block size is 64MB;

    - Good for large files;

    - So a 10GB file will be broken into: _10x1024/64 = 160 blocks_.

  - **Importance of the number of blocks in a file**

    - **Namenode memory usage:** Every block represented as object (default replication this will be further increased 3X);

    - **Number of map tasks:** data tipically processed block at a time.

  - **Large number of small files: Impact on the NameNode**

    - **Memory usage:** circa 150 bytes per object. 1 billion object = 300GB memory!

    - **Network Load:** number of checks with datanodes proportional to number of blocks;

    - **Map Tasks:** depends on number of blocks. 10GB data, 32k file size = 327.680 map tasks;

      - Lots of queued tasks;

      - Large overhead of spin up/tear down for each task;

      - Inneficient disk I/O with small sizes.

      _So in all aspects, having too many map tasks is not good._

    - **HDFS optimized for large files**

      - **Key takeaway** - lots of small files is bad!

      - Solutions:

        - Merge/Concatenate files;

        - Sequence files;

        - HBase, HIVE configuration;

        - CombineFileInputFormat.

#

**Read/Write Processes in HDFS**

**Write process in HDFS**

- Client request to create file (With client side buffering/caching):

<p align="center"><img src="images/hdfs_write_process_1.png" width="500px"></p>

- NameNode contacted once a block of data is accumulated:

<p align="center"><img src="images/hdfs_write_process_2.png" width="500px"></p>

- NameNode responds with list of DataNodes / Rack Aware:

<p align="center"><img src="images/hdfs_write_process_3.png" width="500px"></p>

- First DataNode receives data, writes to local and forwards to second DataNode:

<p align="center"><img src="images/hdfs_write_process_4.png" width="500px"></p>

<p align="center"><img src="images/hdfs_write_process_5.png" width="500px"></p>

- NameNode commits file creation into persistent store. Receives heartbeat and block reports:

<p align="center"><img src="images/hdfs_write_process_6.png" width="500px"></p>

- Client gets DataNode list from NameNode. Read from replica closest to reader:

<p align="center"><img src="images/hdfs_write_process_7.png" width="500px"></p>

#

**HDFS Performance and Tuning**

**HDFS Tuning Parameters**

- **HDFS configuration file**

  - Parameters are in _hdfs-site.xml_;

  - Commercial vendors have GUI based management consoles to make changes.

- **HDFS Block Size**

  - Impacts NameNode memory, number of map tasks and hence performance;

  - 64MB is the default. Can be changed in the workloads. Typically bumped up to 128MB;

  - dfs.blocksize or dfs.block.size _(Size parameters to be changed)_.

- **HDFS Replication**

  - Default replication is **3**;

  - Parameter: _dfs.replication_;

  - Tradeoffs:

    - Lower it to reduce replication cost;

    - Less robust;

    - Higher replication can make data local to more workers;

    - Lower replication **=>** more space;

- **HDFS most important parameters**

    - dfs.datanode.handler.count(10): _Sets the number of server threads on each datanode_;

    - dfs.namenodes.fs-limits.max-blocks-per-file: _Maximum number of blocks per file_.

**Full list:** http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/hdfs-default.xml

#

**HDFS Performance and Robustness**

- **Common Failures**

  - _DataNode Failures:_ Server can fail, disk can crash, data corruption;

  - _Network Failures_;

  - _NameNode Failures:_ Disk failure, node failure;

- **HDFS Robustness**

  - NameNode receives heartbeat and block reports from DataNodes.

<p align="center"><img src="images/hdfsrobustness.png" width="500px"></p>

- **Mitigation of common failures**

  - _Checksum computed_ on file creation;

  - _Checksums stored in HDFS namespace_;

  - Used to check retrieved data. _Re-read from alternate replica need_.

  - Multiple copies of central metadata structures;

  - Failover to standby NameNode - manual by default.

- **Performance**

  - Changing blocksize and replication factor can improve performance;

  - Hadoop distcp allows parallel transfer of files.

- **Replication trade offs w.r.t robustness**

  - Reducing replication has a trade off w.r.t robustness:

    - Might lose a node or local disk during the run - _cannot recover if there is no replication_;

    - If there is data corruption of a block from one of the datanodes - _again, cannot recover without replication_.

#

**HDFS Access, Commands, APIs and Applications**

- **Overview of HDFS Access, APIs and Applications**

- **HDFS Commands**

  - Invoked via bin/hdfs script;

  - User commands - filesystem shell commands for routine operations;

  - Administrator commands;

  - Debug commands;

  - Details at: https://hadoop.apache.org/docs/current//hadoop-project-dist/hadoop-hdfs/HDFSCommands.html

- **Application programming interfaces**

  - **Native Java API:** Base class org.apache.hadoop.fs.FileSystem;

  - **C API for HDFS:** libhdfs, header file (hdfs.h);

  - **WebHDFS REST API:** HTTP, Get, Put, Post and Delete operations.

- **HDFS NFS Gateway**

  - Mount HDFS as a filesystem on the client;

  - Browse files using regular filesystem commands;

  - Upload/Download files from HDFS;

  - Stream data to HDFS.

- **Several other options!**

  - **Apache Flume:** collecting, aggregating streaming data and moving into HDFS;

  - **Apache Sqoop:** Bulk transfer between Hadoop and datastores.

- **Applications using HDFS**

  - Can use API to interact with HDFS;

  - Core component of Hadoop Stack - used by all applications;

  - HBase is a good example of an application that runs on top of HDFS with good integration;

  - Spark can run directly on HDFS without other Hadoop components.

#

**HDFS Commands**

- **HDFS User Commands:**

  - List files in /: `$ hdfs dfs -ls /`

  - Make a directory: `$ hdfs dfs -mkdir /user/test`

  - Create a local file: `$ dd if=/dev/urandom of=sample.txt bs=64M count=16` _(Creates 1GB file called sample.txt on the local filesystem)_

  - Copy the created file to the user's directory in HDFS: `$ hdfs dfs -put sample.txt /user/test`

  - List the copied file in HDFS: `$ hdfs dfs -ls /user/test/sample.txt`

  _OBS1: Whatever files created in the quickstart (with dd command) aren't in HDFS, they are on a local file system on the node. So, we have to activate port tagging to the HDFS file system. The command to do that is: $ hdfs dfs -put sample.txt._

  _OBS2: The number after the permissions in file list, shows the file replication, as we can see marked in red in the image below:_

  <p align="center"><img src="images/filereplication.png" width="500px"></p>

  - HDFS fsck: `$ hdfs fsck /user/test/sample.txt` _(This command is not like linux's hdfs. It shows you the file information in HDFS)_

  - User commands:

  <p align="center"><img src="images/usercommands.png" width="500px"></p>

- **HDFS Administrator Commands**

  - Summary report: `$ hdfs dfsadmin -report`

#

**Native Java API for HDFS**

- **FSDataInputStream Methods**

  - _read_: read bytes;

  - _readFully_: read from stream to buffer;

  - _seek_: seek to given offset;

  - _getPos_: get current position in stream.

- **FSDataOutputStream Methods**

  - _getPos_: get current position in stream;

  - _hflush_: flush out the data in client's user buffer;

  - _close_: close the underlying output stream.

- **Reading from HDFS using API**

  - _get_ an instance of FileSystem:

    `FileSystem fs = FileSystem.get(URI.create(uri),conf);`

  - _Open_ an input stream:

    `in = fs.open(new Path(uri));`

  - Use IO utilities to _copy_ from input stream:

    `IOUtils.copyBytes(in, System.out,4096,false);`

  - Close the stream:

    `IOUtils.closeStream(in);`

- **Writing to HDFS using API**

  - _get_ an instance of FileSystem:

    `FileSystem fs = FileSystem.get(URI.create(outuri),conf);`

  - _Create_ a file:

    `out = fs.create(new Path(outuri));`

  - Write to output stream:

    `out.write(buffer, 0, nbytes);`

  - Close the file:

    `out.close()`

- **REST API for HDFS**

  - **Enabling WebHDFS**

    - In _hdfs-site.xml_

      - dfs.webhdfs.enabled

      - dfs.webhdfs.authentication.kerberos.principal

      - dfs.webhdfs.authentication.kerberos.keytab  

  - **Accessing hdfs-site.xml**

      - Command: `$ more /etc/hadoop/conf/hdfs-site.xml`

  - _Example of dfs.webhdfs.enable configuration inside the /etc/haddop/conf/hdfs-site.xml)_

  ```
  <property>
     <name>dfs.webhdfs.enabled</name>
     <value>true</value>
  </property>
  ```

- **Authentication**

  - If security is off:

  `$ curl -i "http://<HOST>:<PORT>/webhdfs/v1/<PATH>?[user.name=<USER>&]op=..."`

  - Security on with Kerberos:

  `$ curl -i --negotiate -u : "http://<HOST>:<PORT/webhdfs/v1/<PATH>?op=..."`

  - Security on using Hadoop delegation token:

  `$ curl -i "http://<host>:<port>/webhdfs/v1/<PATH>?delegation=<TOKEN>&op=..."`

- **HTTP GET Requests**

  `$ curl -i "http://quickstart.cloudera:14000/webhdfs/v1/user/cloudera?user.name=cloudera&op=GETFILESTATUS"`

- **HTTP PUT Requests**

  `$ curl -i -X PUT "http://quickstart.cloudera:14000/webhdfs/v1/user/test?user.name=cloudera&op=MKDIRS&permission=755"`

- **HTTP GET request on status**

  `$ dd if=/dev/urandom of=sample.txt bs=64M count=16`

  `$ hdfs dfs -put sample.txt /user/test/`

  `$ curl -i "http://quickstart.cloudera:14000/wehdfs/v1/user/test?user.name=cloudera&op=GETCONTENTSUMMARY"`

- **HTTP Operations**

  - _HTTP GET:_ file status, checksums, attributes;

  - _HTTP PUT:_ create, change ownership, rename, permissions, snapshot;

  - _HTTP POST:_ append, concatenate;

  - _HTTP DELETE:_ delete files, snapshot.

- _Resources:_

  - Commands:https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HDFSCommands.html

  - JAVA API: http://hadoop.apache.org/docs/current/api/org/apache/hadoop/fs/FileSystem.html

  - C/libhdfs: https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/LibHdfs.html

  - WebHDFS API:https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html

#

### Introduction to Map/Reduce

**Introduction to Map/Reduce:**

- **The Problem:** Big data means lots of hard drives.

- **The Solution:** Lots of data means we should bring computation to data.

#

- **The Problem:** Lots of disks.

- **Possibility 1:** Data needs updating, so:

<p align="center"><img src="images/mr1.png" width="500px"></p>

- **Possibility 2:** Need to sweep through data, so:

<p align="center"><img src="images/mr2.png" width="500px"></p>

#

**The Map/Reduce Framework**

- **The Framework:**

  - **User defines:**

    - A. <key, value>

    _Explanation: All our data is gonna be placed into key-value pairs. We could think of it as that a key-value pair is gonna become our basic unit of data and our unit of analysis._

    - B. Mapper and Reduce functions

    _Explanation: The user has to specify mapper and reducer functions. The mapper is the function that applied to the data, and the reducer is the function that is applied to the intermediate results that is gonna come from Hadoop._

  - **Hadoop handles the logistics:**

    _Explanation: Hadoop handles all the logistics of parallel execution, of the map and reduce functions, producing the intermediate results and communicating those results to the reducers._

  - **The Logistics:**

    - Hadoop handles the distribution and execution:

    _Explanation: Hadoop distributes the map functions to the data. Hadoop shuffles and groups data according to the key-value pairs. All pairs with the same key are grouped together and passed to the same reducer._

  - **Map/Reduce Flow**

    - User defines a map function:

      - _map()_

    - The _map()_ function reads data and outputs _<key,value>_:

      - _The map function will read in the data and output a key-value pair._

<p align="center"><img src="images/key-value.png" width="500px"></p>

- User defines a reduce function:

  - _reduce()_

- The _reduce()_ function reads _<key,value>_ and outputs your result:

  - _The reduce function is built to read in the key-value pair and output a result._

<p align="center"><img src="images/key-value-reduce.png" width="500px"></p>

- Hadoop distributes data map() to data:

<p align="center"><img src="images/maptodata.png" width="500px"></p>

- Haddop groups <key,value> data:

<p align="center"><img src="images/hadoopgroups.png" width="500px"></p>

- Hadoop distributes groups to reducers():

<p align="center"><img src="images/groupstoreducers.png" width="500px"></p>

#

**Map/Reduce Examples and Principles**

**Recall the framework**

- User defines <key, value>, mapper and reducer;

<p align="center"><img src="images/map-reduce.png" width="500px"></p>

- Hadoop handles the logistics _(Parallelization, shuffling and grouping of key value pairs)_.

<p align="center"><img src="images/hadoop-logistics.png" width="500px"></p>

**Hadoop rule of thumb**

- 1 mapper per data split (tipically);

- 1 reducer per computer core (best parallelism).

**Wordcount strategy**

- Let <word, 1> be the <key, value>;

- Simple mapper and reducer;

- Hadoop did the hard work of shuffling and grouping.

**Good key-value properties**

- Simple;

- Enables reducers to get correct output.

**Good task decomposition**

- Mappers: simple and separable;

- Reducers: easy consolidation.

#

**MapReduce: Trending Wordcount (Example)**

- Twitter Data: date, message, location... [other metadata]

  - **Task1:** Get word count by day;

  - **Task2:** Get total word count.

- _Solutions:_

  - **Task1:**

    - Get word count by day;

    - Design: Use composite key;

    - Map/Reduce: <date word, count>.

  - **Task2:**

    - Get total word count;

    - Easy way: re-use the previous wordcount.

#

**MapReduce Example: Joining Data**

- _Task:_ combine datasets by key

  - A standard data management function;

  - In pseudo SQL:

    `Select * from table A, table B, where A.key=B.key`

  - Joins can be inner, left or right outer. _(We will consider the inner join, where only matching cases are selected for retrieval. Meaning, matching cases in both the first table or in the second table.)_

#

- _Task:_ given two wordcount datasets...

- **File A: <word, total-count>** _(Total Wordcount)_

<p align="center"><img src="images/filea-totalwordcount.png" width="300px"></p>

- **File B: <date word, day-count>** _(Wordcount by date word combinantion)_

<p align="center"><img src="images/fileb-datewordcombinantion.png" width="300px"></p>

#

- _Task:_ combine by word

- **File A: <word, total-count> File B: <date word, day-count>**

<p align="center"><img src="images/combinebyword.png" width="500px"></p>

- Result wanted: **File AjoinB: <word date, day-count total-count>**

<p align="center"><img src="images/resultwanted.png" width="400px"></p>

#

- **Recall that data is split in parts**

_Keep in mind that the info you need could be spread out over different parts. Specially when this is a large dataset. How do we gather the right pieces of data to produce the joint output?_

<p align="center"><img src="images/datasplit.png" width="500px"></p>

- **Key-Value and Task Decomposition**

- Main design consideration:

  _Join depends on word (e.g. Select * where A.word=b.word)_

- For the join:

    - Let \<key\> = word

    - Let \<value\> = other info

    <word, ...>

    _The mapper should set the word to be the key._

- Note:

<p align="center"><img src="images/wordalreadythekey.png" width="500px"></p>

<p align="center"><img src="images/datafilteredout.png" width="500px"></p>

<p align="center"><img src="images/shoulddate.png" width="500px"></p>

_We can put that date information into the value part of the field and let Hadoop just carry that extra information._

<p align="center"><img src="images/valuefield.png" width="500px"></p>

- Now data sets are:

  - **File A: <word, total-count> File B_new: <word, date count>**

<p align="center"><img src="images/newdatasets.png" width="500px"></p>

- How will Hadoop shuffle and group these?

  - **File A: <word, total-count> File B_new: <word, date day-count>**

<p align="center"><img src="images/hadoop-shuffle.png" width="400px"></p>

  - Let's focus on 1 key:

<p align="center"><img src="images/1key.png" width="400px"></p>

  - Hadoop gathers the data for a join:

<p align="center"><img src="images/gathers-join.png" width="400px"></p>

  - Reducer now has all the data for same word grouped together:

<p align="center"><img src="images/reducer-grouped.png" width="400px"></p>

  - Reducer now can join the data and put date back into key:

<p align="center"><img src="images/reducer-join.png" width="400px"></p>

#

**MapReduce Example: Vector Multiplication**

- Task: Multiply 2 arrays of _N_ numbers:

  - A basic mathematical operation;

  - Let's assume _N_ is very large.

<p align="center"><img src="images/vectors.png" width="400px"></p>

<p align="center"><img src="images/data-partitioned.png" width="400px"></p>

- Main design consideration: need elements with same index together:

  - _Let <key, value> = <index, number>_

- **Problem:** array partitions don't have an index. The files are just NUMBERS!!!

  - Hadoop MapReduce implementation does have some ways to get extra information from the **execution environment** or from the **configuration settings**;

<p align="center"><img src="images/environment-information.png" width="400px"></p>

  - That information is available to the mapper with special function calls. This extra information can be passed along in the key value output, or it can be used as a side effect in which the mapper puts some data outside the Hadoop system;

<p align="center"><img src="images/info-mapreduce.png" width="400px"></p>

- _Example:_

<p align="center"><img src="images/vectormult1.png" width="400px"></p>

<p align="center"><img src="images/vectormult2.png" width="400px"></p>

<p align="center"><img src="images/vectormult3.png" width="400px"></p>

<p align="center"><img src="images/vectormult4.png" width="400px"></p>

<p align="center"><img src="images/vectormult5.png" width="400px"></p>

<p align="center"><img src="images/vectormult6.png" width="400px"></p>

#

**Computacional Costs of Vector Multiplication**

- **For Vector Multiplication**

  - How many \<index, number\> are output from map()?

  ```
    For: 2 Vectors with
         N indices each

    Then:
         2N <index, number>
         are output from map()  
  ```         

  - How many \<index\> groups have to be shuffled by Hadoop?

  ```
    For: 2N indices and
         N pairs

    Then:
         N groups are shuffled to
         reducers.
  ```

  _OBS: The actual cost of this operation is gonna depend on how Hadoop partitions the data, how many reducers there are, how many computer nodes there are and the communication cost between computer nodes, for example._

  - Can we reduce shuffling cost?

    - Try: combine map indices in mapper. _(works better for Wordcount)_

    - Or try: use index ranges of lenght R. _(Re-number the indices into bins)_

  _Explanation:_

  - For example, let R=10 and bin the array indices:

  1. Let's say we bin the indices into ranges of lenght ten. We start with the original _N_ keys.

  2. We put each set of ten ranges into a bin, then we use the bins as the key.

  3. So now, instead of _N_ indices, now there are N/10 indices.

  4. The new key is now the index bin number and the original index number can be put into the value field to be used later.

  5. Bin one from vector A will still group with bin one from vector B and reduce will still be able to finish the multiplication by using the original indexes that are now part of the value field.

<p align="center"><img src="images/binindices.png" width="400px"></p>

- Now shuffling costs depend on N/R groups. Now we can rewrite the shuffling cost using N divided by B.

  ```
    If: R=1
    Then: N/R=N groups (same as before)

    If: R>1
    Then: N/R<N (less shuffling to do)
  ```

  - Trade-offs:

  ```
    If:
        size of (N/R) is high
    Then:
        shuffle costs are also high
    But:
        reducer complexity is lower  
  ```

- **Vector to Matrices**

  - Matrix multiplication needs row-index and col-index in the keys;

  - Matrix multiplication more pertinent to data analytic topics;

#

**MapReduce Summary**

- **Task Decomposition**

  - Mappers are separate and independent;

  - Mappers work on data parts;

- **Design Considerations**

  - \<key, value\> must enable correct output;

  - Let Hadoop do the hard work;

  - Trade-offs;

  - Programming > Hadoop;

  - Common mappers:

    - Filter (subset data);

    - Identity (just pass data);

    - Splitter (as for counting);

  - Composite \<keys\>;

  - Extra info in \<values\>;

  - Cascade Map/Reduce jobs;

  - Bin keys into ranges;

  - Aggregate map output when possible (combiner option);

- **Potential Limitations of Map/Reduce**

  - Must fit \<key, value\>;

  - Map/Reduce data nor persistent;

  - Requires programming/debugging;

  - Not interactive;

- **Beyond Map/Reduce**

  - Data access tools (Pig HIVE);

    - SQL like syntax;

  - Interactivity and Persistency (Spark);

#  

### Introduction to Hadoop Spark

**Introduction to Hadoop Spark**

  - **Shortcomings of MapReduce**

    - _Force your pipeline into Map/Reduce steps:_ Everytime you implement a workflow in MapReduce, you have to force your data analysis workflow into a map and a reduce phase. Sometimes, this cannot accommodate every data analysis workflow.

    - _Read from disk for each MapReduce job:_ MapReduce relies heavily on reading data from disk, specially if you have iterative algorithms that require cycling several times through the data. Pipelines like this are very common in Machine Learning. You will be reading data from this many times. This makes your analyst pipeline very slow.

    - _Only native JAVA programming interface:_ It´s possible to use Python and other languages, but, that requires to go through the streaming module that makes the implementation more complex and not very efficient, specially when you are running not with text data, but with floating point numbers.

  - **Solutions?**

    - _New Framework:_ same features of MapReduce and more;

    - Capable of reusing Hadoop ecosystem, like, HDFS, Yarn, etc;

    - Born in UC Berkeley, but, today is managed by Apache Foundation, like Hadoop.

  - **Solution by Spark**

    - _Accomodate other workflows:_ Spark provides a very rich programming interface that gives you more than 20 highly efficient distributed operations;

    - _Iterative algorithms:_ In-memory caching of data specified by the user;

    - _Interactivity and support to other languages:_ Python, Scala and R interfaces. Interactive shells.

  - **100TB sorting competition**

  <p align="center"><img src="images/sorting-competition.png" width="500px"></p>

#

**Architecture of Spark**

  - **Worker Node:** In Spark we have a general executor Java Virtual Machine. It can execute tasks related to mapping stages, reducing stages or other Spark specific workflows. The Java Virtual Machine is the core where all the computation is executed. This is the interface to the rest of the Hadoop Ecosystem. If we have the Hadoop File System, on each worker node some of the data will be stored locally. The most important point of this computing framework is to bring the computation to the data. Spark will send some computational jobs to be executed on the data are already available on the machine.

  - If you are using PySpark, there will be several Python processes. Generally one per task, but, you can configure it depending on your application. The Python processes are connected to the Java Virtual Machine and data are shipped from the Java Virtual Machine to Python for processing.

  <p align="center"><img src="images/workernodes.png" width="500px"></p>

  - We can have hundreds or thousands of worker nodes. It's important to have a system that can automatically manage provisioning and restarting of these nodes, and this system is called the cluster manager. Spark supports two interfaces for cluster management. One is YARN, which is the Hadoop cluster manager,
  and the other is a Standalone mode. Standalone mode means that there is a special Spark process that takes care of restarting nodes that are failing, or starting nodes at the beginning of the computation. And instead, using the YARN interface has an advantage because we can use this in conjunction with Hadoop MapReduce and other Hadoop.

  <p align="center"><img src="images/clustermanager.png" width="500px"></p>

  <p align="center"><img src="images/driverprogram.png" width="500px"></p>

#

**Resilient Distributed Dataset**

- **RDD (Resilient Distributed Dataset):** The RDD or Resilient Distributed Dataset are the data containers used by Spark to store yor data.

  - **Dataset:** Data storage created from: HDFS, S3, HBase, JSON, text or local hierarchy of folders;

  - **Distributed:** Distributed across the cluster of machines. The data is divided in partitions, atomic chunks of data;

  - **Resilient:** Recover from errors, e.g. node failure and slow processes. Tracks history of each partition. In every point in your calculations, Spark knows which are the partitions needed to recreate the partition in case it gets lost. If that happens, then Spark automatically figures out where it can start from to recompute what's the minimum amount of processing needed to recover the lost partition.

- **Check Partitions:**

  - **From the PySpark console:**

    `integer_RDD = sc.paralellize(range(10), 3)`

  - **Gather all data on the driver:**

    `integer_RDD.collect()`

    **Out:** _[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]_

  - **Maintain splitting in partitions:**

    **Out:** _[[0,1,2], [3,4,5], [6,7,8,9]]_

- **Read text into Spark:**

  - **from local filesystem:**

    `text_RDD = sc.textFile("file:///home/cloudera/testfile1")`

  - **from HDFS:**

    `text_RDD = sc.textfile("/user/cloudera/input/textfile1")`

    `text_RDD.take(1)` #outputs the first line

  - **Wordcount in Spark: map**

    ```
    def split_words(line):
        return line.split()
    ```

    ```
    def create_pair(word):
        return (word, 1)
    ```

    `pairs_RDD=text_RDD.flatMap(split_words).map(create_pair)`

    `pairs_RDD.collect()`

    **Out[]**:[(u'A', 1),

    (u'long', 1)

    (u'time', 1)

    (u'ago', 1)

    (u'in', 1)

    (u'a', 1)

    (u'galaxy', 1)

    (u'far', 1)

    (u'far', 1)

    (u'away', 1)]

  - **Wordcount in Spark: reduce**

    ```
    def sum_counts(a, b):
      return a + b
    ```

    `wordcounts_RDD = pairs_RDD.reduceByKey(sum_counts)`

    `wordcounts_RDD.collect()`

    **Out[]**:

    [(u'A', 1),

    (u'ago', 1)

    (u'far', 2)

    (u'away', 1)

    (u'in', 1)

    (u'long', 1)

    (u'a', 1)

    (u'time', 1)

    (u'galaxy', 1)]

#

**Spark Transformations**

  - RDD are immutable;

  - Never modify RDD in place;

  - Transform RDD to another RDD;

  - All the transformations are lazy;

  - **Create RDD:**

    - From local filesystem:

      `text_RDD = sc.textFile("file:///home/cloudera/testfile1")`

  - **Apply a transformation: map**

    - **map:** apply function to each element of RDD

      ```
      def lower(line):
        return line.lower()
      lower_text_RDD = text_RDD.map(lower)
      ```    

<p align="center"><img src="images/rddpartitions.png" width="450px"></p>

#

**Other transformations**

- **flatMap (function):** flatMap is very similar to Map. In the Map case we have one element as an input and one element as an output. Instead, flatMap accepts a function that might have any number of output for one input.

```
def split_words(line):
  return line.split()
words_RDD = text_RDD.flatMap(split_words)
words_RDD.collect()
```

**Out[]**:

[u'A',

u'long',

u'time',

u'ago',

u'in',

u'a',

u'galaxy',

u'far',

u'far',

u'away',]

**OBS:** _The output is just the list of all of the words._

**flatMap:** map then flatten output

<p align="center"><img src="images/flatmap.png" width="450px"></p>

#

- **filter (function):** Filter function takes one element of my RDD and for each of this element returns either _True_ or _False_. _True_ if we wanna keep this element or _False_ if we don´t. The code example below takes the input word, then transforms it to lowercase and checks if this starts with **a**. If it starts with **a**, it returns _True_. If not, it returns _False_. It is filtering out everything that doesn´t start with **a**.

```
def starts_with_a(word):
  return word.lower().startswith("a")
words_RDD.filter(starts_with_a).collect()
```

**Out[]:** [u'A', u'ago', u'a', u'away]

**filter:** keep only elements where func is true

<p align="center"><img src="images/filter.png" width="450px"></p>

#

- **coalesce:** At the example below, it´s introduced the function _"glom"_, which is very useful for debbugging purposes because turns the content of one partition into an array. In the example, we can parallelize on the range of numbers between 0 and 9, and we specify that in parallelize we want to have 4 partitions. So Spark is going to transfer our data from the driver program to our worker nodes in 4 partitions. And, by calling _glom_ and then _collect_, we can find out how this data set was split in this 4 partitions. With transformation **coalesce**, we can reduce the number of partitions. This is used a lot after filtering, where you have reduced the size of your dataset and is not very useful to have a large number of partitions, but it´s better to reduce it to a more manageable number. Generally, it´s a local operation.

`sc.parallelize(range(10), 4).glom().collect()`

**Out[]:** [[0, 1], [2, 3], [4,5], [6, 7, 8, 9]]

`sc.parallelize(range(10),4).coalesce(2).glom().collect()`

**Out[]:** [[0, 1, 2, 3], [4, 5, 6, 7, 8, 9]]

**coalesce:** reduce the number of partitions

<p align="center"><img src="images/coalesce.png" width="450px"></p>

#

**Wide transformations**

- **Transformations of (K,V) pairs:** We have our input text file which is a dataset of where each element is a line of text then we run flatMap and we provide the function split_words that splits each line into the words. And finally,
we call the map transformation with the function create pair. And the output of this is a key value pair where the key is the word and the value is always one. Because then we want to sum all those ones to get the final counts for each word.

```
def create_pair(word):
  return (word,1)
```

`pairs_RDD=text_RDD.flatMap(split_words).map(create_pair)`

So, let´s collect, so that we can get the data back to the driver for inspection. And you see that the output here is the least of words, and each of them has the key one. So the operation I would like to show you is groupByKey. So what groupByKey does is it takes, as an input, an RDD of key value pairs. And, as an output, transfers all the data that has the same key, to the same partition.

`pairs_RDD.collect()`

**Out[]**:

[(u'A',1),

(u'long',1),

(u'time',1)

(u'ago',1)

(u'in',1)

(u'a',1)

(u'galaxy',1)

(u'far',1)

(u'far',1)

(u'away',1])

#

**groupByKey:** groupByKey takes as an input, a RDD of key value pairs. And, as an output, transfers all the data that has the same key to the same partition.

`groupbyKey`: (K,V) pairs => (K, iterable of all V)

(A,1)

(B,8)  =>  (A,[1,2,5])

(A,2)  =>  (B, [8])   

(A,5)

**Example (Directly in Spark):** `pairs_RDD.groupByKey().collect()`

<p align="center"><img src="images/outgbk1.png" width="450px"></p>

or

(Python Code)

```
for k,v pairs_RDD.groupByKey().collect():
  print "Key:", k, ",Values:", list(v)
```

<p align="center"><img src="images/outgbk2.png" width="450px"></p>

`groupbyKey`: (K,V) pairs => (K, iterable of all V)

<p align="center"><img src="images/gbkshuffle.png" width="450px"></p>

<p align="center"><img src="images/gbknarrowwide.png" width="450px"></p>

#

**reduceByKey(func):** We use this to go through all of our words and some of our word counts. The result of this reduceByKey operation is a pair of key and values, where for each key, we have a value which is the result of the reduction of all of the _Vs_ accross our dataset with these functions. So if we have a sum, it's going to be the sum of all our accounts across our data set.

`reduceByKey(func)`: (K,V) pairs => (K, result of reduction by func on all V)

#

**repartitions(NumPartitions):** similar to coalesce, shuffles all data to increase or decrease number of partitions to numPartitions.

#

**Shuffle:** Shuffle is a global redistribution of data and it has a high impact on performance. It´s one of the most performance heavy operations that you have in in your data analysis pipeline.

_And so how this works? So let's take a look at, as usual, our couple of nodes. So you see here that the key A is available on both nodes. And this list will transferred over the network from the second node to the first.
And How does this actually happen? So, the first step is that on the source side, the data are written to disk, and they are written to local disk, already separated. They're already ordered by the partition in which they're gonna be.
On the receiving side, on the final operation. And then, the data are requested over the network from the output nodes.
And this data is transferred from the source to the final destination._

<p align="center"><img src="images/shuffle.png" width="500px"></p>

_Know shuffle, avoid it_

- Which operations cause it?

- Is it necessary?

#

_Really need groupByKey?_

`groupbyKey`: (K,V) pairs => (K, iterable of all V)

If you plan to call **reduce** later in the pipeline, use **reduceByKey** instead.

<p align="center"><img src="images/gbkplusreduce.png" width="450px"></p>

<p align="center"><img src="images/rbk.png" width="450px"></p>

#

**Job scheduling, Actions, Caching and Shared Variables**

- **Directed Acyclic Graph (DAG) Scheduler:** It´s a collection of nodes, which are connected by edges. Those nodes are acyclic. If you start from a node and then you follow arrows down, you can never go back to the previous node.

<p align="center"><img src="images/dag.png" width="500px"></p>

<p align="center">**Track dependencies!** _(also known as lineage provenance)_</p>
