# Core Services `Storage`
<aside>
💡Amazon S3
</aside>

Amazon Simple Storage Service (Amazon S3) is a fully managed, serverless, low-cost, object-level storage service. With Amazon S3, you store unlimited amounts of data (with different formats) on AWS. Amazon S3 offers multiple storage options.

## **Amazon S3 storage classes**

Amazon S3 offers a range of storage classes that you can choose from based on your workload's data access, resiliency, and cost requirements.

**Amazon S3 Standard**

Amazon S3 Standard is appropriate for various use cases, including cloud applications, dynamic websites, content distribution, mobile and gaming applications, and big data analytics.

**Amazon S3 Intelligent-Tiering**

Amazon S3 Intelligent-Tiering delivers milliseconds latency and high throughput performance for frequently, infrequently, and rarely accessed data in the Frequent, Infrequent, and Archive Instant Access tiers. You can use S3 Intelligent-Tiering as the default storage class for virtually any workload, especially data lakes, data analytics, new applications, and user-generated content.

**Amazon S3 Standard-IA**

Amazon S3 Standard-IA is for data accessed less frequently but requires rapid access when needed. S3 Standard-IA offers the high durability, high throughput, and low latency of Amazon S3 Standard with a low per GB storage price and per GB retrieval charge. This combination of low cost and high performance makes S3 Standard-IA ideal for long-term storage, backups, and data store for disaster recovery files.

**Amazon S3 One Zone-IA**

Amazon S3 One Zone-IA is for data accessed less frequently but requires rapid access when needed. For example, S3 One Zone-IA offers the same high durability, high throughput, and latency as Amazon S3 Standard with a low per GB storage price and per GB retrieval charge.

### Other storage classess in S3

**Amazon S3 Glacier Instant Retrieval**

Amazon S3 Glacier Instant Retrieval is an archive storage class that delivers the lowest-cost storage for long-lived data that is rarely accessed and requires retrieval in milliseconds.

**Amazon S3 Glacier Flexible Retrieval**

Amazon S3 Glacier Flexible Retrieval delivers the most flexible retrieval options that balance cost with access times ranging from minutes to hours and with free bulk retrievals. It is an ideal solution for backup, disaster recovery, and offsite data storage needs. When some data occasionally needs to be retrieved in minutes, you don’t want to worry about costs.

**Amazon S3 Glacier Deep Archive**

Amazon S3 Glacier Deep Archive is lowest-cost storage class in Amazon S3 and supports long-term retention and digital preservation for data that can be accessed once or twice a year. It is designed for customers that retain data sets for 7—10 years or longer to meet regulatory compliance requirements. S3 Glacier Deep Archive can also be used for backup and disaster recovery use cases. It is a cost-effective and easy-to-manage alternative to magnetic tape systems, whether on-premises libraries or off-premises services.

**Amazon S3 Outposts**

Amazon S3 on Outposts delivers object storage to your on-premises AWS Outposts environment. Using the S3 APIs and features available in AWS Regions today, S3 on Outposts makes it easy to store and retrieve data on your Outpost, secure the data, control access, tag, and report on it

# S3 storage benefits

- Amazon S3 gives you confidence that there is **very little** chance for Amazon S3 to lose or break your object after you have uploaded it.
- It is designed for 99.999999999 percent durability.
- With this support, you can build event-driven applications.
- To create thumbnails of your photos to arrive in your S3 bucket:
    - You can create event triggers on each object "put the request."
    - This triggers the AWS Lambda function that runs a code to transform the image into a thumbnail, sending the result to another S3 bucket.

# Amazon S3 use cases

**Content storage and distribution**

- Benefit from the unlimited storage capacity for **big data workloads**, using Amazon S3 as a data lake for large amounts of data.
- Store various **types of content,** including **media content**.

**Backup and archiving**

- Use Amazon S3 for durably storing backups (even from different AWS services).
- Amazon S3 Glacier is a great choice when:
    - You have to archive your data for long periods of time.
    - You need low-cost storage.
    - You must make sure your archives will not be deleted for a period of time (vault lock).
    

**Build a data lake**

- Run big data analytics, artificial intelligence (AI), machine learning (ML), and high performance computing (HPC) applications to unlock data insights.

**Backup and restore critical data**

- Meet Recovery Time Objectives (RTO), Recovery Point Objectives (RPO), and compliance requirements with S3's robust replication features.

**Archive data**

- Move data archives to the Amazon S3 Glacier storage classes to lower costs, eliminate operational complexities, and gain new insights.

**Run cloud-native apps**

- Build fast, powerful mobile and web-based cloud-native apps that scale automatically in a highly available configuration.

# Other Storage services in AWS

**Amazon Elastic File System (Amazon EFS)**

- Scalable network file storage for Amazon EC2 instances

**Amazon Elastic Block Store (Amazon EBS)**

- Purpose focused volume types
- Network-attached volumes that provide durable block-level storage for Amazon EC2 instances

## Amazon EBS

Amazon EBS has the following benefits:

- Persistent network-attached block storage for instances that can persist even after the EC2 instance to which this storage is attached is terminated
- Different drive types
- Scalable
- Pay only for what you provision
- Snapshot functionality
- Encryption available to enhance security

More information about Amazon EBS includes the following:

- As data is very important, you have the opportunity to take incremental snapshots of the volume. You can keep them indefinitely while having the opportunity to recover the volumes when needed.
- When you encrypt Amazon EBS volume, all the data in the volume, data traveling between the instance and EBS are encrypted.
- When you encrypt EBS volume, snapshots taken from these volumes are encrypted.
- Just like Amazon EC2, you have control over how much and what type SSD/HDD of storage you provision and if you need to scale it you can modify your volume.


## Amazon EFS

When you need a serverless shared file system, you can use Amazon Elastic File System (Amazon EFS).

Amazon EFS provides serverless, fully elastic file storage so that you can share file data without provisioning or managing storage capacity and performance.

With Amazon EFS, you can build high performing and cost-optimized file systems on AWS benefitting from the built-in-elasticity, durability, and availability.

**Advantages of EFS**

1. Serverless shared and scalable storage class
2. Elastic, simple, and highly reliable
3. Performant and cost optimized
4. Full AWS compute integration
5. Highly durable and available
6. Four storage classes

## Amazon FSx

- Amazon FSx makes it easy and cost effective to launch, run, and scale feature-rich, high-performance file systems in the cloud.
- It supports a wide range of workloads with its reliability, security, scalability, and broad set of capabilities.
- Amazon FSx is built on the latest AWS compute, networking, and disk technologies to provide high performance and lower total cost of ownership (TCO). And as a fully managed service, it handles hardware provisioning, patching, and backups—freeing you up to focus on your applications, your end users, and your business.
- You can choose between four widely used file systems: NetApp ONTAP, OpenZFS, Windows File Server, and Lustre.