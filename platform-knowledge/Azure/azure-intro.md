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

