## <img src="images/acg.png" width="30px"> AWS Certified Solutions Architect - A Cloud Guru Exam Tips <img src="images/acg.png" width="30px">

## Chapter 1: Introduction - Exam Blue Print

- 130 minutes in lenght

- 60 questions _(this can change)_

- Multiple choice

- Results are between 100-1000 with a passing score of 720

- Aim for 70%

- Qualification is valid for 3 years

- Scenario based questions


## Chapter 2: AWS - 10.000 Foot Overview (Exam Tips) <img src="images/amazon-web-services-logo.png" width="30px">

**Understand the difference between a Region, an Availability Zone (AZ) and an Edge Location**

- A **Region** is a physical location in the world which consists of two or more Availability Zones (AZ's).

- An **Availability Zone** is one or more discrete data centers, each with redundant power, networking and connectivity, housed in separate facilities.

- **Edge Locations** are endpoints for AWS which are used for caching content. Typically this consists of CloudFront, Amazon's Content Delivery Network (CDN). *PS: There are many more edge locations than regions*

#

**What Do I Need To Know To Pass My Solutions Architect Exam?**

  - **Security, Identity & Compliance**

    - [IAM](https://github.com/pivorodrigues/devopstips/blob/master/acsa.md#chapter-3-identity-access-management--s3-)

  - **Storage**

    - [S3](https://github.com/pivorodrigues/devopstips/blob/master/acsa.md#chapter-3-identity-access-management--s3-)

  - **Compute**

    - [EC2](https://github.com/pivorodrigues/devopstips/blob/master/acsa.md#chapter-4-ec2-)

    - Lambda

  - **Databases**

    - RDS

    - DynamoDB

    - Redshift

  - **Network & Content Delivery**

    - Route 53


## Chapter 3: Identity Access Management & S3 <img src="images/s3logo.png" width="30px">

**Identity Access Management 101** [[FAQ](https://aws.amazon.com/pt/iam/faqs/)]

- Identity Access Management consists of the following:

	- Users

	- Groups

	- Roles

	- Policies

- **IAM is universal.** It does not apply to regions at this time.

- The **"root account"** is simply the account created when first setup your AWS account. It has complete Admin access.

- New users have **NO permissions** when first created.

- New Users are assigned **Access Key ID** & **Secret Access Keys** when first created.

- **These are not the same as password**. You cannot use the Access Key ID & Secret Access via to login into the console. You can use this to access AWS via the APIs and Command Line, however.

- You only get to view the Access Key ID and Secret Access Key once. If you lose them, you have to **regenerate** them. So, save them in a secure location.

- Always setup **Multifactor Authentication** on your root account.

- You can create and customise your own password rotation policies.

_Resources:_

  - [AWS DOC: Create a Billing Alarm](https://docs.aws.amazon.com/pt_br/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html)

  - [AWS DOC: Create a Free Tier Billing Alert](https://aws.amazon.com/pt/about-aws/whats-new/2017/12/aws-free-tier-usage-alerts-automatically-notify-you-when-you-are-forecasted-to-exceed-your-aws-service-usage-limits/)

#

**S3 (Simple Storage Service) 101** [[FAQ](https://aws.amazon.com/pt/s3/faqs/)]

- Remember that S3 is **Object-based**: i.e. allows you to upload files.

- Files can be from 0 Bytes to 5 TB.

- There is unlimited storage.

- Files are stored in Buckets (It´s basically a folder in the cloud).

- **S3 is a universal namespace**. That is, names must be unique globally.

- Bucket URL Examples: https://acloudguru.s3.amazonaws.com/

  - https://acloudguru.eu-west-1.amazonaws.com/

- **Not suitable to install an operating system on or databases**.

- Successful uploads will generate a HTTP 200 status code.

- By default, all newly created buckets are **PRIVATE**. _(Review this information)_ You can setup access control to your buckets using:

	- Bucket Policies

	- Access Control Lists

- S3 buckets can be configured to create access logs which log all requests made to the S3 bucket. This can be sent to another bucket and even another bucket in another account.

- You can turn on **MFA Delete**.

- **The Key Fundamentals of S3 Are:**

  - Key (This is simply the name of the object).

  - Value (This is simply the data and is made up of a sequence of bytes).

  - Version ID (Important for versioning).

  - Metadata (Data about data you are storing).

  - Subresources:

    - Access Control Lists

    - Torrent

- Read after Write consistency for PUTS of new Objects.

- Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate).

- **1. S3 Standard**: 99.99% availability, 99.999999999% durability, stored redundantly across multiple devices in multiple facilities, and is designed to sustain the loss of 2 facilities concurrently.

- **2. S3 - IA** _(Infrequently Accessed)_: For data that is accessed less frequently, but requires rapid access when needed. Lower fee than S3, but you are charged a retrieval fee.

- **3. S3 One Zone - IA**: For where you want a lower-cost option for Infrequently accessed data, but do not require the multiple Availability Zone data resilience.

- **4. S3 - Intelligent Tiering**: Designed to optimize costs by automatically moving data to the most cost-effective access tier, without performance impact or operational overhead.

- **S3 Glacier**: S3 Glacier is a secure, durable, and low-cost storage class for data archiving. Retrieval time configurable from minutes to hours.

- **S3 Glacier Deep Archive**: S3 Glacier Deep Archive is Amazon S3's lowest-cost storage class where a retrieval time of 12 hours is acceptable.

<p align="center"><img src="images/aws-s3-comparison.png" width="500px"></p>

#

**S3 Bucket Lab**

- **Buckets are a universal name space**

- Upload an object to S3 receive a HTTP 200 Code

- S3, S3 - IA, S3 IA (One Zone), Glacier

- Control access to buckets using either **bucket ACL** or using **Bucket Policies**

#

**S3 Security and Encryption**

- Encryption In Transit is achieved by:

	- SSL/TLS

- Encryption at Rest (Server Side) is achieved by:

	- S3 Managed Keys - SSE-S3

	- AWS Key Management Service, Managed Keys (SSE-KMS)

	- Server Side Encryption with Customer Provided Keys (SSE-C)

- Client Side Encryption	 

#

**S3 Versioning**

- Store all versions of an object (including all writes and even if you delete an object).

- Great backup tool.

- Once enabled, Versioning cannot be disabled, only suspended.

- Integrates with Lifecycles rules.

- Versioning's MFA Delete capability, which uses multi-factor authentication, can be used to provide an additional layer of security.

#

**S3 Lifecycle Management, S3 IA and Glacier**

- Automates moving your objects between the different storage tiers.

- Can be used in conjunction with versioning.

- Can be applied to current versions and previous versions.

#

**AWS Organizations & Consolidate Billing**

- **Some best practices with AWS Organizations:**

  - Always enable multi-factor authentication.

  - Always use a strong and complex password on root account.

  - Paying account should be used for billing purposes only. Do not deploy resources into the paying account.

  - Enable/disable AWS services using _Service Control Policies (SCP)_ either on OU (Organizational Unit) or on individual accounts.

#

**Sharing S3 Buckets Across Accounts**

- **3 different ways to share S3 buckets across accounts:**

  - Using bucket policies and IAM (applies across the entire bucket). Programmatic Access Only.

  - Using bucket ACLs and IAM (individual objects). Programmatic Access Only.

  - Cross-Account IAM Roles. Programmatic and Console access.

#

**Cross Region Replication**

- Versioning must be enabled on both the source and destination buckets.

- Files in an existing bucket are not replicated automatically.

- All subsequent updated files will be replicated automatically.

- Delete markers are not replicated.

- Deleting individual versions or delete markers will not be replicated.

- Understand what Cross Replication is at a high level.

#

**S3 Transfer Acceleration**

- S3 Transfer Acceleration utilises the Cloudfront Edge Network to accelerate your uploads to S3. Instead of uploading directly to your S3 bucket, you can use a distinct URL to upload directly to an edge location which will then transfer that file to S3. You will get a distinct URL to upload to: acloudguru.s3-accelerate.amazonaws.com _(example)_.

<p align="center"><img src="images/s3ta.png" width="500px"></p>

- [Amazon S3 Transfer Acceleration Speed Comparison](https://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html)

#

**AWS DataSync [SAA-C02]**

<p align="center"><img src="images/aws-datasync.png" width="500px"></p>

- Used to move **large amount** of data from on-premises to AWS.

- Used with **NFS**-compatible and **SMB**-compatible file systems.

- **Replication** can be done hourly, daily, or weekly.

- Install the **DataSync agent** to start the replication.

- Can be used to replicate **EFS** to **EFS**.

#

**CloudFront**

- **Edge Location** - This is the location where content will be cached. This is separate to an AWS Region/AZ.

- **Origin** - This is the origin of all the files that the CDN will distribute. This can be either an S3 bucket, an EC2 instance, an Elastic Load Balancer, or Route 53.

- **Distribution** - This is the name given the CDN which consists of a collection of Edge Locations.

- **Web Distribution** - Typically used for Websites.

- **RTMP** - Used for Media Streaming.

- Edge Locations are not just READ only - you can write to them too. (ie put an object on to them.)

- Objects are cached for the life of the **TTL (Time To Live)**.

- You can clear cached objects, **but you will be charged**.

#

**CloudFront Signed URLs and Cookies**

<p align="center"><img src="images/aws-cf-signedurl.png" width="500px"></p>

- Use signed **URL/Cookies** when you want to secure content so that only the people you authorize are able to access it.

- A signed URL is for individual files. **1 file = 1 URL**.

- A signed cookie is for multiple files. **1 cookie = multiple files**.

- If your origin is EC2, then use CloudFront. If you origin is S3, use S3 signed URLs.

#

**Snowball**

- Understand what Snowball is.

- Understand what Snowball Can.

- Import to S3.

- Export from S3

#

**Storage Gateway**

- **File Gateway**

	- File Gateway - For flat files, stored directly on S3.

- **Volume Gateway**

	- **Stored Volumes** - Entire Dataset is store on site and is asynchronously backed to S3.

	- **Cached Volumes** - Entire Dataset is stored on S3 and the most frequently accessed data is cached on site.

- **Gateway Virtual Tape Library**

#

**Athena vs Macie**

- **Athena Exam Tips:** Remember what Athena is and what it allows you to do.

  - Athena is an interactive query service.

  - It allows you to query data located in S3 using standard SQL.

  - Serverless

  - Commonly used to analyze log data stored in S3.

- **Macie Exam Tips:** Remember what Macie is and what it allows you to do.

  - Macie uses AI to analyze data in S3 and helps identify PII (Personal Identity Information).

  - Can also be used to analyze Cloud Trail logs for suspicious API activity.

  - Includes Dashboards, Reports and Alerting.

  - Great for PCI-DSS compliance and preventing ID theft.

#

**S3 Lock Policies and Glacier Vault Lock**

- **S3 Lock Policies**

  - Use **S3 Object Lock** to store objects using a write once, read many (WORM) model.

  - Object locks can be individual objects or **applied across the bucket** as a whole.

  - Object locks come in two modes: **governance mode** and **compliance mode**

    - With **governance mode**, users can't overwrite or delete an object version or alter its lock settings unless they have special permissions.

    - With **compliance mode**, a protected object version can't be overwritten or deleted by any user, including the root user in your AWS account.

- **Glacier Vault Lock**

  - **S3 Glacier Vault Lock** allows you to easily deploy and enforce compliance controls for individual S3 Glacier vaults with a Vault Lock policy. You can **specify controls such as WORM in a Vault Lock policy and lock the policy from future edits**. Once locked, the policy can no longer be changed.    

#

**S3 Performance**

- **Prefixes**

  - _mybucketname/folder1/subfolder1/myfile.jpg_ > /folder1/subfolder1

  - You can also achieve a high number of requests: **3500 PUT/COPY/POST/DELETE** and **5.500 GET/HEAD** requests per second por fix

  - You can get better performance by spreading your reads across **different prefixes**. For example, if you are using **two prefixes**, you can achieve **11.000 requests per second**.

- **SSE-KMS**

  - If you are using SS3-KMS to encrypte your objects in S3, you must keep in mind the KMS limits.

    - Region-Specific, however, it's either **5.500**, **10.000**, or 30.000 requests per second.

    - Currently, you **cannot** request a quota increase for KMS.

    - Uploading/download will count towrd the KMS quota.  

- **Multipart Uploads**

  - Use **multipart uploads** to increse performance when **uploading files** to S3.

  - Should be used for any files **over 100 MB** and must be used for any file over 5G.

  - Use **s3 byte-range fetches** to increase performance when **downloading files** to S3.   

#

**S3 Select and Glacier Select**

<p align="center"><img src="images/aws-s3-select.png" width="500px"></p>

- Remember that S3 Select is used to **retrieve only a subset of data** from an object by using simple SQL expressions.

- Get data by **rows or colums** using simple SQL expressions.

- Save money on **data transfer** and increase speed.

#

## Chapter 4: EC2 <img src="images/ec2.png" width="30px">

**EC2 (Elastic Compute Cloud) 101** [[FAQ](https://aws.amazon.com/pt/ec2/faqs/)]

- **EC2 Pricing Policies:**

  - **1. On Demand**: Allows you to pay a fixed rate by the hour (or by the second) with no commitment.

  - **2. Reserved**: Provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. Contract terms are 1 Year or 3 Year terms.

  - **3. Spot**: Enables you to bid whatever price you want for instance capacity, providing for even greater savings if your applications have flexible start and end times.

  - **4. Dedicated Hosts**: Physical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licences.

  If the Spot instance is terminated by Amazon EC2, you will not be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for any hour in which the instance ran.

- **EC2 Family Instance Types - Mnemonic**

  - **F** - For FPGA

  - **I** - For IOPS

  - **G** - Graphics

  - **H** - High Disk Throughput

  - **T** - Cheap general purpose (think T2 Micro)

  - **D** - For Density

  - **R** - For RAM

  - **M** - Main choice for general purpose apps

  - **C** - For Compute

  - **P** - Graphics (think Pics)

  - **X** - Extreme Memory

  - **Z** - Extreme Memory AND CPU

  - **A** - Arm-based workloads

  - **U** - Bare Metal

#

**EC2 Labs - Exam and Use Tips**

- **How to login (SSH) in the EC2 instance?**

  - Create a new key in the moment of instance creation, or use an existing key

  - Get the instance's public IP address

  - Execute the command: `$ ssh ec2-user@<public-IP-address> -i <keyname>.pem`

- Termination Protection is **turned off** by default, you must turn it on.

- On an EBS-Backed instance, the **default action is for the root EBS volume to be deleted** when the instance is terminated.

- EBS **Root** Volumes of your DEFAULT AMI´s **CAN** be encrypted. You can also use a third party tool (such as bit locker, etc) to encrypt the root volume, or this can be done when creating AMI´s (lab to follow) in the AWS console or using the API.

- Additional volumes can be encrypted.

#

**Security Groups Lab**

- All Inbound traffic is blocked by default.

- All Outbound traffic is allowed.

- Changes to Security Groups take effect immediately.

- You can have any number of EC2 instances within a security group.

- You can have multiple security groups attached to EC2 instances.

- Security Groups are **STATEFUL**.

- If you create an inbound rule allowing traffic in, that traffic is automatically allowed back out again.

- You cannot block specific IP addresses using Security Groups, instead use Network Access Control Lists.

- You can specify allow rules, but not deny rules.

#

**EBS (Elastic Block Storage) 101**

<p align="center"><img src="images/aws-ebs-types.png" width="500px"></p>

- Termination Protection is **turned off** by default, you must turn it on.

- On an EBS-backed instance, the **default action is for the root EBS volume to be deleted** when the instance is terminated.

- EBS Root Volume of your DEFAULT AMI's **CAN** be encrypted. You can also use a third party tool (such as a bit locker, etc) to encrypt the root volume, or this can be done when creating AMI's (remember the lab) in the AWS console or using the API.

- Aditional volumes can be encrypted.

#

**EBS Snapshots**

- Volumes exist on EBS. Think of EBS as a virtual hard disk.

- Snapshots exist on S3. Think of snapshots as a photograph of the disk.

- Snapshots are point in time copies of Volumes.

- Snapshots are incremental - this means that only the blocks that have changed since your last snapshot are moved to S3.

- If this is your first snapshot, it may take some time to create.

- To create a snapshot for Amazon EBS volumes that serve as root devices, you should stop the instance before taking the snapshot.

- However you can take a snap while the instance is running.

- You can create AMI´s _(Amazon Machine Images)_ from both Volumes and Snapshots.

- You can change EBS volume sizes on the fly, including changing the size and storage type.

- Volumes will ALWAYS be in the same availability zone as the EC2 instance.

#

**Migrating EBS**

- To move an EC2 volume from one AZ to another, take a snapshot of it, create an AMI from the snapshot and then use the AMI to launch the EC2 instance in a new AZ.

- To move an EC2 volume from one region to another, take a snapshot of it, create an AMI from the snapshot and then copy the AMI from one region to the other. Then use the copied AMI to launch the new EC2 instance in the new region.

#

**EBS Encryption**

- Snapshots of encrypted volumes are encrypted automatically.

- Volumes restored from encrypted snapshots are encrypted automatically.

- You can share snapshots, but only if they are **unencrypted**.

- These snapshots can be shared with other AWS accounts or made public.

#

**Volumes and snapshots**

- Root Devices can now be encrypted. If you have an unencrypted root device volume that needs to be encrypted do the following;

  - Create a Snapshot of the unencrypted root device volume.

  - Create a copy of the Snapshot and select the encrypt option.

  - Create an AMI from the encrypted Snapshot.

  - Use that AMI to launch new encrypted instances.

#

**EBS vs Instance Store**

- Instance Store Volumes are sometimes called Ephemeral Storage.

- Instance store volumes cannot be stopped. if the underlying host fails, you will lose your data.

- EBS Backed instances can be stopped. You will not lose the data on this instance if it is stopped.

- You can reboot both, you will not lose your data.

- By default, both ROOT volumes will be deleted on termination. However, with EBS volumes, you can tell AWS to keep the root device volume.

#

**Encrypting Root Device Volumes**

- Create a Snapshot of the unencrypted root device volume.

- Create a copy of the Snapshot and select the encrypt option.

- Create an AMI from the encrypted Snapshot.

- Use that AMI to launch new encrypted instances.

#

**Enhanced Networking**

In the exam you will be given different scenarios and you will be asked to choose whether you should use an ENI, EN or EFA.

- **ENI (Elastic Network Interfaces)**

  - For basic networking. Perhaps you need a separate management network to your production network or a separate logging network and you need to do this at low cost. In this scenario use multiple ENIs for each network.

- **EN (Enhanced Network)**

  - For when you need speeds between 10Gbps and 100Gbps. Anywhere you need reliable, high throughput.

- **EFA (Elastic Fabric Adaptor)**

  - For when you need to accelerate High Performance Computing (HPC) and machine learning applications _or_ if you need to do an OS-Bypass. If you see a scenario question mentioning HPC or ML and asking what network adaptor you want, choose EFA.

#

**Spot instances and Spot Fleets**

- Spot instances save up to **90%** of the cost of On-Demand Instances.

- Useful for any type of computing where you don't need **persistent storage**.

- You can block Spot Instances from terminating by using **Spot Block**.

- A Spot Fleet is a collection of Spot Instances and, optionally, On-Demand Instances.

#

**EC2 Hibernate**

- **EC2 Hibernate** preserves the in-memory RAM on persistent storage (EBS).

- Much faster to boot up because you **don't need to reload the operating system**.

- Instance RAM must be less than **150 GB**.

- Instance families include C3, C4, C5, M3, M4, M5, R3, R4 and R5.

- Available for Windows, Amazon Linux 2 AMI, and Ubuntu.

- Instances can't be hibernate for more than **60 days**.

- Available for **On-demand instances** and **Reserved Instances**

#

**Cloudwatch 101**

- Cloudwatch is used for monitoring performance.

- CloudWatch can monitor most of AWS as well as your applications that run on AWS.

- CloudWatch with EC2 will monitor events **every 5 minutes by default**.

- You can have 1 minute intervals by turning on detailed monitoring.

- You can create CloudWatch alarms with trigger notifications.

- Cloudwatch is all about performance. CloudTrail is all about auditing.

#

**Cloudwatch Lab**

- Standard monitoring = 5 minutes.

- Detailed monitoring = 1 minute.

  - _What can I do with Cloudwatch?_

    - Dashboards: Creates awesome dashboards to see what is happening with your AWS environment.

    - Alarms - Allows you to set Alarms that notify you when particular thresholds are hit.

    - Events - Cloudwatch events helps you to respond to state changes in your AWS recourses.

    - Logs - Cloudwatch logs helps you to aggregate, monitor and store logs.

- CloudWatch monitors performance.

- CloudTrail monitors API calls in the AWS platform.

#

**AWS Command Line (CLI) Lab**

- You can interact with AWS from anywhere in the world just by using the command line (CLI).

- You will need to set up access in IAM.

- Commands themselves are not in the exam, but some basic commands will be useful to know for real life.

#

**Identity Access Management Roles LAB**

- Roles are more secure than storing your access key and secret access key on individual EC2 instances.

- Roles are easier to manage.

- Roles can be assigned to an EC2 instance after it is created using both the console and command line.

- Roles are universal - you can use them in any region.

#

**Instance Metadata**

- Command to see the content of bootstrap script inside our EC2 instance:

  - _$ curl "http://169.254.169.254/latest/user-data"_

  - Results:

    ```
      #!/bin/bash

      sudo su -

      yum update -y

      yum install httpd -y

      systemctl start httpd

      chkconfig httpd on

      cd /var/www/html

      echo '<html><h1>Hello Cloud Gurus</h1></html>' > index.html

      aws s3 mb s3://pivorodrigueskjuuenfiuiehjeiuifjheie87765

      aws s3 cp index.html s3://pivorodrigueskjuuenfiuiehjeiuifjheie87765

    ```

- Command to get information about an EC2 instance:

  - _$ curl "http://169.254.169.254/latest/meta-data"_

  - Results:

    ```
      ami-id
      ami-launch-index
      ami-manifest-path
      block-device-mapping/
      events/
      hostname
      iam/
      identity-credentials/
      instance-action
      instance-id
      instance-type
      local-hostname
      local-ipv4
      mac
      metrics/
      network/
      placement/
      profile
      public-hostname
      public-ipv4
      public-keys/
      reservation-id
      security-groups
      services/
    ```

  - _$ curl "http://169.254.169.254/latest/meta-data/local-ipv4"_

    `172.31.93.65`

#

**EFS - Elastic File System**

- Supports the Network File System version 4 (NFSv4) protocol.

- You only pay for the storage you use (no pre-provisioning required).

- Can scale up to the petabytes.

- Can support thousands of concurrent NFS connections.

- Data is stored across multiple AZ's within a region.

- Read After Write consistency.

#

**Amazon FSx for Windows & Amazon FSx for Lustre**

In the exam you'll be given different scenarios and asked to choose whether you should use an EFS, FSx for Windows or FSx for Lustre.

- **EFS**

  - When you need distributed, highly resilient storage for Linux instances and Linux-based applications.

- **Amazon FSx for Windows**

  - When you need centralized storage for Windows-based applications such as Sharepoint, Microsoft SQL Server, Workspaces, IIS Web Server or any other native Microsoft Application.

- **Amazon FSx for Lustre**

  - When you need high-speed, high-capacity distributed storage. This will be for applications that do High Performance Compute (HPC), financial modelling etc. Remember that FSx for Lustre can store data directly on S3.    

#

**Placement Groups**

- **Three Types of Placement Groups**

  - _Clustered Placement Group_

    - Low Network Latency / High Network Throughput

  - _Spread Placement Group_

    - Individual Critical EC2 instances

  - _Partitioned Placement Group_

    - Multiple EC2 instances HDFS, HBase and Cassandra

- A clustered placement group can´t span multiple Availability Zones.

- A spread placement and partitioned group can.

- The name you specify for a placement group must be unique within your AWS account.

- Only certain types of instances can be launched in a placement group (Compute Optimized, GPU, Memory Optimized, Storage Optimized).

- AWS recommend homogenous instances within clustered placement groups.

- You can´t merge placement groups.

- You can´t move an existing instance into a placement group. You can create an AMI from your existing instance, and then launch a new instance from the AMI into a placement group.

#

**HPC (High Performance Compute) on AWS**

- We can achieve HPC on AWS through:

  - **Data Transfer**

    - Snowball, Snowmobile (**terabytes/petabytes worth of data**)

    - AWS DataSync to store on S3, EFS, FSx for Windows, etc.

    - Direct Connect

  - **Compute and Networking**

    - EC2 instances that are **GPU** or **CPU** optimized.

    - **EC2 Fleets** (Spot instances and Spot Fleets).

    - Placement Groups (cluster placement groups).

    - Enhanced networking single root I/O virtualization (**SR-IOV**).

    - Elastic Network Adapters or **Intel 82599 Virtual Function** (VF) interface.

    - Elastic Fabric Adapters.

  - **Storage**

    - **Instance-attached storage:**

      - **EBS:** Scale up to 64.000 IOPS with Provisioned IOPS (PIOPS).

      - **Instance Store:** Scale to millions of IOPS; low latency

    - **Network storage:**

      - **Amazon S3:** Distributed object-based storage; not a file system.

      - **Amazon EFS:** Scale IOPS based on total size, or use Provisioned IOPS.

      - **Amazon FSx for Lustre:** HPC-Optimized distributed file system; millions of IOPS, which is also backed by S3.

  - **Orchestration and Automation**

    - AWS Batch

    - AWS ParallelCluster   

#

**Amazon WAF (Web Application Firewall)**

A its most basic level, AWS WAF allows 3 different behaviours:

  1. Allow all requests except the ones you specify

  2. Block all requests except the ones you specify

  3. Count the requests that match the properties you specify

Extra protection against web attacks using conditions you specify. You can define conditions by using characteristics of web requests such as:

  - IP addresses that requests originate from.

  - Country that requests originate from.

  - Values in request headers.

  - Strings that appear in requests, either specific strings or string that match regular expression (regex) patterns.

  - Lenght of requests.

  - Presence of SQL code that is likely to be malicious (known as SQL injection).

  - Presence of a script that is likely to be malicious (know as cross-sites-scripting)

Obs: In the exam you will be given different scenarios and you will be asked how to block malicious IP addresses.


## Chapter 5: Databases on AWS <img src="images/aws-database.png" width="30px">

**Databases 101**

- **RDS (OLTP - Online Transaction Processing)(Relational Solution)**

  - SQL Server

  - MySQL

  - PostgreSQL

  - Oracle

  - Aurora

  - MariaDB

- **DynamoDB**

  - NoSQL Database Solution

- **Redshift (OLAP - Online Analytics Processing)**

  - Datawarehouse Solution

  - Used for Business Intelligence or Data Warehousing

- **Elasticache**

  - Memcache

  - Redis

  - Caching Solution

  - Used to speed up performance of existing databases (frequent identical queries)

#

**Databases 101 - Relational Databases**

- Remember the following points:

  - RDS runs on virtual machines

  - You cannot log in to these operating systems however

  - Patching of the RDS Operating System and DB is Amazon's responsibility

  - RDS is NOT Serverless

  - Aurora Serverless IS Serverless

#

**RDS -  Backups, Multi-AZ and Read Replicas**

**Backups**

- There are two different types of Backups for RDS:

  - Automated Backups

  - Database Snapshots

**Read Replicas**

- Can be Multi-AZ

- Used to increase performance

- Must have backups turned on

- Can be in different regions

- Can be MySQL, PostgreSQL, MariaDB, Oracle, Aurora

- MSSQL is now available to be used with Read Replicas

- Can be promoted to master, this will break the Read Replica

**Multi-AZ**

- Used for Data Replication

- You can force a failover from one AZ to another by rebooting the RDS instance

Encryption at rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB and Aurora. Encryption is done using the AWS Key Management Service (KMS). Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas and snapshots.

#

**DynamoDB**

- **The basics of DynamoDB** are as follows:

  - Stored on SSD Storage

  - Spread across 3 geographically distinct data centers

  - Eventual Consistent Reads (Default)

  - Strongly Consistent Reads

#

**Advanced DynamoDB**

- **DynamoDB Accelerator (DAX)**

  - Fully managed, highly available, in-memory cache.

  - 10x performance improvement.

  - Reduces request time from milliseconds to **microseconds** - even under load.

  - No need for developers to manage caching logic.

  - Compatible with DynamoDB API calls.

<p align="center"><img src="images/aws-dax.png" width="600px"></p>

- **Transactions**

  - Multiple "all-or-nothing" operations.

  - Financial transactions.

  - Fulfilling orders.

  - Two underlying reads or writes - prepare/commit.

  - Up to 25 items or 4 MB of data.

- **On-Demand Capacity**

  - **Pay-per-use** pricing.

  - Balance cost and performance.

  - No minimum capacity.

  - No charge for read/write - only storage and backups.

  - **Pay more per request** than with provisioned capacity.

  - Use for new products launches.

- **On-Demand Backup and Restore**

  - Full backups.

  - Zero impact on table performance or availability.

  - Consistent within seconds and **retained until deleted**.

  - Operates within same region as the source table.

- **Point-in-Time Recovery**

  - Protects against accidental writes or deletes.

  - Restore to any point in the last **35 days**.

  - Incremental backups.

  - Not enabled by default.

  - Latest restorable: **five minutes** in the past.

- **Streams**

  - Time-ordered sequence of item-level changes in a table.

  - Stored for **24 hours**.

  - Inserts, updates, and deletes.

  - Combine with Lambda functions for functionality like stored procedures. 

  <p align="center"><img src="images/aws-streams.png" width="600px"></p>

- **Global Tables**

  - **Managed Multi-Master, Multi-Region Replication**

    - Globally.

    - Based on DynamoDB streams.

    - Multi-Region redundancy for DR or HA.

    - No application rewrites.

    - Replication latency under **on second**.

#

**Database Migration Service (DMS)**

  - DMS allows you to **migrate databases** from one source to AWS.

  - You can do **homogeneous** migrations (same DB engines) or **heterogeneous** migrations.

  - The source can either be on-premises, or inside AWS itself or another cloud provider such as Azure.

  - If you do a heterogeneous migration, you will need the **AWS Schema Conversion Tool** (SCT). 

<p align="center"><img src="images/aws-dms.png" width="600px"></p>

<p align="center"><img src="images/aws-sct.png" width="600px"></p>

#

**Caching strategies on AWS**

<p align="center"><img src="images/aws-cache-architecture.png" width="600px"></p>

- Caching is a balancing between **up-to-date**, **accurate information** and **latency**. We can use the following services to **cache on AWS**:

  - CloudFront;

  - API Gateway;

  - Elasticache - **Memcached** and **Redis**;

  - DynamoDB Accelerator; 

#

**EMR Overview**

- EMR is used for **big data processing**.

- Consists of a **master node**, a **core node**, and (optionally) a **task node**.

- By default, log data is **stored on the master node**.

- You can configure replication to S3 on **five-minutes intervals for all log data from the master node**; however, this can only be configured when creating the cluster for the first time.

#

- **Security**

  - Encryption at rest using **KMS**.

  - Site-to-site **VPN**.

  - Direct Connect (DX).

  - IAM policies and roles.

  - Fine-grained access.

  - CloudWatch and CloudTrail.

  - VPC Endpoints.

#

**Redshift**

- Redshift is a Data Warehouse used for business intelligence

- Available in only 1 AZ

- **Redshift Backups:**

  - Enabled by default with a 1 day retention period

  - Maximum retention period is 35 days

  - Redshift always attempts to maintain at least three copies of your data (the original and replica on the compute nodes and a backup in Amazon S3)

  - Redshift can also asynchronously replicate your snapshots to S3 in another region for disaster recovery

#

**Amazon Aurora**

- 2 copies of your data is contained in each availability zone, with minimum of 3 availability zones. 6 copies of your data.

- You can share Aurora Snapshots with other AWS accounts.

- 3 types of replicas available. Aurora replicas, MySQL replicas and PostgresSQL replicas. Automated failover is only available with Aurora Replicas.

- Aurora has automated backups turned on by default. You can also take snapshots with Aurora. You can share these snapshots with other AWS accounts.

- Use Aurora Serverless if you want a simple, cost-effective option for infrequent, intermittent, or unpredictable workloads.

<p align="center"><img src="images/aws-replicas-comparison.png" width="750px"></p>

#

**Elasticache**

- Use Elasticache to increase database and web application performance.

- Two flavors: Memcached and Redis.

- Redis is Multi-AZ.

- You can do backups and restore of Redis


## Chapter 6: Advanced IAM <img src="images/aws-iam.png" width="30px">

**AWS Directory Service**

- **What is AWS Directory Service?**

  - Family of managed services.

  - Connect AWS resources with on-premises AD.

  - Standalone directory in the cloud.

  - Use existing corporate credentials.

  - SSO to any domain-joined EC2 instance.

- **What is Active Directory?**

  - On-premises directory service.

  - Hierarchical database of users, groups, computers - **trees** and **forests**.

  - Group policies.

  - LDAP and DNS.

  - Kerberos, LDAP, and NTLM authentication.

  - Highly available.

- **AWS Managed Microsoft AD**

  - AD domain controllers (DCs) running Windows Server.

  - Reachable by applications in your VPC.

  - Add DCs for HA and performance.

  - Exclusive access to DCs.

  - Extend existing AD to on-premises using **AD Trust**.

  - **AWS**

    - Multi-AZ deployment.

    - Patch, monitor, recover.

    - Instance rotation.

    - Snapshot and restore.

  - **Customer**

    - Users, groups, GPOs.

    - Standard AD tools.

    - Scale out DCs.

    - Trusts (resource forest).

    - Certificate authorities (LDAPS).

    - Federation.

  <p align="center"><img src="images/aws-managed-ad.png" width="500px"></p>

- **Simple AD**

  - Standalone managed directory.

  - Basic AD features.

  - Small: <= 500; Large <= users.

  - Easier to manage EC2.

  - Linux workloads that need LDAP.

  - Does not supporte **trusts** (can't join on-premises AD).

- **AD Connector**

  - Directory gateway (proxy) for on-premises AD.

  - Avoid caching information in the cloud.

  - Allow on-premises users to log in to AWS using AD.

  - Join EC2 instances tou your existing AD domain.

  - Scale across multiple AD connectors.

- **Cloud Directory**

  - Directory-based store for developers.

  - Multiple hierarchies with hundreds of millions of objects.

  - Use cases: org charts, course catalogs, device registries.

  - Fully managed service.

- **Amazon Cognito User Pools**

  - Managed user directory for SaaS applications.

  - Sign-up and sign-in for web mobile.

  - Works with **social media** identities.

- **AD vs Non-AD Compatible Services**

  - **AD Compatible**

    - Managed Microsoft AD (a.k.a., Directory Service for Microsoft Active Directory).

    - AD Connector.

    - Simple AD.

  - **Not AD Compatible**

    - Cloud Directory

    - Cognito user pools
#

**Evaluating IAM Policies**

- Not explicit allowed == **implicit denied**.

- Explicit deny > Everything else.

- Only attached policies have effect.

- AWS **joins** all applicable policies.

- AWS-managed vs. customer-managed.

- **Permission boundaries:**

  - Used to **delegate** administration to other users.

  - Prevent **privilege scalation** or **unnecessarily broad permissions**.

  - Control **maximum** permissions an IAM policy can grant.

  - Use cases:

    - Developers creating roles for Lambda functions;

    - Application owners creating roles for EC2 instances;

    - Admins creating ad hoc users.


## Chapter 7: Route 53 <img src="images/aws-route53-logo.png" width="30px">

- _How to discover a DNS name server record:_ `$ nslookup -type=ns globo.com`

- _How to discover the TTL of a server:_ `$ dig +nocmd +noall +answer +ttlid a google.com`

**Route 53**

- ELBs do not have pre-defined IPv4 addresses; you resolve to them using a DNS name

- Understand the difference between an **Alias Record** and a **CNAME** [[Medium](https://medium.com/@Constellix/whats-the-difference-between-aname-aaaa-a-and-cname-records-656c1ca2cb73)]

- Given the choice, always choose an **Alias Record** over a **CNAME**

- **Common DNS Types:**

  - SOA Records

  - NS Records

  - A Records

  - CNAMES

  - MX Records

  - PTR Records

#

**Register a Domain Name - Lab**

- You can buy domain names directly with AWS

- It can take up to 3 days to register depending on the circumstances

#

**Route 53 Routing Policies Available on AWS**

- Simple Routing

- Weighted Routing

- Latency-based Routing

- Failover Routing

- Geolocation Routing

- Geoproximity Routing (Traffic Flow Only)

- Multivalue Answer Routing

#

**Simple Routing Policy - Lab**

- If you choose the simple routing policy, you can only have one record with multiple IP addresses. If you specify multiple values in a record, Route53 returns all values to the user in a random order.

#

**Weighted Routing Policy - Lab**

<p align="center"><img src="images/aws-wighted-routing.png" width="750px"></p>

**Health Checks**

- You can set health checks on individual record sets

- If a record set fails, a health check it will be removed from Route 53 until it passes the health check

- You can set SNS notifications to alert you if a health check is failed

#

**Latency-Based Routing**

<p align="center"><img src="images/aws-latency-routing.png" width="750px"></p>

#

**Failover Routing Policy**

<p align="center"><img src="images/aws-failover-routing.png" width="750px"></p>

#

**Geolocation Routing Policy**

<p align="center"><img src="images/aws-geolocation-routing.png" width="750px"></p>

#

**Geoproximity Routing (Traffic Flow Only)**

- Geoproximity routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources. You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as Bias. A Bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.

**To use geoproximity routing, you must use Route 53 traffic flow.**

#

**Multivalue Answer Policy**

<p align="center"><img src="images/aws-multivalue-routing.png" width="750px"></p>

## Chapter 7: VPCs <img src="images/aws-vpc.png" width="30px">

**Introduction to VPCs**

[Interactive IP Address and CIDR Range Visualizer](https://cidr.xyz/)

_Note:_ Before you go and do your exam, you should be able to build out your own VPC from memory. If you can do that, then you'll be able to pass the Certified Solutions Architect Associate Exam.

_Private IP Address Ranges:_

  ```
    10.0.0.0 - 10.255.255.255 (10/8 prefix)
    172.16.0.0 - 172.31.255.255 (172.16/12 prefix)
    192.168.0.0 - 192.168.255.255 (192.168/16 prefix)
  ```

**OBS:** Amazon don't allow /8 prefix. The **larger subnet** that you can have inside a VPC is a **/16**. The **smallest subnet** that you can have inside a VPC is **/28**.

_Remember the following:_

  - Think of VPC as a logical datacenter in AWS

  - Consists of IGWs (Internet Gateways)(Or Virtual Private Gateways), Route Tables, Network Access Control Lists, Subnets and Security Groups

  - 1 Subnet = 1 Availability Zone

  - Security Groups are Stateful; Network Access Control Lists are Stateless

  - NO TRANSITIVE PEERING

<p align="center"><img src="images/aws-no-tp.png" width="400px"></p>

#

**Build a Custom VPC - Lab Notes**

[VPCs and Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)

[Troubleshooting Connecting to Your Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html)

[SSH Agent Forwarding](https://aws.amazon.com/pt/blogs/security/securely-connect-to-linux-instances-running-in-a-private-amazon-vpc/)

- Steps:

  **1.** Set the basic VPC information - Name and IPv4 CIDR Block: `10.0.0.0/16`

  _The range of IPv4 addresses for our VPC in CIDR block format. As mentioned in the earlier topic, block sizes must be between a /16 and /28 netmask._

  **2.** Choose _Amazon provided IPv6 CIDR block_.

  _After the new VPC creation, AWS created Security Group, Network ACL and Route Table. After this, we need to create subnets:_

  <p align="center"><img src="images/aws-vpc-lab1.png" width="700px"></p>

  **3.** Create subnet with basic information - Name, VPC, AZ and IPv4 CIDR block (required): `10.0.1.0/24`

  **4.** Create another subnet with basic information - Name, VPC, AZ and IPv4 CIDR block (required): `10.0.2.0/24`

  **5.** In order to automatically request a public IPv4 or IPv6 address for an instance launched in a subnets, enable auto-assign IP settings for first subnet.

  <p align="center"><img src="images/aws-vpc-lab2.png" width="700px"></p>

  **6.** Create an internet gateway and attach it to the VPC created.

  _OBS:You can have only one attached internet gateway to a VPC._

  **7.** Create a new route table and associate it to the public subnet: 0.0.0.0/0 to created internet gateway.

  **8.** Associate the public route table to the `10.0.1.0/24` subnet.

  **9.** Create 2 EC2 instances and select public subnet settings for one of them.

  **10.** Create a security group to the private instance allowing.

  **11.** Change the private instance network to the new security group.

  **12.** Create a NAT EC2 instance and disable Source/Destination check.

  **13.** Add a route in the VPC's route table to communicate the NAT instance and the private instance.

  _OBS: Create an New WebDMZ security group for the Web instance with SSH and HTTP protocols._  

  <p align="center"><img src="images/aws-vpc-lab3.png" width="700px"></p>

  <p align="center"><img src="images/aws-vpc-arc.png" width="700px"></p>

  _Remember the following:_

    - When you create a VPC a default Route Table, Network Access Control List (NACL) and a default Security Group are created

    - It won't create any subnets, nor will it create a default internet gateway

    - US-East-1A in your AWS account can be completely different availability zone to US-East-1A in another AWS account. The AZ's are randomized

    - Amazon always reserve 5 IP addresses within your subnets

    - You can only have 1 Internet Gateway per VPC

    - Security Groups can't span VPC's

#

**NAT Instances & NAT Gateways**

[Nat Instances](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_NAT_Instance.html)

<p align="center"><img src="images/aws-nat-gateways.png" width="700px"></p>

- **Nat Instances:**

  - When creating a NAT instance, disable Source/Destination Check on the instance

  - NAT instances must be in a public subnet

  - There must be a route out of the private subnet to the NAT instance, in order for this to work

  - The amount of traffic that NAT instances can support depends on the instance size. If you are bottlenecking, increase the instance size

  - You can create high availability using Autoscaling Groups, multiple subnets in different AZs, and a script to automate failover

  - Behind a Security Group

- **Nat Gateways:**

  - Redundant inside the Availability Zone

  - Preferred by the enterprise

  - Starts at 5Gbps and scales currently to 45Gbps

  - No need to patch

  - Not associated with security groups

  - Automatically assigned a public ip address

  - Remember to update your route tables

  - No need to disable Source/Destination Checks

  - _If you have resources in multiple Availability Zones and they share one NAT Gateway, in the event that the NAT gateway's Availability Zone is down, resources in the other Availability Zones lose internet access. To create an Availability Zone-independent architecture, create a NAT gateway in each Availability Zone and configure your routing to ensure that resources use the NAT gateway in the same Availability Zone._

#

**Network Access Control Lists (ACL) vs Security Groups**

[Ephemeral Ports](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html#nacl-ephemeral-ports)

- Your VPC automatically comes with a default network ACL and by default it allows all outbound and inbound traffic.

- You can create custom network ACLs. By default, each custom network ACL denies all inbound and outbound traffic until you add rules.

- Each subnet in your VPC must be associated with a network ACL. If you don't explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL.

- Block IP Addresses using network ACLs not Security Groups.

- You can associate a network ACL with multiple subnets; however, a subnet can be associated with only one network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed.

- Network ACLs contain a numbered list of rules that is evaluated in order, starting with the lowest numbered rule.

- Network ACLs have separate inbound and outbound rules, and each rule can either allow or deny traffic.

- Network ACLs are stateless; responses to allowed inbound traffic are subject to the rules for outbound traffic (and vice versa).

#

**Custom VPCs and ELBs**

- **[Important to Exam]** When you're provisioning a load balancer, you're gonna need at least two public subnets.

#

**VPC Flow Logs**

_What Are VPC Flow Logs?_

VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to an from network interfaces in your VPC. Flow log data is stored using Amazon CloudWatch Logs. After you've created a flow log, you can view and retrieve its data in Amazon CloudWatch Logs.

- You cannot enable flow logs for VPCs that are peered with your VPC unless the peer VPC is in your account.

- You cannot tag a flow log.

- After you've created a flow log, you cannot change its configuration; for example, you can't associate a different IAM role with the flow log.

**Not all IP Traffic is monitored:**

- Traffic generated by instances when they contact the Amazon DNS server. If you use your own DNS server, then all traffic to that DNS server is logged.

- Traffic generated by a Windows instance for Amazon Windows licence activation.

- Traffic to and from 169.254.169.254 for instance metadata.

- DHCP traffic.

- Traffic to the reserved IP address for the default VPC router.

#

**Bastion Hosts**

[SSH Agent Forwarding](https://aws.amazon.com/pt/blogs/security/securely-connect-to-linux-instances-running-in-a-private-amazon-vpc/)

**A Bastion Host:** A Bastion Host is a special purpose computer on a network specifically designed and configured to withstand attacks. The computer generally hosts a single application, for example a proxy server, and all other services are removed or limited to reduce the threat to the computer. It is hardened in this manner primarily due to its location and purpose, which is either on the outside of a firewall or in a demilitarized zone (DMZ) and usually involves access from untrusted networks or computers.

<p align="center"><img src="images/aws-bastion-host.png" width="700px"></p>

- A NAT Gateway or NAT Instance is used to provide internet traffic to EC2 instances in a private subnets.

- A Bastion is used to securely administer EC2 instances (Using SSH or RDP). Bastions are called Jump Boxes in Australia.]

- You cannot use a NAT Gateway as a Bastion Host.

#

**Direct Connect**

**Direct Connect:** AWS Direct Connect is a cloud service solution that makes it easy to stablish a dedicated network connection from your premises to AWS. Using AWS Direct Connect, you can stablish private connectivity between AWS and your datacenter, office, or colocation environment, which in many cases can reduce your network costs, increase bandwidth throughput, and provide a more consistent network experience than Internet-based connections.

<p align="center"><img src="images/aws-direct-connect.png" width="700px"></p>

- Direct Connect directly connects your data center to AWS

- Useful for high throughput workloads (i.e lots of network traffic)

- Or if you need a stable and reliable secure connection

#

**Setting Up a VPN over a Direct Connect**

Remember the steps to creating a Direct Connect Connection.

  - Create a virtual interface in the Direct Connect console. This is a PUBLIC Virtual Interface.

  - Go to the VPC console and then to VPN connections. Create a Customer Gateway.

  - Create a Virtual Private Gateway.

  - Attach the Virtual Private Gateway to the desired VPC.

  - Select VPN Connections and create new VPN Connection.

  - Select the Virtual Private Gateway and the Customer Gateway.

  - Once the VPN is available, setup the VPN on the customer gateway or firewall.  

#

**Global Accelerator**

Know what a Global Accelerator is and where you would use it.

- AWS Global Accelerator is a service in which you create accelerators to improve availability and performance of your applications for local and global users.

- You are assigned two static IP addresses (or alternatively you can bring your own).

- You can control traffic using traffic dials. This is done within endpoint group.

#

**VPC Endpoints**

**A VPC Endpoint:** A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon Network.

Endpoints are virtual devices. They are horizontally scaled, redundant, and highly available VPC components that allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.

<p align="center"><img src="images/aws-vpc-endpoint.png" width="700px"></p>

**There are two types of VPC Endpoints:**

  - Interface Endpoints

  - Gateway Endpoints

**Currently Gateway Endpoints Support:**

  - Amazon S3

  - DynamoDB

## Chapter 8: HA Architecture <img src="images/aws-elb-logo.png" width="30px">

**Elastic Load Balancers**

- ***Application Load Balancers:*** are best suited for load balancing of HTTP and HTTPS traffic. They operate at Layer 7 and are application-aware. They are intelligent, and you can create advanced request routing, sending specified requests to specific web servers.

- ***Network Load Balancers:*** are best suited for load balancing of TCP traffic where extreme performance is required. Operating at the connection level (Layer 4), Network Load Balancer are capable of handling millions of requests per second, while maintaining ultra-low latencies. Use for extreme performance.

- ***Classic Load Balancers:*** are the legacy Elastic Load Balancers. You can load balance HTTP/HTTPS applications and use Layer 7-specific features, such as X-Forwarded and sticky sessions. You can also use strict Layer 4 load balancing for applications that rely purely on the TCP protocol.

- 504 Error means the gateway has timed out. This means that the application not responding within the idle timeout period.

- Troubleshoot the application. Is it the Web Server or Database Server?

- If you need the IPv4 address of your end user, look for the **X-Forwarded-For** header.

- Instances monitored by ELB are reported as: InService or OutofService.

- Healthchecks check the instance health by talking to it.

- Load Balancers have their own DNS name. You are never given an IP address.

- Read the ELB FAQ for all the AWS Load Balancers, because, the exam has about **10 questions of Load Balancing**.

#

**Advanced Load Balancer Theory**

- **Sticky Sessions** enable your users to stick to the same EC2 instance. Can be useful if you are storing information locally to that instance.

<p align="center"><img src="images/aws-sticky-sessions.png" width="700px"></p>

- **Cross Zone Load Balancing** enables you to load balance across multiple availability zones.

<p align="center"><img src="images/aws-cross-zone.png" width="700px"></p>

- **Path Patterns** allow you to direct traffic to different EC2 instances based on the URL contained in the request.

<p align="center"><img src="images/aws-path-patterns.png" width="700px"></p>

#

**Autoscaling Theory**

What are my scaling options?

- Maintain current instance level at all times

- Scale manually

- Scale based on a schedule

- Scale based on demand

- Use predictive scaling

#

**HA Architecture**

<p align="center"><img src="images/aws-ha-architecture.png" width="700px"></p>

**Remember the following**

  - Always Design for failure.

  - Use Multiple AZ's and Multiple Regions wherever you can.

  - Know the difference between Multi-AZ _(is for disaster recovery)_ and Read Replicas _(is for performance improvement)_ for RDS.

  - Know the difference between scaling out _(horizontal - use of Auto-Scaling groups to add additional EC2 instances)_ and scaling up _(vertical - is where we increase the resources inside our EC2 instances)_.

  - Read the question carefully and always consider the cost element.

  - Know the different S3 storage classes.

#

**CloudFormation**

- Is a way of completely scripting your cloud environment.

- Quick Start is a bunch of CloudFormation templates already built by AWS Solutions Architects allowing you to create complex environments very quickly.

#

**Elastic Beanstalk**

- With Elastic Beanstalk, you can quickly deploy and manage applications on the AWS Cloud without worring about the infrastructure that runs those applications. You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling and application health monitoring.

## Chapter 9: Applications <img src="images/aws-sqs-logo.png" width="30px">

**SQS - Simple Queue Service**

[How Amazon SQS Works](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-how-it-works.html)

- SQS is pull based, not pushed based.

- Messages are 256 KB in size.

- Messages can be kept in the queue from 1 minute to 14 days; the default retention period is 4 days.

- Visibility Time Out is the amount of time that the message is invisible in the SQS queue after a reader picks up that message. Provided the job is processed before the visibility time out expires, the message will then be deleted from the queue. If the job is not processed within that time, the message will become visible again and another reader will process it. This could result in the same message being delivered twice.

- Visibility timeout maximum is 12 hours.

- SQS guarantees that your messages will be processed at least once.

- Amazon SQS long polling is a way to retrieve messages from your Amazon SQS queues. While the regular short polling returns immediately (even if the message queue being polled is empty), long polling doesn't return a response until a message arrives in the message queue, or the long poll times out.

- Types of Queue: Standard Queues (default) and FIFO Queues.

#

**SWF - Simple Workflow Service**

- **SWF vs SQS**

  - SQS has a retention period of up to 14 days; with SWF, workflow executions can last up to 1 year.

  - Amazon SWF presents a task-oriented API, whereas Amazon SQS offers a message-oriented API.

  - Amazon SWF ensures that a task is assigned only once and is never duplicated. With Amazon SQS, you need to handle duplicated messages and may also need to ensure that a message is processed only once.

  - Amazon SWF keeps track of all the tasks and events in an application. With Amazon SQS, you need to implement your own application-level tracking, specially if your application uses multiple queues.

- **SWF Actors**

  - _Workflow Starters_ - An application that can initiate (start) a workflow. Could be your e-commerce website following the placement of an order, or a mobile app searching for bus times.

  - _Deciders_ - Control the flow of activity tasks in a workflow execution. If something has finished (or failed) in a workflow, a Decider decides what to do next.

  - _Activity Workers_ - Carry out the activity tasks.

#

**SNS - Simple Notification Service**

- **SNS Benefits:**

  - Instantaneous, push-based delivery (No polling)

  - Simple APIs and easy integration with applications

  - Flexible message delivery over multiple transport protocols

  - Inexpensive, pay-as-you-go model with no up-front costs

  - Web-based AWS Management Console offers the simplicity of a point-and-click interface

- **SNS vs SQS**

  - Both Messaging Services in AWS

  - SNS - Push

  - SQS - Poll (Pull)

#

**Elastic Transcoder**

- Just remember that Elastic Transcoder is a media transcoder in the cloud. It converts media files from their original source format into different formats that will play on smartphones, tablets, PCs, etc.

#

**API Gateway**

- Remember what API Gateway is at a high level (It's essentially a door to your AWS environment).

- API Gateway has caching capabilities to increase performance.

- API Gateway is low cost and scales automatically.

- You can throttle API Gateway to prevent attacks.

- You can log results to CloudWatch.

- If you are using Javascript/AJAX that uses multiple domains with API Gateway, ensure that you have enabled CORS on API Gateway.

- CORS is enforced by the client.

#

**Kinesis 101**

- Know the difference between Kinesis Streams and Kinesis Firehose. You will be given scenario questions and you must choose the most relevant service.

  - **Kinesis Streams (Obs: Kinesis Streams has Shards)**

  <p align="center"><img src="images/aws-kinesis-st.png" width="700px"></p>

  - **Kinesis Firehose**

  <p align="center"><img src="images/aws-kinesis-fh.png" width="700px"></p>

  - **Understand what Kinesis Analytics is.**

  <p align="center"><img src="images/aws-kinesis-anl.png" width="700px"></p>

#

**Web Identity Federation & Cognito**

- Federation allows users to authenticate with a Web Identity Provider (like Google, Facebook and Amazon).

- The user authenticates first with the Web ID Provider and receives an authentication token, which is exchanged for temporary AWS credentials allowing them to assume an IAM role.

- Cognito is an Identity Broker which handles interaction between your applications and the Web ID Provider (You don't need to write your own code to do this).

- **User pool** is user based. It handles things like user registration, authentication and account recovery.

- **Identity pool** authorize access to your AWS resources.


## Chapter 10: Serverless <img src="images/aws-lambda-logo.png" width="30px">

**Lambda**

- **Traditional vs Serverless Architecture**

<p align="center"><img src="images/aws-tradserv-arc.png" width="700px"></p>

- Lambda scales out (not up) automatically.

- Lambda functions are independent, 1 event = 1 function.

- Lambda is serverless.

- Know what services are serverless.

- Lambda Functions can trigger other lambda functions, 1 event can = x functions if functions trigger other functions.

- Architectures can get extremely complicated, AWS X-ray allows you to debug what is happening.

- Lambda can do things globally, you can use it to backup S3 buckets to other S3 buckets, etc.

- Know your triggers.
