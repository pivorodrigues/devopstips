## AWS Certified Solutions Architect - Study and Quiz Notes

### Amazon S3

**Amazon S3 Bucket Properties**

  - **Versioning -** Versioning enables you to keep multiple versions of an object in one bucket. By default, versioning is disabled for a new bucket.

  - **Server access logging –** Server access logging provides detailed records for the requests that are made to your bucket. By default, Amazon S3 does not collect server access logs.

  - **Static website hosting –** You can host a static website on Amazon S3. To enable static website hosting, choose **Static website hosting** and then specify the settings you want to use.

  - **Object-level logging –** Object-level logging records object-level API activity by using CloudTrail data events.

  - **Tags –** With AWS cost allocation, you can use bucket tags to annotate billing for your use of a bucket. A tag is a key-value pair that represents a label that you assign to a bucket. To add tags, choose Tags, and then choose **Add tag**.

  - **Transfer acceleration –** Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket.

  - **Events –** You can enable certain Amazon S3 bucket events to send a notification message to a destination whenever the events occur. To enable events, choose **Events** and then specify the settings you want to use.

  - **Requester Pays** – You can enable Requester Pays so that the requester (instead of the bucket owner) pays for requests and data transfers.

#

**Amazon S3 Object Properties**

  - **Storage class –** Each object in Amazon S3 has a storage class associated with it. The storage class that you choose to use depends on how frequently you access the object. The default storage class for S3 objects is STANDARD. You choose which storage class to use when you upload an object.

  - **Encryption –** You can encrypt your S3 objects.

  - **Metadata –** Each object in Amazon S3 has a set of name-value pairs that represents its metadata.

  - **Tags –** You can add tags to an S3 object.

#

**Amazon S3 Data Consistency Model**

  - Amazon S3 provides *read-after-write* consistency for PUTS of **NEW** objects in buckets.

  - Amazon S3 offers *eventual* consistency for **OVERWRITE** PUTS and DELETES in all regions.

  - Read-after-write consistency allows you to retrieve objects immediatly after creation in Amazon S3.

#

**File Gateway**

  - The File Gateway presents a file interface that enables you to store files as objects in Amazon S3 using the industry-standard NFS and SMB protocols and access those files via NFS and SMB from your datacenter or Amazon EC2, or access those files as objects with the S3 API.

#

**Request Rate and Performance Guidelines**

  - Amazon S3 automatically scales to high request rates. For example, your application can achieve at least 3.500 PUT/POST/DELETES and 5.500 GET requests per second per prefix in a bucket. There are no limits to the number of prefixes in a bucket. It is simple to increase your read or write performance exponentially. For example, if you create 10 prefixes in an Amazon S3 bucket to parallelize reads, you could scale your read performance to 55.000 read requests per second.

#

**Uploading Objects (Multi-parts Uploading)**

  - Depending on the size of the data you are uploading, Amazon S3 offers the following options:

    - **Upload objects in a single operation -** With a _single PUT operation_, you can upload up to **5 GB** in size.

    - **Upload objects in parts -** using the _multipart upload API_, you can upload large objects, up to **5 TB**. The multipart upload API is designed to improve the upload experience for larger objects. You can upload objects in parts. These object parts can be uploaded independently, in any order, and in parallel. You can use a multipart upload for objects from **5 MB** to **5TB** in size.

  - Amazon recommends that you use multipart uploading in the following ways:

    - If you're uploading large objects over a **stable high-bandwidth network**, use multipart uploading to **maximize** the use of your available bandwidth by uploading object parts in parallel for mult-threaded performance.

    - If you're uploading over a **spotty network**, use multipart uploading to increase **resiliency** to network errors by avoiding upload restarts. When using multipart uploading, you need to retry uploading only parts that are interrupted during the upload. You don't need to restart uploading your object from the beginning.

#

**Amazon S3 Object-Level Actions Tracked by CloudTrail Logging**

  - Using the information collected by CloudTrail, you can determine what request was made to Amazon S3, the source IP address from which the request was made, who made the request, when its made, and so on. This information helps you to track changes made to your AWS resources and to troubleshoot operational issues.

  - You can also get CloudTrail logs for object-level Amazon S3 actions. To do this, specify the Amazon S3 object for your trail. When an object-level action occurs in your account, CloudTrail evaluates your trail settings. If the event matches the object that you specified in a trail, the event is logged.

#

**Object Metadata**

  - There are two kinds of metadata: ***system metadata*** and ***user-defined metadata***.

    - **System-Defined Object Metadata**
