## Choosing the right compute option

If you’re responsible for setting up servers on AWS to run your infrastructure, you have many compute options. First, you need to know which compute service to use for each use case. 

At a fundamental level, three types of compute options are available: 

- virtual machines (VMs)
- container services
- serverless.

If you have prior infrastructure knowledge, a `virtual machine` will often be the easiest compute option to understand. This is because a virtual machine emulates a physical server and allows you to install an HTTP server to run your applications, for example. To run virtual machines, you install a hypervisor on a host machine. 

In its simplest form, a `hypervisor` is software or firmware that makes it possible to share physical hardware resources across one or more virtual machines. The hypervisor provisions the resources to create and run your VMs.

In AWS, `Amazon Elastic Compute Cloud` (Amazon EC2) is a web service that provides secure and resizable compute capacity in the cloud. You can provision virtual servers called EC2 instances. 

Behind the scenes, AWS operates and manages the host machines and the hypervisor layer. AWS also installs the virtual machine operating system, called the guest operating system.

Beneath the surface, some AWS compute services use Amazon EC2 or use virtualization concepts.

## Getting started with EC2

<aside>
💡 **When architecting any application for high availability, consider using at least two EC2 instances in two separate Availability Zones.**

</aside>

### Amazon EC2

> `Amazon EC2` is a web service that provides secure, resizable compute capacity in the cloud. With this service, you can provision virtual servers called EC2 instances.
> 

With Amazon EC2, you can do the following:

- Provision and launch one or more EC2 instances in minutes.
- Stop or shut down EC2 instances when you finish running a workload.
- Pay by the hour or second for each instance type (minimum of 60 seconds).

To create an EC2 instance, you must define the following:

- **Hardware specifications:** CPU, memory, network, and storage
- **Logical configurations:** Networking location, firewall rules, authentication, and the operating system of your choice

### Amazon Machine Image

> An `AMI` includes the operating system, storage mapping, architecture type, launch permissions, and any additional preinstalled software applications.
> 

#### Relationship between AMIs and EC2

> EC2 instances are live instantiations (or versions) of what is defined in an AMI
> 

you can also see this kind of relationship between a class and an object. In this case, the AMI is how you model and define your instance. The EC2 instance is the entity you interact with, where you can install your web server and serve your content to users.

![relationship-ami-ec2.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/89306d87-fba5-419f-8eb3-bf584d2697e3/7ef58183-3950-4d74-99bb-e180a9aa60f2/relationship-ami-ec2.png)

![ami.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/89306d87-fba5-419f-8eb3-bf584d2697e3/14a94e7d-bcdb-43f4-be70-6da521f31c06/ami.png)

### finding AMI

Each AMI in the AWS Management Console has an AMI ID, which is prefixed by *ami-*, followed by a random hash of numbers and letters. The IDs are unique to each AWS Region.

## configuring EC2

### Amazon EC2 instance types

`EC2 instances` are a combination of virtual processors (vCPUs), memory, network, and, in some cases, instance storage and graphics processing units (GPUs). When you create an EC2 instance, you need to choose how much you need of each of these components.

For example, the instance type `c5n.xlarge` can be broken down as follows:

- **First position –** The first position, **c**, indicates the instance family. This indicates that this instance belongs to the compute optimized family.
- **Second position –** The second position, **5**, indicates the generation of the instance. This instance belongs to the fifth generation of instances.
- **Remaining letters before the period –** In this case, **n** indicates additional attributes, such as local NVMe storage.
- **After the period –** After the period, **xlarge** indicates the instance size. In this example, it's xlarge.

