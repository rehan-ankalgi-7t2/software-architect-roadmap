# Core service `Networking`
## Amazon VPC

- Amazon VPC is your **private network** **space** you create to **launch your resources** in the AWS Cloud.
- **More than one VPC** can be launched into your AWS accounts.

**A private network that provides logical isolation for your workloads**

- This private network is **logically isolated** from other VPC or remote networks; for *example, isolating development from testing.*
- You can **control** **the traffic** that can flow in and out of Amazon VPC and the resources launched within.
- You can also control how to **connect your VPC with other networks.**

**Custom access controls and security settings for your resource**

- You can use different VPCs to **launch different workloads or stages or workloads** if you want to benefit from such logical isolation.
- You configure how the **packets travel through the layers of your network**.

## Amazon Route 53

> **Amazon Route 53 is a highly available and scalable cloud DNS service.**
> 

Route 53 has various benefits:

- Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service.
- You can use Route 53 to perform three main functions in any combination: domain registration, DNS routing, and health checking.
- DNS translates domain names into IP addresses.
- With Route 53, you can purchase and manage domain names and configure DNS settings.
- Route 53 has multiple routing options.

<aside>
💡 Amazon Route 53 is a highly available and scalable DNS web service. Route 53 connects user requests to internet applications running on AWS or on premises.

</aside>

### Elastic Load Balancing (EBS)

<aside>
💡 Amazon Route 53 is a DNS service. Elastic Load Balancing (ELB) is the load balancing service.

</aside>

Elastic Load Balancing is a web service that improves an application's availability by distributing incoming traffic between two or more EC2 instances. ELB automatically distributes incoming application traffic across multiple targets and virtual appliances in one or more Availability Zones (AZs).

It also serves as a single point of contact with your application. As a result, your end users do not need to be aware of how many machines your application is running on or all the details, such as the IP addresses of those machines.