# Block Storage with Amazon EC2 instance store and Amazon EBS

## **Amazon EC2 instance store**

Amazon Elastic Compute Cloud (Amazon EC2) instance store provides temporary block-level storage for an instance. This storage is located on disks that are physically attached to the host computer. This ties the lifecycle of the data to the lifecycle of the EC2 instance. If you delete the instance, the instance store is also deleted. Because of this, instance store is considered ephemeral storage. Read more about it in the Amazon EC2 documentation found in the resources section at the end of this lesson.

Instance store is ideal if you host applications that replicate data to other EC2 instances, such as Hadoop clusters. For these cluster-based workloads, having the speed of locally attached volumes and the resiliency of replicated data helps you achieve data distribution at high performance. It’s also ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content.

## **Amazon EBS**

As the name implies, Amazon Elastic Block Store (Amazon EBS) is block-level storage that you can attach to an Amazon EC2 instance. You can compare this to how you much attach an external drive to your laptop. This attachable storage is called an EBS volume. EBS volumes act similarly to external drives in more than one way.

- **Detachable:** You can detach an EBS volume from one EC2 instance and attach it to another EC2 instance in the same Availability Zone to access the data on it.
- **Distinct:** The external drive is separate from the computer. That means that if an accident occurs and the computer goes down, you still have your data on your external drive. The same is true for EBS volumes.
- **Size-limited:** You’re limited to the size of the external drive, because it has a fixed limit to how scalable it can be. For example, you might have a 2 TB external drive, which means you can only have 2 TB of content on it. This also relates to Amazon EBS, because a volume also has a max limitation of how much content you can store on it.
- **1-to-1 connection:** Most EBS volumes can only be connected with one computer at a time. Most EBS volumes have a one-to-one relationship with EC2 instances, so they cannot be shared by or attached to multiple instances at one time.

**AWS announced the Amazon EBS multi-attach feature that permits Provisioned IOPS SSD (io1 or io2) volumes to be attached to multiple EC2 instances at one time. This feature is not available for all instance types, and all instances must be in the same Availability Zone. (Read more about this in the Amazon EBS documentation in the resources section at the end of this lesson.)**

## **Scaling Amazon EBS volumes**

You can scale EBS volumes in two ways. To learn about a category, choose the appropriate tab.

**INCREASE VOLUME SIZE**

**Increase the volume size** only if it doesn’t increase above the maximum size limit. Depending on the volume selected, Amazon EBS currently supports a maximum volume size of 64 tebibytes (TiB). For example, if you provision a 5-TiB io2 Block Express volume, you can choose to increase the size of your volume until you get to 64 TiB.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713952800/7AZkEX2vofB-YL7dB03ENA/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/HUyuu1LCvpIieQkv_nZwyYL3OuW_hyqQY.png

**ATTACH MULTIPLE VOLUMES**

**Attach multiple volumes** to a single EC2 instance. Amazon EC2 has a one-to-many relationship with EBS volumes. You can add these additional volumes during or after EC2 instance creation to provide more storage capacity for your hosts.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713952800/7AZkEX2vofB-YL7dB03ENA/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/aNTLKpW8mfclxoMK_sytu3ehG-qSyNzOw.png

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713952800/7AZkEX2vofB-YL7dB03ENA/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/aNTLKpW8mfclxoMK_sytu3ehG-qSyNzOw.png

## **Amazon EBS use cases**

Amazon EBS is useful when you must retrieve data quickly and have data persist long term. Volumes are commonly used in the following scenarios.

To learn more, expand each of the following four categories.

- Operating Systems
- Databases
- Enterprise Applications
- Big data analytics engines