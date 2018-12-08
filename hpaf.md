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

    - **Cassandra:** distributed data management system.

  - **Querying**

    - **Pig:** Platform for analyzing large data sets in HDFS;

    - **Hive:** Query and manage large data sets;

    - **Impala:** High-performance, low-latency SQL querying of data in Hadoop file formats;

    - **Spark:** General processing engine for streaming, SQL, machine learning and graph processing.

  - **Machine Learning, Graph Processing**

    - **Giraph:** Iterative graph processing using Hadoop framework;

    - **Mahout:** Framework for machine learning applications using Hadoop and Spark;

    - **Spark:** General processing engine for streaming, SQL, machine learning and graph processing.
