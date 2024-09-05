# Core service `Database`

| **Database type** | **Use cases** | **AWS service** |
| --- | --- | --- |
| **Relational** | Traditional applications, enterprise resource planning (ERP), customer relationship management (CRM), e-commerce | Amazon AuroraAmazon RDSAmazon Redshift |
| **Key-value** | High-traffic web applications, e-commerce systems, gaming applications | Amazon DynamoDB |
| **In-memory** | Caching, session management, gaming leaderboards, geospatial applications | Amazon ElastiCache,Amazon MemoryDBfor Redis |
| **Document** | Content management, catalogs, user profiles | Amazon DocumentDB (with MongoDB compatibility) |
| **Wide column** | High-scale industrial apps for equipment maintenance, fleet management, route optimization | Amazon Keyspaces |
| **Graph** | Fraud detection, social networking, recommendation engines | Amazon Neptune |
| **Time series** | Internet of Things (IoT) applications, DevOps, industrial telemetry | Amazon Timestream |
| **Ledger** | Systems of record, supply chain, registrations, banking transactions | Amazon Ledger Database Services (QLDB) |

---

## Relational Database

### Amazon Aurora ✨

> MySQL and PostgreSQL-compatible **relational database**
 built in the cloud for the cloud.
> 

- It is compatible with MySQL, so you can run those engines with increased performance on AWS.
- The database supports **High availability and** durability, ****and you can run it serverless. This takes care of automatically scaling the resources for you.
- With Aurora, you also can run the database with multi-Regional replicas.
- Performance and availability of commercial-grade databases at 1/10th the cost.

### Amazon RDS

<aside>
💡 Set up, operate, and scale a relational database in the cloud with just a few clicks.

</aside>

- You can choose Amazon Relational Database Service (Amazon RDS) to launch the database in the Multi-AZ configuration if you want to deploy it for high availability (HA).
- The service will launch the primary and standby databases in different Availability Zones and set up synchronous replication of data and failover strategy.
- If the primary database goes down, the standby picks up the traffic.

### Amazon Redshift

<aside>
💡 Analyze your data with the fastest and most widely used cloud data warehouse.

</aside>

- Amazon Redshift is a data warehouse service that provides **benefits from columnar storage.**
- With this approach, you can **perform complex queries on** your **data**, helping you **run online analytical processing (OLAP) workloads**.


## Key-value database

### Amazon DynamoDB

<aside>
💡 Get a fast, flexible, and serverless NoSQL database for any scale to support key-value and document workloads.

</aside>

- With DynamoDB, you can achieve **single-digit millisecond performance at any scale.**
- It is a **fully managed, serverless, nonrelational database**.
- DynamoDB is a great choice when you're looking for **seamless database scalability**. DynamoDB will automatically scale to meet demand.
- DynamoDB is also an excellent choice for workloads that involve working with databases, **flexible schemas**, and **high throughput** (with many read/write requests).

## In-Memory Database

### Amazon ElastiCache

- Unlock microsrcond latency
- Scalable caching service

### Amazon MemoryDB for Redis

- Compatible
- Durable

## Document Database

### Amazon DocumentDB (with MongoDB Compatibility)

- Scale JSON workloads with ease
- Use an enterprise-ready document database service compatible with MongoDB

## Wide column database

### Amazon Keyspaces

- Scalable
- Highly Available
- Run your Apache Cassandra workloads

## Graph Database

### Amazon Neptune AWS service

- Amazon Neptune is used for simplifying the setup and running of your graph databases.
- This helps you run databases aware of relationships between data.
- Amazon Neptune can be useful for fraud detection, social media, and similar applications.
- Build applications that work with highly connected datasets.

## TimeSeries Database

### Amazon Timestream
- Fast
- Scalable
- Store and analyze trillions of events per day


## Ledger Database

### Amazon Quantum Ledger Database (QLDB)
Provides logs that are as follows:

- Transparent
- Immutable
- Cryptographically verifiable