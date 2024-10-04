> **Object storage is built for the cloud and delivers virtually unlimited scalability, high durability, and cost effectiveness.**
> 

# **Amazon S3**

Unlike Amazon EBS, Amazon Simple Storage Service (Amazon S3) is a standalone storage solution that isn’t tied to compute. With Amazon S3, you can retrieve your data from anywhere on the web. If you have used an online storage service to back up the data from your local machine, you most likely have used a service similar to Amazon S3. The big difference between those online storage services and Amazon S3 is the storage type.

Amazon S3 is an object storage service. Object storage stores data in a flat structure. An object is a file combined with metadata. You can store as many of these objects as you want. All the characteristics of object storage are also characteristics of Amazon S3.

# **Amazon S3 concepts**

![](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/295g13cRIaMQIRKc_J5XS-4bErHuFtWRy.png)

In Amazon S3, you store your objects in containers called buckets. You can’t upload an object, not even a single photo, to Amazon S3 without creating a bucket first. When you store an object in a bucket, the combination of a bucket name, key, and version ID uniquely identifies the object.

When you create a bucket, you specify, at the very minimum, two details: the bucket name and the AWS Region that you want the bucket to reside in.

To learn more, choose each of the numbered markers.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/s3XrzDAuvsjgq76i_w4B6158YVyIYUoJC.jpg

**Amazon S3 bucket names**

Amazon S3 supports global buckets. Therefore, each bucket name must be unique across all AWS accounts in all AWS Regions within a partition. A partition is a grouping of Regions, of which AWS currently has three: Standard Regions, China Regions, and AWS GovCloud (US). When naming a bucket, choose a name that is relevant to you or your business. For example, you should avoid using AWS or Amazon in your bucket name.

The following are some examples of the rules that apply for naming buckets in Amazon S3. For a full list of rules, see the link in the resources section.

- Bucket names must be between 3 (min) and 63 (max) characters long.
- Bucket names can consist only of lowercase letters, numbers, dots (.), and hyphens (-).
- Bucket names must begin and end with a letter or number.
- Buckets must not be formatted as an IP address.
- A bucket name cannot be used by another AWS account in the same partition until the bucket is deleted.

If your application automatically creates buckets, choose a bucket naming scheme that is unlikely to cause naming conflicts and will choose a different bucket name, should one not be available.

**Object key names**

The object key (key name) uniquely identifies the object in an Amazon S3 bucket. When you create an object, you specify the key name. As described earlier, the Amazon S3 model is a flat structure, meaning there is no hierarchy of subbuckets or subfolders. However, the Amazon S3 console does support the concept of folders. By using key name prefixes and delimiters, you can imply a logical hierarchy.

