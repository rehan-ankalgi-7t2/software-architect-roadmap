# Azure Fundamentals

## Shared Responsibility model
![shared responsibility model image](https://learn.microsoft.com/en-us/training/wwl-azure/describe-cloud-compute/media/shared-responsibility-b3829bfe.svg)

When using a cloud provider, you’ll always be responsible for:
- The information and data stored in the cloud
- Devices that are allowed to connect to your cloud (cell phones, computers, and so on)
- The accounts and identities of the people, services, and devices within your organization

The cloud provider is always responsible for:
- The physical datacenter
- The physical network
- The physical hosts

Your service model will determine responsibility for things like:
- Operating systems
- Network controls
- Applications
- Identity and infrastructure

## benefits of high availability and scalability in the cloud
> When building or deploying a cloud application, two of the biggest considerations are uptime (or availability) and the ability to handle demand (or scale).

### High availability
> High availability focuses on ensuring maximum availability, regardless of disruptions or events that may occur.
- Azure is a highly available cloud environment with uptime guarantees depending on the service. These guarantees are part of the `service-level agreements (SLAs)`.
[Azure SLAs explained](https://www.youtube.com/embed/oHdRvN5rIaw?si=rlAmPOEMtdVJ1qhY)

### Scalability
> Scalability refers to the ability to adjust resources to meet demand
#### Vertical scaling
With vertical scaling, if you were developing an app and you needed more processing power, you could vertically scale up to add more CPUs or RAM to the virtual machine. Conversely, if you realized you had over-specified the needs, you could vertically scale down by lowering the CPU or RAM specifications.

#### Horizontal scaling
With horizontal scaling, if you suddenly experienced a steep jump in demand, your deployed resources could be scaled out (either automatically or manually). For example, you could add additional virtual machines or containers, scaling out. In the same manner, if there was a significant drop in demand, deployed resources could be scaled in (either automatically or manually), scaling in.

## benefits of reliability and predictability in the cloud
### Reliability
> Reliability is the ability of a system to recover from failures and continue to function.
> Predictability in the cloud lets you move forward with confidence. Predictability can be focused on performance predictability or cost predictability

#### Performance Predictability
Performance predictability focuses on predicting the resources needed to deliver a positive experience for your customers. Autoscaling, load balancing, and high availability are just some of the cloud concepts that support performance predictability

#### Cost Predictibility
Cost predictability is focused on predicting or forecasting the cost of the cloud spend. With the cloud, you can track your resource use in real time, monitor resources to ensure that you’re using them in the most efficient way, and apply data analytics to find patterns and trends that help better plan resource deployments

## Infrastructure as a Service (IaaS)
- Infrastructure as a service (IaaS) is the most flexible category of cloud services, as it provides you the maximum amount of control for your cloud resources. 
- In an IaaS model, the cloud provider is responsible for maintaining the hardware, network connectivity (to the internet), and physical security.
- You’re responsible for everything else: operating system installation, configuration, and maintenance; network configuration; database and storage configuration; and so on.
- With IaaS, you’re essentially renting the hardware in a cloud datacenter, but what you do with that hardware is up to you.

Some common scenarios where IaaS might make sense include:
- **Lift-and-shift migration**: You’re setting up cloud resources similar to your on-prem datacenter, and then simply moving the things running on-prem to running on the IaaS infrastructure.
- **Testing and development**: You have established configurations for development and test environments that you need to rapidly replicate. You can start up or shut down the different environments rapidly with an IaaS structure, while maintaining complete control.

## Platform as a Service (PaaS)
- Platform as a service (PaaS) is a middle ground between renting space in a datacenter (infrastructure as a service) and paying for a complete and deployed solution (software as a service).
- In a PaaS environment, the cloud provider maintains the physical infrastructure, physical security, and connection to the internet. They also maintain the operating systems, middleware, development tools, and business intelligence services that make up a cloud solution.
- In a PaaS scenario, you don't have to worry about the licensing or patching for operating systems and databases.
- PaaS is well suited to provide a complete development environment without the headache of maintaining all the development infrastructure.

### Some common scenarios where PaaS might make sense include:
- **Development framework**: PaaS provides a framework that developers can build upon to develop or customize cloud-based applications. Similar to the way you create an Excel macro, PaaS lets developers create applications using built-in software components. Cloud features such as scalability, high-availability, and multi-tenant capability are included, reducing the amount of coding that developers must do.
- **Analytics or business intelligence**: Tools provided as a service with PaaS allow organizations to analyze and mine their data, finding insights and patterns and predicting outcomes to improve forecasting, product design decisions, investment returns, and other business decisions.

## Software as a Service (SaaS)
- Software as a service (SaaS) is the most complete cloud service model from a product perspective. 
- With SaaS, you’re essentially renting or using a fully developed application. Email, financial software, messaging applications, and connectivity software are all common examples of a SaaS implementation.
- While the SaaS model may be the least flexible, it’s also the easiest to get up and running. It requires the least amount of technical knowledge or expertise to fully employ.

### Some common scenarios for SaaS are:
- Email and messaging.
- Business productivity applications.
- Finance and expense tracking.
