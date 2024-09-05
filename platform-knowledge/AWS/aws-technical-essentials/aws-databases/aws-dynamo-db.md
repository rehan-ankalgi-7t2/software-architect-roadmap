# **DynamoDB overview**

DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. With DynamoDB, you can offload the administrative burdens of operating and scaling a distributed database. You don't need to worry about hardware provisioning, setup and configuration, replication, software patching, or cluster scaling.

Amazon DynamoDB

With DynamoDB, you can do the following:

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720990800/6YntGnCZRWG1u-xVNKikrQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/kVuzDqUDnDo_SlWX_GpaRXnlLkGyMvpSN.jpg

- Create database tables that can store and retrieve any amount of data and serve any level of request traffic.
- Scale up or scale down your tables' throughput capacity without downtime or performance degradation.
- Monitor resource usage and performance metrics using the AWS Management Console.

DynamoDB automatically spreads the data and traffic for your tables over a sufficient number of servers to handle your throughput and storage requirements. It does this while maintaining consistent, fast performance. All your data is stored on SSDs and is automatically replicated across multiple Availability Zones in a Region, providing built-in high availability and data durability.

---

# **DynamoDB core components**

In DynamoDB, tables, items, and attributes are the core components that you work with. A table is a collection of items, and each item is a collection of attributes. DynamoDB uses primary keys to uniquely identify each item in a table and secondary indexes to provide more querying flexibility.

- table
- item
- attribute

---

# **DynamoDB use cases**

DynamoDB is a fully managed service that handles the operations work. You can offload the administrative burdens of operating and scaling distributed databases to AWS.

You might want to consider using DynamoDB in the following circumstances:

- You are experiencing scalability problems with other traditional database systems.
- You are actively engaged in developing an application or service.
- You are working with an OLTP workload.
- You care deploying a mission-critical application that must be highly available at all times without manual intervention.
- You require a high level of data durability, regardless of your backup-and-restore strategy.

DynamoDB is used in a wide range of workloads because of its simplicity, from low-scale operations to ultrahigh-scale operations, such as those demanded by Amazon.com.

- software applications
- create media metadata stores
- scale gaming platform
- deliver seamless retail experiences

---

# **DynamoDB security**

DynamoDB provides a number of security features to consider as you develop and implement your own security policies. They include the following:

- DynamoDB provides a highly durable storage infrastructure designed for mission-critical and primary data storage. Data is redundantly stored on multiple devices across multiple facilities in a DynamoDB Region.
- All user data stored in DynamoDB is fully encrypted at rest. DynamoDB encryption at rest provides enhanced security by encrypting all your data at rest using encryption keys stored in AWS Key Management Service (AWS KMS).
- IAM administrators control who can be authenticated and authorized to use DynamoDB resources. You can use IAM to manage access permissions and implement security policies.
- As a managed service, DynamoDB is protected by the AWS global network security procedures.

---

# **Resources**

[(opens in a new tab)](https://www.coursera.org/learn/dynamodb-nosql-database-driven-apps)

[(opens in a new tab)](https://aws.amazon.com/dynamodb/#)For more information, see the following resources:

- AWS website: [Amazon DynamoDB(opens in a new tab)](https://aws.amazon.com/dynamodb/#)
- AWS developer guide: [What is Amazon DynamoDB?(opens in a new tab)](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- AWS blog: [AWS Database Blog](https://aws.amazon.com/blogs/database/how-to-determine-if-amazon-dynamodb-is-appropriate-for-your-needs-and-then-plan-your-migration/)