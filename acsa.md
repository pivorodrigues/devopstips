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

- **IAM is universal.** It does not apply to regions at this time.

- The **"root account"** is simply the account created when first setup your AWS account. It has complete Admin access.

- New users have **NO permissions** when first created.

- New Users are assigned **Access Key ID** & **Secret Access Keys** when first created.

- **These are not the same as password**. You cannot use tha Access Key ID & Secret Access via to login into the console. You can use this to access AWS via the APIs and Command Line, however.

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

- https://s3-eu-west-1.amazonaws.com/acloudguru

- **Not suitable to install an operating system on**.

- Successful upload will generate a HTTP 200 status code.

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
