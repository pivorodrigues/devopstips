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

  - Hadoopn can achieve reliability by replicating the cross multiple hosts, and therefore does not require any range storage on hosts.

  - The HTFS file system encodes the so-called secondary NameNode.

  - The secondary NameNode regularly connects to the primary NameNode and builds snapshots of the primary's NameNodes, the rapture information, and remembers which system saves to the local and the remote directories.

  - About every one of the Hadoop based system sits some version of a MapReduce engine.

  - The typical MapReduce engine will consist of a job tracker, to which client applications can submit MapReduce jobs, and this job tracker typically pushes work out to all the available task trackers, now it's in the cluster.

  - YARN was born as a need to enable a broader array of interaction patterns for data stored in HDFS beyond the MapReduce kind of framework.

  - Yarn enhances the power of the Hadoop compute cluster, without being limited by the map produce kind of framework.

  - The processing power and data centers continue to grow quickly, because the YARN research manager focuses exclusively on scheduling. He can manage those very large clusters quite quickly and easily.

  *YARN == MapReduce 2.0*

  <p align="center"><img src="images/hds-Architecture.jpg" width="500px"></p>

  - **The Hadoop Zoo**
