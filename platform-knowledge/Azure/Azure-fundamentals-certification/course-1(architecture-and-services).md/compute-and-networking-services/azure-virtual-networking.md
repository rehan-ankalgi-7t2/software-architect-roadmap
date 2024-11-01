# Azure Virtual Networks

> `Azure virtual networks` and `virtual subnets` enable Azure resources, such as VMs, web apps, and databases, to communicate with each other, with users on the internet, and with your on-premises client computers.

Azure virtual networks provide the following key networking capabilities:

- Isolation and segmentation
- Internet communications
- Communicate between Azure resources
- Communicate with on-premises resources
- Route network traffic
- Filter network traffic
- Connect virtual networks

Azure virtual networking supports both public and private endpoints to enable communication between external or internal resources with other internal resources.

Here’s a simplified summary of Azure Virtual Networks and their capabilities:

---

### **Azure Virtual Networks Overview**
Azure Virtual Networks (VNets) link Azure resources like VMs, web apps, and databases, enabling communication:
- **Within Azure** (between resources in the same or other VNets)
- **With the Internet** (for public communication)
- **With on-premises networks** (to extend your network into Azure)

### **Key Capabilities of Azure VNets**

1. **Isolation and Segmentation**
   - VNets allow you to create isolated networks with a private IP range.
   - This IP range isn’t internet-routable and can be split into subnets.
   - Azure offers built-in DNS or external DNS options for name resolution.

2. **Internet Communications**
   - Public IP addresses enable internet access for resources.
   - Public load balancers can distribute incoming internet traffic to resources.

3. **Internal Communication between Azure Resources**
   - Resources within a VNet (e.g., VMs, Azure Kubernetes Service) can communicate securely.
   - **Service Endpoints** improve security and routing when connecting VNets to resources like Azure SQL and Storage accounts.

4. **Connecting with On-Premises Resources**
   - **Point-to-site VPN**: Connect individual devices to an Azure VNet.
   - **Site-to-site VPN**: Connects an on-premises network to an Azure VNet.
   - **ExpressRoute**: Private, high-speed connection without using the internet.

5. **Routing Traffic**
   - Azure auto-routes traffic but allows custom routing:
     - **Route tables** define custom rules for traffic between subnets.
     - **Border Gateway Protocol (BGP)** manages routes between Azure and on-premises networks.

6. **Traffic Filtering**
   - **Network Security Groups (NSGs)**: Set rules to allow/block traffic by IP, port, and protocol.
   - **Network Virtual Appliances**: Specialized VMs that can run firewall or WAN optimization services.

7. **Connecting VNets (Virtual Network Peering)**
   - **Peering** connects VNets directly, allowing private communication over Azure’s backbone network.
   - **User-Defined Routes (UDR)**: Set custom routing between subnets or VNets to control traffic flow.

---

These capabilities enable Azure VNets to support both public and private endpoints, enhance security, and provide flexible, scalable networking for cloud and hybrid environments.