For example, suppose your bucket called *testbucket* has two objects with the following object keys: *2022-03-01/AmazonS3.html* and *2022-03-01/Cats.jpg*. The console uses the key name prefix, *2022-03-01*, and delimiter (*/*) to present a folder structure.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/KrcyXuZ1QWVOpiJq_sN1Un2LLeNg_T0eo.png

# S3 Usecases

- Backup and storage
- Media Hosting
- Software delivery
- data lakes
- static websites
- static content

# Security in Amazon S3

Everything in Amazon S3 is private by default. This means that all Amazon S3 resources, such as buckets and objects, can only be viewed by the user or AWS account that created that resource. Amazon S3 resources are all private and protected to begin with.

If you decide that you want everyone on the internet to see your photos, you can choose to make your buckets and objects public. A public resource means that everyone on the internet can see it. Most of the time, you don’t want your permissions to be all or nothing. Typically, you want to be more granular about the way that you provide access to your resources.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/P9SUsZxRgA_qWqPA_qHtpoUP9GBh3EM0n.png

To be more specific about who can do what with your Amazon S3 resources, Amazon S3 provides several security management features: IAM policies, S3 bucket policies, and encryption to develop and implement your own security policies.

**Amazon S3 and IAM policies**

Previously, you learned about creating and using AWS Identity and Access Management (IAM) policies. Now you can apply that knowledge to Amazon S3. When IAM policies are attached to your resources (buckets and objects) or IAM users, groups, and roles, the policies define which actions they can perform. Access policies that you attach to your resources are referred to as *resource-based policies* ****and access policies attached to users in your account are called *user policie***s**.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/Pfa9KAgXPW6HPKKr_KRLzH0N3cmxDxdbv.png

You should use IAM policies for private buckets in the following two scenarios:

- You have many buckets with different permission requirements. Instead of defining many different S3 bucket policies, you can use IAM policies.
- You want all policies to be in a centralized location. By using IAM policies, you can manage all policy information in one location.

**Amazon S3 bucket policies**

Like IAM policies, S3 bucket policies are defined in a JSON format. Unlike IAM policies, which are attached to resources and users, S3 bucket policies can only be attached to S3 buckets. The policy that is placed on the bucket applies to every object in that bucket. S3 bucket policies specify what actions are allowed or denied on the bucket.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/akU_ZLGswUu3ffWC_ViWAEK_d9Xgt0pjU.png

You should use S3 bucket policies in the following scenarios:

- You need a simple way to do cross-account access to Amazon S3, without using IAM roles.
- Your IAM policies bump up against the defined size limit. S3 bucket policies have a larger size limit.

For examples of bucket policies, see the [Bucket Policy Examples(opens in a new tab)](https://docs.aws.amazon.com/en_us/AmazonS3/latest/userguide/example-bucket-policies.html) link here or in the resources section.

**Amazon S3 encryption**

Amazon S3 reinforces encryption in transit (as it travels to and from Amazon S3) and at rest. To protect data, Amazon S3 automatically encrypts all objects on upload and applies server-side encryption with S3-managed keys as the base level of encryption for every bucket in Amazon S3 at no additional cost

# **Amazon S3 storage classes**

When you upload an object to Amazon S3 and you don’t specify the storage class, you upload it to the default storage class, often referred to as standard storage. In previous lessons, you learned about the default Amazon S3 standard storage class.

Amazon S3 storage classes let you change your storage tier when your data characteristics change. For example, if you are accessing your old photos infrequently, you might want to change the storage class for the photos to save costs.

| **Storage Class** | **Description** |
| --- | --- |
| **S3 Standard** | This is considered general-purpose storage for cloud applications, dynamic websites, content distribution, mobile and gaming applications, and big data analytics. |
| **S3 Intelligent-Tiering** | This tier is useful if your data has unknown or changing access patters. S3 Intelligent-Tiering stores objects in three tiers: a frequent access tier, an infrequent access tier, and an archive instance access tier. Amazon S3 monitors access patterns of your data and automatically moves your data to the most cost-effective storage tier based on frequency of access. |
| **S3 Standard-Infrequent Access (S3 Standard-IA)** | This tier is for data that is accessed less frequently but requires rapid access when needed. S3 Standard-IA offers the high durability, high throughput, and low latency of S3 Standard, with a low per-GB storage price and per-GB retrieval fee. This storage tier is ideal if you want to store long-term backups, disaster recovery files, and so on. |
| **S3 One Zone-Infrequent Access (S3 One Zone-IA)** | Unlike other S3 storage classes that store data in a minimum of three Availability Zones, S3 One Zone-IA stores data in a single Availability Zone, which makes it less expensive than S3 Standard-IA. S3 One Zone-IA is ideal for customers who want a lower-cost option for infrequently accessed data, but do not require the availability and resilience of S3 Standard or S3 Standard-IA. It's a good choice for storing secondary backup copies of on-premises data or easily recreatable data. |
| **S3 Glacier Instant Retrieval** | Use S3 Glacier Instant Retrieval for archiving data that is rarely accessed and requires millisecond retrieval. Data stored in this storage class offers a cost savings of up to 68 percent compared to the S3 Standard-IA storage class, with the same latency and throughput performance. |
| **S3 Glacier Flexible Retrieval** | S3 Glacier Flexible Retrieval offers low-cost storage for archived data that is accessed 1–2 times per year. With S3 Glacier Flexible Retrieval, your data can be accessed in as little as 1–5 minutes using an expedited retrieval. You can also request free bulk retrievals in up to 5–12 hours. It is an ideal solution for backup, disaster recovery, offsite data storage needs, and for when some data occasionally must be retrieved in minutes. |
| **S3 Glacier Deep Archive** | S3 Glacier Deep Archive is the lowest-cost Amazon S3 storage class. It supports long-term retention and digital preservation for data that might be accessed once or twice a year. Data stored in the S3 Glacier Deep Archive storage class has a default retrieval time of 12 hours. It is designed for customers that retain data sets for 7–10 years or longer, to meet regulatory compliance requirements. Examples include those in highly regulated industries, such as the financial services, healthcare, and public sectors. |
| **S3 on Outposts** | Amazon S3 on Outposts delivers object storage to your on-premises AWS Outposts environment using S3 API's and features. For workloads that require satisfying local data residency requirements or need to keep data close to on premises applications for performance reasons, the S3 Outposts storage class is the ideal option. |

# 

---

# **Amazon S3 versioning**

As described earlier, Amazon S3 identifies objects in part by using the object name. For example, when you upload an employee photo to Amazon S3, you might name the object *employee.jpg* and store it in a bucket called employees. Without Amazon S3 versioning, every time you upload an object called employee.jpg to the employees bucket, it will overwrite the original object.

This can be an issue for several reasons, including the following:

- **Common names:** The employee.jpg object name is a common name for an employee photo object. You or someone else who has access to the bucket might not have intended to overwrite it; but once it's overwritten, the original object can't be accessed.
- **Version preservation:** You might want to preserve different versions of employee.jpg. Without versioning, if you wanted to create a new version of employee.jpg, you would need to upload the object and choose a different name for it. Having several objects all with slight differences in naming variations can cause confusion and clutter in S3 buckets.

To counteract these issues, you can use Amazon S3 versioning. Versioning keeps multiple versions of a single object in the same bucket. This preserves old versions of an object without using different names, which helps with object recovery from accidental deletions, accidental overwrites, or application failures.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/xwBBNteqRz68ZXSa_86d-BbLx9Y1g9QZN.png

If you enable versioning for a bucket, Amazon S3 automatically generates a unique version ID for the object. In one bucket, for example, you can have two objects with the same key but different version IDs, such as employeephoto.jpg (version 111111) and employeephoto.jpg (version 121212).

By using versioning-enabled buckets, you can recover objects from accidental deletion or overwrite. The following are examples:

- Deleting an object does not remove the object permanently. Instead, Amazon S3 puts a marker on the object that shows that you tried to delete it. If you want to restore the object, you can remove the marker and the object is reinstated.
    
- If you overwrite an object, it results in a new object version in the bucket. You still have access to previous versions of the object.
    

**Versioning states**

Buckets can be in one of three states. The versioning state applies to all objects in the bucket. Storage costs are incurred for all objects in your bucket, including all versions. To reduce your Amazon S3 bill, you might want to delete previous versions of your objects when they are no longer needed.

---

# **Managing your storage lifecycle**

If you keep manually changing your objects, such as your employee photos, from storage tier to storage tier, you might want to automate the process by configuring their Amazon S3 lifecycle. When you define a lifecycle configuration for an object or group of objects, you can choose to automate between two types of actions: transition and expiration.

- **Transition actions** define when objects should transition to another storage class.
- **Expiration actions** define when objects expire and should be permanently deleted.

For example, you might transition objects to S3 Standard-IA storage class 30 days after you create them. Or you might archive objects to the S3 Glacier Deep Archive storage class 1 year after creating them.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720972800/kjTISSVDPO9bHUNsksf1gg/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/1Wmf6ixnfVxsezYv_yJcSJtGhz1K8Fs3r.png

The following use cases are good candidates for the use of lifecycle configuration rules:

- **Periodic logs:** If you upload periodic logs to a bucket, your application might need them for a week or a month. After that, you might want to delete them.
- **Data that changes in access frequency:** Some documents are frequently accessed for a limited period of time. After that, they are infrequently accessed. At some point, you might not need real-time access to them. But your organization or regulations might require you to archive them for a specific period. After that, you can delete them.