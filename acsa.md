## <img src="images/acg.png" width="30px"> AWS Certified Solutions Architecht - A Cloud Guru Exam Tips <img src="images/acg.png" width="30px">

## Chapter 1: Introduction - Exam Blue Print

- 130 minutes in lenght

- 60 questions _(this can change)_

- Multiple choice

- Results are between 100-1000 with a passing score of 720

- Aim for 70%

- Qualification is valid for 3 years

- Scenario based questions


## Chapter 2: AWS - 10.000 Foot Overview (Exam Tips)

**Understand the difference between a Region, an Availability Zone (AZ) and an Edge Location**

- A **Region** is a physical location in the world which consists of two or more Availability Zones (AZ's).

- An **Availability Zone** is one or more discrete data centers, each with redundant power, networking and connectivity, housed in separate facilities.

- **Edge Locations** are endpoints for AWS which are used for caching content. Typically this consists of CloudFront, Amazon's Content Delivery Network (CDN). *PS: There are many more edge locations than regions*

#

**What Do I Need To Know To Pass My Solutions Architect Exam?**

  - **Security, Identity & Compliance**

    - [IAM](https://github.com/pivorodrigues/devopstips/blob/master/acsa.md#identity-access-management---101-)

  - **Storage**

    - [S3](https://github.com/pivorodrigues/devopstips/blob/master/acsa.md#chapter-3-identity-access-management--s3)

  - **Compute**

    - EC2

    - Lambda

  - **Databases**

    - RDS

    - DynamoDB

    - Redshift

  - **Network & Content Delivery**

    - Route 53


## Chapter 3: Identity Access Management & S3

**Identity Access Management 101 - Exam Tips**

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

**S3 101 - Exam Tips**

- Remember that S3 is **Object-based**: i.e. allows you to upload files.

- Files can be from 0 Bytes to 5 TB.

- There is unlimited storage.

- Files are stored in Buckets (It´s basically a folder in the cloud).

- **S3 is a universal namespace**. That is, names must be unique globally.

- URL Example: https://s3-eu-west-1.amazonaws.com/acloudguru

- **Not suitable to install an operating system on**.

- Successful uploads will generate a HTTP 200 status code.

- By default, all newly created buckets are **PRIVATE**. You can setup access control to your buckets using:

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

#

**S3 Bucket Lab - Exam Tips**

- **Buckets are a universal name space**

- Upload an object to S3 receive a HTTP 200 Code

- S3, S3 - IA, S3 IA (One Zone), Glacier

- Control access to buckets using either **bucket ACL** or using **Bucket Policies**

#

**S3 Security and Encryption - Exam Tips**

- Encryption In Transit is achieved by:

	- SSL/TLS

- Encryption at Rest (Server Side) is achieved by:

	- S3 Managed Keys - SSE-S3

	- AWS Key Management Service, Managed Keys (SSE-KMS)

	- Server Side Encryption with Customer Provided Keys (SSE-C)

- Client Side Encryption	 

#

**S3 Versioning - Exam Tips**

- Store all versions of an object (including all writes and even if you delete an object).

- Great backup tool.

- Once enabled, Versioning cannot be disabled, only suspended.

- Integrates with Lifecycles rules.

- Versioning's MFA Delete capability, which uses multi-factor authentication, can be used to provide an additional layer of security.

#

**S3 Lifecycle Management, S3 IA and Glacier - Exam Tips**

- Automates moving your objects between the different storage tiers.

- Can be used in conjunction with versioning.

- Can be applied to current versions and previous versions.

#

**Cross Region Replication - Exam Tips**

- Versioning must be enabled on both the source and destination buckets.

- Regions must be unique.

- Files in an existing bucket are not replicated automatically.

- All subsequent updated files will be replicated automatically.

- Delete markers are not replicated.

- Deleting individual versions or delete markers will not be replicated.

- Understand what Cross Replication is at a high level.

#

**S3 Transfer Acceleration**

<p align="center"><img src="images/s3ta.png" width="500px"></p>

- [Amazon S3 Transfer Acceleration Speed Comparison](https://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html)

#

**CloudFront - Exam Tips**

- **Edge Location** - This is the location where content will be cached. This is separate to an AWS Region/AZ.

- **Origin** - This is the origin of all the files that the CDN will distribute. This can be either an S3 bucket, an EC2 instance, an Elastic Load Balancer, or Route 53.

- **Distribution** - This is the name given the CDN which consists of a collection of Edge Locations.

- **Web Distribution** - Typically used for Websites.

- **RTMP** - Used for Media Streaming.

- Edge Locations are not just READ only - you can write to them too. (ie put an object on to them.)

- Objects are cached for the life of the **TTL (Time To Live)**.

- You can clear cached objects, but you will be charged.

- CloudFront is a global service.

- You can invalidate cached objects, but, you will be charged.

#

**Snowball - Exam Tips**

- Understand what Snowball is.

- Understand what Snowball Can.

- Import to S3.

- Export from S3

#

**Storage Gateway - Exam Tips**

- **File Gateway**

	- File Gateway - For flat files, stored directly on S3.

- **Volume Gateway**

	- **Stored Volumes** - Entire Dataset is store on site and is asynchronously backed to S3.

	- **Cached Volumes** - Entire Dataset is stored on S3 and the most frequently accessed data is cached on site.

- **Gateway Virtual Tape Library**		 