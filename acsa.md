# :cloud: AWS Certified Solutions Architecht - My Notes :cloud:

## Exam Blue Print

- 130 minutes in lenght

- 60 questions _(this can change)_

- Multiple choice

- Results are between 100-1000 with a passing score of 720

- Aim for 70%

- Qualification is valid for 2 years

- Scenario based questions

#

## The 10.000 foot overview 2018

- **Region** - A geographycal area or a physical location with two or more availability zones.

- **Availability Zone** - Discrete data centers with redundant power, networking and connectivity in separate facilities.

- **Edge Location** - Endpoints for AWS for caching content. Consists in CloudFront, Amazon's Content Delivery Network (CDN). *PS: There are many more edge locations than regions*

#

## AWS Services

### Compute

- **EC2** - Elastic Cloud (Compute)
  - Virtual Machines

- **EC2 Container Services** - Containers
  - Data containers at scale

- **Elastic Beanstalk** - Autoscaling deployment tool

- **Lambda** - Serverless computing

- **Lightsail** - Amazon's VPN Service

- **Batch** - Batch computing

#

### Storage

- **S3** - Simple Storage Service
  - Object based storage
  - Upload files to buckets

- **EFS** - Elastic File System
  - Network attached storage
  - Store files in NFS volumes and mount to multiple virtual machines

- **Glacier** - Data archive

- **Snowball** - A huge storage

- **Storage Gateway** - Virtual appliances to replicate local information to S3

#

### Databases

- **RDS** - Relational Database Service
  - MySQL, Microsoft SQL and Aurora (Amazon)

- **DynamoDB** - Non-Relational databases

- **Elasticache** - A way of caching
  - Queries data from your database server

- **Redshift** - A datawarehouse or business intelligence

#

### Migration

- **AWS Migration Hub** - Application tracking service

- **Application Discovery Service** - A tool for discover services and their dependencies

- **Database Migration Service** - A tool for migrate on premise databases into AWS

- **Server Migration Service** - A tool for migrate virtual and physical servers into AWS Cloud

- **Snowball** - A tool for migrate large amounts of data into AWS Cloud _(Terabytes)_

#

### Networking & Content Delivery

- **VPC** - Virtual Private Cloud
  - A virtual datacenter (to configure firewall, availability zones and network addresses)

- **CloudFront** - Amazon's content delivery network

- **Route 53** - Amazon's DNS Service

- **API Gateway** - A tool to creating personal API's

- **Direct Connect** - A tool to stablish a dedicated connection between on-premises network and Amazon's VPC

#

### Management Tools

- **Cloudwatch** - Monitoring Service _(Very important to the exam)_ :star:

- **CloudFormation** - Infrastructure as Code tool _(Very important to the exam)_ :star:

- **CloudTrail** - A log tool for all AWS changes and operations _(Very important to the exam)_ :star:

- **Config** - Monitors the configuration of your entire AWS Environment with snapshots

- **OpsWorks** -  A tool to automate your environment, like ansible, puppet or chef

- **Service Catalog** - Manage catalogs of IT Services _(Very important to the exam)_ :star:

- **Systems Manager** - An interface to manage your AWS resources _(It's not important for the exam)_ :star:

- **Trusted Advisor** - An advisor to the possibly fails or problems in your AWS environment

- **Managed Services**

#

### Analytics

- **EMR** - Elastic MapReduce - A tool for process great amounts of data

- **Kinesis** - A tool for look and analyze real-time streaming data on AWS

- **Data Pipeline** - A tool to share data between your AWS applications

#

### Identity Access Management 101 <img src="images/iamlogo.png" width="20px"></p>

- **What Is IAM?**

  - **IAM** allows you to manage users and their level of access to the AWS Console.

- **Key Features of IAM**

  - Identity Access Management (IAM) offers the following features:

    - Centralised control of your AWS account;

    - Shared Access to your AWS account;

    - Granular permissions;

    - Identity Federation (including Active Directory, Facebook, Linkedin etc);

    - Multifactor Authentication;

    - Provide temporary access for users/devices and services where necessary;

    - Allows you to set up your own password rotation policy;

    - Integrates with many different AWS services;

    - Supports PCI DSS Compliance.

- **Key Terminology For IAM**

  1. **Users:** End users such as people, employees of an organization, etc;

  2. **Groups:** A collection of users. Each user in the group will inherit the permissions of the group.

  3. **Policies:** Policies are made up of documents, called Policy Documents. These documents are in a format called JSON and they give pemissions as to what a User/Group/Role is able to do.

  4. **Roles:** You create roles and then assign them to AWS Resources.

#

**IAM Lab**

- **Recommendations and best practices**

  - Personallize IAM user login link;  

  - Activate MFA (Multi-factor Authentication);

  - Create users;

  - Create groups;

  - Create roles;

- **OBS:**

  - **IAM is universal**. It does note apply to regions at this time;

  - The **"root account"** is simply yhe account created when first setup your AWS account. It has complete Admin access;

  - New users have **NO permissions** when first created;

  - New users are assigned **Access Key ID & Secret Access Keys** when first created;

  - **These are not the same as a password.** You cannot use the Access Key ID & Secret Access Key to login in the console. You can use this to access AWS via the APIs and Command Line, however;

  - **You only get to view these once.** If you lose them, you have to regenerate them. So, save them in a secure location;

  - **Always setup Multifactor Authentication on your root account;**

  - **You can create and customise your own password rotation policies;**

#

- **IAM policy example (JSON):**

```
  {
    "Version":"2012-10-17",
    "Statement":[
      {
        "Effect": "Allow",
        "Action": "*",
        "Resource:" "*"
      }
    ]
  }
```