![ec2-instance-example.jpg](https://prod-files-secure.s3.us-west-2.amazonaws.com/89306d87-fba5-419f-8eb3-bf584d2697e3/46ada34d-dc29-4727-ad08-7bee68fc5e39/ec2-instance-example.jpg)

- Instance Families
    
    Each instance family is optimized to fit different use cases. The following table describes instance families and some typical workloads.
    
    | **Instance family** | **Description** | **Use Cases** |
    | --- | --- | --- |
    | **General purpose** | General purpose instances provide a balance of compute, memory, and networking resources, and can be used for a variety of workloads. | Ideal for applications that use these resources in equal proportions, such as web servers and code repositories |
    | **Compute optimized** | Compute optimized instances are ideal for compute-bound applications that benefit from high-performance processors. | Well-suited for batch processing workloads, media transcoding, high performance web servers, high performance computing (HPC), scientific modeling, dedicated gaming servers and ad server engines, machine learning inference, and other compute intensive applications |
    | **Memory optimized** | Memory optimized instances are designed to deliver fast performance for workloads that process large datasets in memory. | Memory-intensive applications, such as high-performance databases, distributed web-scale in-memory caches, mid-size in-memory databases, real-time big-data analytics, and other enterprise applications |
    | **Accelerated computing** | Accelerated computing instances use hardware accelerators or co-processors to perform functions such as floating-point number calculations, graphics processing, or data pattern matching more efficiently than is possible in software running on CPUs. | Machine learning, HPC, computational fluid dynamics, computational finance, seismic analysis, speech recognition, autonomous vehicles, and drug discovery |
    | **Storage optimized** | Storage optimized instances are designed for workloads that require high sequential read and write access to large datasets on local storage. They are optimized to deliver tens of thousands of low-latency random I/O operations per second (IOPS) to applications that replicate their data across different instances. | NoSQL databases (Cassandra, MongoDB and Redis), in-memory databases, scale-out transactional databases, data warehousing, Elasticsearch, and analytics |
    | **HPC optimized** | High performance computing (HPC) instances are purpose built to offer the best price performance for running HPC workloads at scale on AWS. | Ideal for applications that benefit from high-performance processors, such as large, complex simulations and deep learning workloads |

### EC2 instance locations

Unless otherwise specified, when you launch EC2 instances, they are placed in a default virtual private cloud (VPC). The default VPC is suitable for getting started quickly and launching public EC2 instances without having to create and configure your own VPC.

Any resource that you put inside the default VPC will be public and accessible by the internet, so you shouldn’t place any customer data or private information in it.

When you get more comfortable with networking on AWS, you should change this default setting to choose your own custom VPCs and restrict access with additional routing and connectivity mechanisms.

### Architecting for high availability

Although EC2 instances are typically reliable, two are better than one, and three are better than two. Specifying the instance size gives you an advantage when designing your architecture because you can use more smaller instances rather than a few larger ones.

If your frontend only has a single instance and the instance fails, your application goes down. Alternatively, if your workload is distributed across 10 instances and one fails, you lose only 10 percent of your fleet, and your application availability is hardly affected.

When architecting any application for high availability, consider using at least two EC2 instances in two separate Availability Zones. ­­

![high-availability-architecture.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/89306d87-fba5-419f-8eb3-bf584d2697e3/4720f47f-c344-4152-9656-82a0a361d7be/high-availability-architecture.png)

---

## EC2 Instance Lifecycle 🔁

**An EC2 instance transitions between different states from the moment you create it until its termination.**

![ec2-instance-lifecycle.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/89306d87-fba5-419f-8eb3-bf584d2697e3/92d803e3-bf56-4f96-b812-61d1808cad3b/ec2-instance-lifecycle.png)

1. When you launch an instance, it enters the **pending** state. When an instance is pending, billing has not started. At this stage, the instance is preparing to enter the running state. Pending is where AWS performs all actions needed to set up an instance, such as copying the AMI content to the root device and allocating the necessary networking components.
2. When your instance is **running**, it's ready to use. This is also the stage where billing begins. As soon as an instance is running, you can take other actions on the instance, such as reboot, terminate, stop, and stop-hibernate.
3. When you reboot an instance, it’s different than performing a stop action and then a start action. **Rebooting** an instance is equivalent to rebooting an operating system. The instance keeps its public DNS name (IPv4) and private and public IPv4 addresses. An IPv6 address (if applicable) remains on the same host computer and maintains its public and private IP address, in addition to any data on its instance store volumes.
4. When you stop your instance, it enters the **stopping** and then **stopped** state. This is similar to when you shut down your laptop. You can stop and start an instance if it has an Amazon Elastic Block Store (Amazon EBS) volume as its root device. When you stop and start an instance, your instance can be placed on a new underlying physical server. Your instance retains its private IPv4 addresses and if your instance has an IPv6 address, it retains its IPv6 address. When you put the instance into stop-hibernate, the instance enters the stopped state, but saves the last information or content into memory, so that the start process is faster.
5. When you **terminate** an instance, the instance stores are erased, and you lose both the public IP address and private IP address of the machine. Termination of an instance means that you can no longer access the machine. As soon as the status of an instance changes to **shutting down** or **terminated,** you stop incurring charges for that instance.

## **Difference between stop and stop-hibernate**

When you stop an instance, it enters the stopping state until it reaches the stopped state. AWS does not charge usage or data transfer fees for your instance after you stop it. But storage for any Amazon EBS volumes is still charged. While your instance is in the stopped state, you can modify some attributes, like the instance type. When you stop your instance, the data from the instance memory (RAM) is lost.

When you stop-hibernate an instance, Amazon EC2 signals the operating system to perform hibernation (suspend-to-disk), which saves the contents from the instance memory (RAM) to the EBS root volume. You can hibernate an instance only if hibernation is turned on and the instance meets the hibernation prerequisites.

## **Pricing**

One of the ways to reduce costs with Amazon EC2 is to choose the right pricing option for the way that your applications run. AWS offers a variety of pricing options to address different workload scenarios.

- On-demand instances
    
    With On-Demand Instances, you pay for compute capacity per hour or per second, depending on which instances that you run. There are no long-term commitments or upfront payments required. Billing begins whenever the instance is running, and billing stops when the instance is in a stopped or terminated state. You can increase or decrease your compute capacity to meet the demands of your application and only pay the specified hourly rates for the instance that you use.
    
    On-Demand Instances are recommended for the following use cases:
    
    - Users who prefer the low cost and flexibility of Amazon EC2 without upfront payment or long-term commitments
    - Applications with short-term, spiky, or unpredictable workloads that cannot be interrupted
    - Applications being developed or tested on Amazon EC2 for the first time
- Spot instances
    
    For applications that have flexible start and end times, Amazon EC2 offers the Spot Instances option. With Amazon EC2 Spot Instances, you can request spare Amazon EC2 computing capacity for up to 90 percent off the On-Demand price. Spot Instances are recommended for the following use cases:
    
    - Applications that have flexible start and end times
    - Applications that are only feasible at very low compute prices
    - Users with fault-tolerant or stateless workloads
    
    With Spot Instances, you set a limit on how much you want to pay for the instance hour. This is compared against the current Spot price that AWS determines. Spot Instance prices adjust gradually based on long-term trends in supply and demand for Spot Instance capacity. If the amount that you pay is more than the current Spot price and there is capacity, you will receive an instance.
    
- Savings plans
    
    Savings Plans are a flexible pricing model that offers low usage prices for a 1-year or 3-year term commitment to a consistent amount of usage. Savings Plans apply to Amazon EC2, AWS Lambda, and AWS Fargate usage and provide up to 72 percent savings on AWS compute usage.
    
    For workloads that have predictable and consistent usage, Savings Plans can provide significant savings compared to On-Demand Instances. Savings Plans are recommended for the following use cases:
    
    - Workloads with a consistent and steady-state usage
    - Customers who want to use different instance types and compute solutions across different locations
    - Customers who can make monetary commitment to use Amazon EC2 over a 1-year or 3-year term
- Reserved instances
    
    For applications with steady state usage that might require reserved capacity, Amazon EC2 offers the Reserved Instances option. With this option, you save up to 75 percent compared to On-Demand Instance pricing. You can choose between three payment options: All Upfront, Partial Upfront, or No Upfront. You can select either a 1-year or 3-year term for each of these options.
    
    With Reserved Instances, you can choose the type that best fits your applications needs.
    
    - Standard Reserved Instances: These provide the most significant discount (up to 72 percent off On-Demand pricing) and are best suited for steady-state usage.
    - Convertible Reserved Instances: These provide a discount (up to 54 percent off On-Demand pricing) and the capability to change the attributes of the Reserved Instance if the exchange results in the creation of Reserved Instances of equal or greater value. Like Standard Reserved Instances, Convertible Reserved Instances are best suited for steady-state usage.
    - Scheduled Reserved Instances: These are available to launch within the time windows that you reserve. With this option, you can match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day, a week, or a month.
- Dedicated hosts
    
    A Dedicated Host is a physical Amazon EC2 server that is dedicated for your use. Dedicated Hosts can help you reduce costs because you can use your existing server-bound software licenses, such as Windows Server, SQL Server, and Oracle licenses. And they can also help you meet compliance requirements. Amazon EC2 Dedicated Host is also integrated with AWS License Manager, a service that helps you manage your software licenses, including Microsoft Windows Server and Microsoft SQL Server licenses.
    
    - Dedicated Hosts can be purchased on demand (hourly).
    - Dedicated Hosts can be purchased as a Reservation for up to 70 percent off the On-Demand price.