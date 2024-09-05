# Introduction to databases on AWS

# **Choose between unmanaged and managed databases**

If you want to trade your on-premises database for a relational database on AWS, you first need to select how you want to run it—managed or unmanaged. Managed services and unmanaged services are handled similar to the shared responsibility model. The shared responsibility model distinguishes between AWS security responsibilities and the customer’s security responsibilities. Likewise, managed compared to unmanaged can be understood as a trade-off between convenience and control.

**Unmanaged databases**

If you operate a relational database on premises, you are responsible for all aspects of operation. This includes data center security and electricity, host machines management, database management, query optimization, and customer data management. You are responsible for absolutely everything, which means you have control over absolutely everything.

Now, suppose you want to shift some of the work to AWS by running your relational database on Amazon Elastic Compute Cloud (Amazon EC2). If you host a database on Amazon EC2, AWS implements and maintains the physical infrastructure and hardware and installs the EC2 instance operating system (OS). However, you are still responsible for managing the EC2 instance, managing the database on that host, optimizing queries, and managing customer data.

This is called an unmanaged database option. In this option, AWS is responsible for and has control over the hardware and underlying infrastructure. You are responsible for and have control over management of the host and database.

You are responsible for everything in a database hosted on-premises. AWS takes on more of that responsibility in databases hosted in Amazon EC2.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/tCWAW7N_ulNvnDIJ_qnA3DCLuIj69t7zG.png

**Managed databases**

To shift more of the work to AWS, you can use a managed database service. These services provide the setup of both the EC2 instance and the database, and they provide systems for high availability, scalability, patching, and backups. However, in this model, you’re still responsible for database tuning, query optimization, and ensuring that your customer data is secure. This option provides the ultimate convenience but the least amount of control compared to the two previous options.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/OSKho6F8uXYdN76j_AOuKIausIFuSmauW.png

# **Resources**

[(opens in a new tab)](https://aws.amazon.com/relational-database/)For more information, see the following resources:

- AWS website: [What Is a Relational Database?(opens in a new tab)](https://aws.amazon.com/relational-database/)
- AWS website: [AWS Cloud Databases](https://aws.amazon.com/products/databases/)