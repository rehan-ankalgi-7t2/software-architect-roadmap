# **Amazon RDS overview**

Amazon Relational Database Service (Amazon RDS)

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/yJhL8pzTtot8NIEq_YflAxuhYwZDS5mdn.png

Amazon RDS is a managed database service customers can use to create and manage relational databases in the cloud without the operational burden of traditional database management. For example, imagine you sell healthcare equipment, and your goal is to be the number-one seller on the West Coast of the United States. Building a database doesn’t directly help you achieve that goal. However, having a database is a necessary component to achieving that goal.

With Amazon RDS, you can offload some of the unrelated work of creating and managing a database. You can focus on the tasks that differentiate your application, instead of focusing on infrastructure-related tasks, like provisioning, patching, scaling, and restoring.

Amazon RDS supports most of the popular RDBMSs, ranging from commercial options to open-source options and even a specific AWS option. Supported Amazon RDS engines include the following:

- **Commercial:** Oracle, SQL Server
- **Open source:** MySQL, PostgreSQL, MariaDB
- **Cloud native:** Aurora

---

# **Database instances**

Just like the databases you build and manage yourself, Amazon RDS is built from compute and storage. The compute portion is called the database (DB) instance, which runs the DB engine. Depending on the engine selected, the instance will have different supported features and configurations. A DB instance can contain multiple databases with the same engine, and each DB can contain multiple tables.

Underneath the DB instance is an EC2 instance. However, this instance is managed through the Amazon RDS console instead of the Amazon EC2 console. When you create your DB instance, you choose the instance type and size. The DB instance class you choose affects how much processing power and memory it has.

To learn more about the various instance classes, choose each of the four numbered markers.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/CUBPkwivlQXbuEip_jEejSDXvrCT_sMKJ.png

---

# **Storage on Amazon RDS**

The storage portion of DB instances for Amazon RDS use Amazon Elastic Block Store (Amazon EBS) volumes for database and log storage. This includes MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server.

When using Aurora, data is stored in cluster volumes, which are single, virtual volumes that use solid-state drives (SSDs). A cluster volume contains copies of your data across three Availability Zones in a single AWS Region. For nonpersistent, temporary files, Aurora uses local storage.

Amazon RDS provides three storage types: General Purpose SSD (also called gp2 and gp3), Provisioned IOPS SSD (also called io1), and Magnetic (also called standard). They differ in performance characteristics and price, which means you can tailor your storage performance and cost to the needs of your database workload.

---

# **Amazon RDS in an Amazon Virtual Private Cloud**

When you create a DB instance, you select the Amazon Virtual Private Cloud (Amazon VPC) your databases will live in. Then, you select the subnets that will be designated for your DB. This is called a DB subnet group, and it has at least two Availability Zones in its Region. The subnets in a DB subnet group should be private, so they don’t have a route to the internet gateway. This ensures that your DB instance, and the data inside it, can be reached only by the application backend.

Access to the DB instance can be restricted further by using network access control lists (network ACLs) and security groups. With these firewalls, you can control, at a granular level, the type of traffic you want to provide access into your database.

Using these controls provides layers of security for your infrastructure. It reinforces that only the backend instances have access to the database.

---

# **Backup data**

You don’t want to lose your data. To take regular backups of your Amazon RDS instance, you can use automated backups or manual snapshots. To learn about a category, choose the appropriate tab.

## Automated Backups

Automated backups are turned on by default. This backs up your entire DB instance (not just individual databases on the instance) and your transaction logs. When you create your DB instance, you set a backup window that is the period of time that automatic backups occur. Typically, you want to set the window during a time when your database experiences little activity because it can cause increased latency and downtime.

**Retaining backups:** Automated backups are retained between 0 and 35 days. You might ask yourself, “Why set automated backups for 0 days?” The 0 days setting stops automated backups from happening. If you set it to 0, it will also delete all existing automated backups. This is not ideal. The benefit of automated backups that you can do point-in-time recovery.

**Point-in-time recovery:** This creates a new DB instance using data restored from a specific point in time. This restoration method provides more granularity by restoring the full backup and rolling back transactions up to the specified time range.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/c_pMH598qgWk7S1P_bYtYIJwvBfBmglnI.jpg

## Manual Snapshots

If you want to keep your automated backups longer than 35 days, use manual snapshots. Manual snapshots are similar to taking Amazon EBS snapshots, except you manage them in the Amazon RDS console. These are backups that you can initiate at any time. They exist until you delete them. For example, to meet a compliance requirement that mandates you to keep database backups for a year, you need to use manual snapshots. If you restore data from a manual snapshot, it creates a new DB instance using the data from the snapshot.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/y_Y-OYIsnmNFdD5C_QT-2JHlAXXeiyhfF.jpg

**Choosing a backup option**

It is advisable to deploy both backup options. Automated backups are beneficial for point-in-time recovery. With manual snapshots, you can retain backups for longer than 35 days.

---

# **Redundancy with Amazon RDS Multi-AZ**

In an Amazon RDS Multi-AZ deployment, Amazon RDS creates a redundant copy of your database in another Availability Zone. You end up with two copies of your database—a primary copy in a subnet in one Availability Zone and a standby copy in a subnet in a second Availability Zone.

The primary copy of your database provides access to your data so that applications can query and display the information. The data in the primary copy is synchronously replicated to the standby copy. The standby copy is not considered an active database, and it does not get queried by applications.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/uH2dbGPLi5h5x4Xk_427K0gUGe81kqVaq.png

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/uH2dbGPLi5h5x4Xk_427K0gUGe81kqVaq.png

To improve availability, Amazon RDS Multi-AZ ensures that you have two copies of your database running and that one of them is in the primary role. If an availability issue arises, such as the primary database loses connectivity, Amazon RDS initiates an automatic failover.

When you create a DB instance, a Domain Name System (DNS) name is provided. AWS uses that DNS name to fail over to the standby database. In an automatic failover, the standby database is promoted to the primary role, and queries are redirected to the new primary database.

To help ensure that you don't lose Multi-AZ configuration, there are two ways you can create a new standby database. They are as follows:

- Demote the previous primary to standby if it's still up and running.
- Stand up a new standby DB instance.

The reason you can select multiple subnets for an Amazon RDS database is because of the Multi-AZ configuration. You will want to ensure that you have subnets in different Availability Zones for your primary and standby copies.

---

# **Amazon RDS security**

When it comes to security in Amazon RDS, you have control over managing access to your Amazon RDS resources, such as your databases on a DB instance. How you manage access will depend on the tasks you or other users need to perform in Amazon RDS. Network ACLs and security groups help users dictate the flow of traffic. If you want to restrict the actions and resources others can access, you can use AWS Identity and Access Management (IAM) policies.

- IAM
- security groups
- Amazon RDS encryption
- SSL & TLS