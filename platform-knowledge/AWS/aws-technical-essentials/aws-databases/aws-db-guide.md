# **Purpose-built databases for all application needs**

We covered Amazon RDS and relational databases in the previous lesson, and for a long time, relational databases were the default option. They were widely used in nearly all applications. A relational database is like a multi-tool. It can do many things, but it is not perfectly suited to any one particular task. It might not always be the best choice for your business needs.

The one-size-fits-all approach of using a relational database for everything no longer works. Over the past few decades, there has been a shift in the database landscape, and this shift has led to the rise of purpose-built databases. Developers can consider the needs of their application and choose a database that will fit those needs.

AWS offers a broad and deep portfolio of purpose-built databases that support diverse data models. Customers can use them to build data-driven, highly scalable, distributed applications. You can pick the best database to solve a specific problem and break away from restrictive commercial databases. You can focus on building applications that meet the needs of your organization.

---

**Amazon DynamoDB**

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720990800/6YntGnCZRWG1u-xVNKikrQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/NteSxsEQYaoMTPXp_DPO9rJxq5DJ9vGbH.jpg

DynamoDB is a fully managed NoSQL database that provides fast, consistent performance at any scale. It has a flexible billing model, tight integration with infrastructure as code (IaC), and a hands-off operational model. DynamoDB has become the database of choice for two categories of applications: high-scale applications and serverless applications. Although DynamoDB is the database of choice for high-scale and serverless applications, it can work for nearly all online transaction processing (OLTP) application workloads. We will explore DynamoDB more in the next lesson.

---

**Amazon ElastiCache**

ElastiCache is a fully managed, in-memory caching solution. It provides support for two open-source, in-memory cache engines: Redis and Memcached. You aren’t responsible for instance failovers, backups and restores, or software upgrades.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720990800/6YntGnCZRWG1u-xVNKikrQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/3VW4NJKF0pa2-tzz_6t3J60vEUqL5xSVD.jpg

---

**Amazon MemoryDB for Redis**

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720990800/6YntGnCZRWG1u-xVNKikrQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/Izh5otLQSaoelNkr_QNvFX17gTaUqOTi8.jpg

MemoryDB is a Redis-compatible, durable, in-memory database service that delivers ultra-fast performance. With MemoryDB, you can achieve microsecond read latency, single-digit millisecond write latency, high throughput, and Multi-AZ durability for modern applications, like those built with microservices architectures. You can use MemoryDB as a fully managed, primary database to build high-performance applications. You do not need to separately manage a cache, durable database, or the required underlying infrastructure.

---

**Amazon DocumentDB (with MongoDB compatibility)**

Amazon DocumentDB is a fully managed document database from AWS. A document database is a type of NoSQL database you can use to store and query rich documents in your application. These types of databases work well for the following use cases: content management systems, profile management, and web and mobile applications. Amazon DocumentDB has API compatibility with MongoDB. This means you can use popular open-source libraries to interact with Amazon DocumentDB, or you can migrate existing databases to Amazon DocumentDB with minimal hassle.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720990800/6YntGnCZRWG1u-xVNKikrQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/Sob2JTCPw34Gzvlp_8SnxZy3BVFDnyL7o.jpg

---

**Amazon Keyspaces (for Apache Cassandra)**

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720990800/6YntGnCZRWG1u-xVNKikrQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/Jvjhds_DmGrf3MJr_4bV4iE5mklGZT95C.jpg

Amazon Keyspaces is a scalable, highly available, and managed Apache Cassandra compatible database service. Apache Cassandra is a popular option for high-scale applications that need top-tier performance. Amazon Keyspaces is a good option for high-volume applications with straightforward access patterns. With Amazon Keyspaces, you can run your Cassandra workloads on AWS using the same Cassandra Query Language (CQL) code, Apache 2.0 licensed drivers, and tools that you use today.

---

**Amazon Neptune**

Neptune is a fully managed graph database offered by AWS. A graph database is a good choice for highly connected data with a rich variety of relationships. Companies often use graph databases for recommendation engines, fraud detection, and knowledge graphs.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720990800/6YntGnCZRWG1u-xVNKikrQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/FJCi0y2sbmM76oup_jDeqOAfXphRlOHGg.jpg

---

**Amazon Timestream**

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720990800/6YntGnCZRWG1u-xVNKikrQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/1GFeT9IkuDN30ySV_Ox7oerB5roOIChoG.jpg

Timestream is a fast, scalable, and serverless time series database service for Internet of Things (IoT) and operational applications. It makes it easy to store and analyze trillions of events per day up to 1,000 times faster and for as little as one-tenth of the cost of relational databases. Time series data is a sequence of data points recorded over a time interval. It is used for measuring events that change over time, such as stock prices over time or temperature measurements over time.

---

**Amazon Quantum Ledger Database (Amazon QLDB)**

With traditional databases, you can overwrite or delete data, so developers use techniques, such as audit tables and audit trails to help track data lineage. These approaches can be difficult to scale and put the burden of ensuring that all data is recorded on the application developer. Amazon QLDB is a purpose-built ledger database that provides a complete and cryptographically verifiable history of all changes made to your application data.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720990800/6YntGnCZRWG1u-xVNKikrQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/MSfjz0upeUhx_Tm__rwwNX-sea70gSgPv.jpg

# **Resources**

[(opens in a new tab)](https://aws.amazon.com/products/databases/)For more information, see the following resource:

- AWS website: [AWS Cloud Databases](https://aws.amazon.com/products/databases/)