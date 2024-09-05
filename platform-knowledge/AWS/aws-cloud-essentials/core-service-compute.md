# Core Service `Compute` 
<aside>
💡 Amazon Elastic Compute Cloud

</aside>

Amazon Elastic Compute Cloud (Amazon EC2) provides scalable computing capacity in the Amazon Web Services (AWS) Cloud. In the compute area, there are various options for the types of resources you might want to launch, such as the following:

- Virtual machines
- Containers
- Batch processing compute resources
- Serverless compute

Amazon EC2 benefits include the following:

- Complete control of your computing resources
- Resizable compute capacity
- Reduced time required to obtain and boot new server instances

- Amazon EC2 is a virtual machine launched on AWS hardware.
- AWS takes care of the hardware, whereas you focus on setting up Amazon EC2 to match your application needs.

The applications you can launch on Amazon EC2 are similar to what you would do on a typical server:

- Websites
- Databases
- Analytical applications and more

When you need compute capacity, you can do the following:

- **Select and configure** the EC2 instance to match your application need and have **complete control** over this resource.
- **Start and stop** this instance when you need or terminate it when you do not need capacity anymore.

If, at some point, you realize you need more or fewer resources to support your app, you have the opportunity to **scale** your machine up or down by changing the EC2 instance type and size.

There are many types of instances, each built to provide a specific set of resources, and they run on certain hardware (including Intel families and Graviton).

There are a broad variety of instance types so that you can do the following:

- Pick the most suitable type of virtual machine for your specific application.
- Match your needs as precisely as possible.

### Instance types

determine your **use case**:

- General purpose
- High performance
- In-memory databases
- Machine learning (ML)
- Distributed file systems

**Memory optimized**

**Examples of the Instance types:** r4, r5, x1, z1

**Use case:** High compute and memory-intensive workloads

**Accelerated computing**

**Examples of the Instance types:** f1, g3, g4, p2, p3

**Use case:** Machine learning and high performance computing

**Storage optimized**

**Examples of the Instance types:** d2, h1, i3

**Use case:** Maximize the number of transactions processed per second (TPS)

**General purpose**

**Examples of the Instance types:** a1, m4, m5, t2, t3

**Use case:** High performance file systems

**Compute optimized**

**Examples of the Instance types:** c4, c5

**Use case:** Network intensive workloads

**HPC optimized**

**Examples of the Instance types:** Hpc6a, Hpc6id

**Use case:** Best price performance for running HPC workloads

More benefits of EC2

- With **dynamic scaling capabilities**, the service will be able to match the demand in a **live manner**, understanding when resources are over-provisioned or under-provisioned based on the CPU utilization or such metrics.
- With Amazon EC2, you can add or remove EC2 instances and unhealthy applications automatically and replace the instances without intervention. However, you do not need to physically monitor and adjust capacities continuously.
- Scale horizontally to precisely match the current demand and avoid over-provisioning or under-provisioning. The process is all done automatically.
- Amazon EC2 Auto Scaling **detects impaired EC2 instances and unhealthy applications** and r**eplaces the instances** without intervention.
- Amazon EC2 Auto Scaling provides several **scaling options: manual, scheduled, dynamic or on demand, and predictive**. When you know that you will have significant (or not enough) traffic in a certain period, you can **schedule** the service to launch the resources in advance to be ready to serve the traffic.
- With the **elasticity** of the cloud, you can also provision the amount of resources to **match the demand as closely as possible**. Also, because cloud resources are disposable, you can be flexible when you launch or remove resources.

---

### Serverless (AWS Lambda)

> **Serverless computing is building and running applications and services without managing servers.**
> 
- With serverless resources, you save time from configuring servers, take care of scaling the capacity with usage, and have built-in availability and fault tolerance.
- Serverless services do not run idle resources, so you pay for what you need.

> **AWS Lambda is a fully managed serverless compute service.**
> 

AWS Lambda benefits include the following:

- It supports multiple languages.
- It runs stateless code.
- When you upload the code in the language you prefer, Lambda can run your code on a schedule or in response to events, such as changes to data in an Amazon Simple Storage Service (Amazon S3) bucket or Amazon DynamoDB table.
- It offers per-millisecond pricing of the code being run.
- It is a great solution to be used in event-driven architectures.
- Provisioning, scaling, and underlying resources are taken care of by Lambda itself.
- It provides high availability.

---

### Container Orchestration (ECS & EKS)

Amazon Elastic Container Service (Amazon ECS) and Amazon Elastic Kubernetes Service (Amazon EKS) are the **container orchestrating services** that help you schedule, maintain, and scale ****
the fleet of nodes running your containers. They also give you a **centralized way of monitoring and controlling** how you want your containers launched.

**Amazon ECS**

Amazon ECS is an AWS container orchestration tool giving you seamless control over your containerized application.

**Amazon EKS**

Amazon EKS is a managed service that you can use to run Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane or nodes. Kubernetes is an open-source system for automating the deployment, scaling, and management of containerized applications.