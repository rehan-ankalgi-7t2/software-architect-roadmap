# Amazon VPC Security 🔒

> **Cloud security at AWS is the highest priority. You benefit from a data center and network architecture that is built to meet the requirements of the most security-sensitive organizations.**
> 

## **Secure subnets with network access control lists (Network ACLs)**

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713798000/P8kY5be_AfKIyOY6LQFXgQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/XzSTAuPBQu9e1zDf_mc0ohrPRO6iK9bfX.png

Think of a network access control list (network ACL) as a virtual firewall at the subnet level. A network ACL lets you control what kind of traffic is allowed to enter or leave your subnet. You can configure this by setting up rules that define what you want to filter. Here is an example of a default ACL for a VPC that supports IPv4.

Expand the following block for an example of a default network ACL.

- Default Network ACL
    - *Note: For users with screen readers, use table mode to read the table.
    
    | **Inbound** |  |  |  |  |  |
    | --- | --- | --- | --- | --- | --- |
    | **Rule #** | **Type** | **Protocol** | **Port Range** | **Source** | **Allow or Deny** |
    | 100 | All IPv4 traffic | All | All | 0.0.0.0/0 | ALLOW |
    | * | All IPv4 traffic | All | All | 0.0.0.0/0 | DENY |
    
    | **Outbound** |  |  |  |  |  |
    | --- | --- | --- | --- | --- | --- |
    | **Rule #** | **Type** | **Protocol** | **Port Range** | **Destination** | **Allow or Deny** |
    | 100 | All IPv4 traffic | All | All | 0.0.0.0/0 | ALLOW |
    | * | All IPv4 traffic | All | All | 0.0.0.0/0 | DENY |
    
    The default network ACL shown in the preceding table, allows all traffic in and out of the subnet. To allow data to flow freely to the subnet, this is a good starting place.
    
    However, you might want to restrict data at the subnet level. For example, if you have a web application, you might restrict your network to allow HTTPS traffic and Remote Desktop Protocol (RDP) traffic to your web servers.
    
    Expand the following block or an example of a custom network ACL.
    
- custom Network ACL
    - *Note: For users with screen readers, use table mode to read the table.
    
    | **Inbound** |  |  |  |  |  |
    | --- | --- | --- | --- | --- | --- |
    | **Rule #** | **Source IP** | **Protocol** | **Port** | **Allow or Deny** | **Comments** |
    | 100 | All IPv4 traffic | TCP | 443 | ALLOW | Allows inbound HTTPS traffic from anywhere |
    | 130 | 192.0.2.0/24 | TCP | 3389 | ALLOW | Allows inbound RDP traffic to the web servers from your home network’s public IP address range (over the internet gateway) |
    | * | All IPv4 traffic | All | All | DENY | Denies all inbound traffic not already handled by a preceding rule (not modifiable) |
    
    | **Outbound** |  |  |  |  |  |
    | --- | --- | --- | --- | --- | --- |
    | **Rule #** | **Destination IP** | **Protocol** | **Port** | **Allow or Deny** | **Comments** |
    | 120 | 0.0.0.0/0 | TCP | 1025-65535 | ALLOW | Allows outbound responses to clients on the internet (serving people visiting the web servers in the subnet) |
    | * | 0.0.0.0/0 | All | All | DENY | Denies all outbound traffic not already handled by a preceding rule (not modifiable) |
    
    Notice that in the custom network ACL in the preceding example, you allow inbound 443 and outbound range 1025–65535. That’s because HTTPS uses port 443 to initiate a connection and will respond to an ephemeral port. Network ACLs are considered stateless, so you need to include both the inbound and outbound ports used for the protocol. If you don’t include the outbound range, your server would respond but the traffic would never leave the subnet.
    

Because network ACLs are configured by default to allow incoming and outgoing traffic, you don’t need to change their initial settings unless you need additional security layers.

## **Secure EC2 instances with security groups**

The next layer of security is for your EC2 instances. Here, you can create a virtual firewall called a security group. The default configuration of a security group blocks all inbound traffic and allows all outbound traffic.

By default, a security group only allows outbound traffic. To allow inbound traffic, you must create inbound rules.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713798000/P8kY5be_AfKIyOY6LQFXgQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/Zo6nSROnpaximj9X_LHSo8q3H-_Wuu73H.jpg

You might be wondering, “Wouldn’t this block all EC2 instances from receiving the response of any customer requests?” Well, security groups are stateful. That means that they will remember if a connection is originally initiated by the EC2 instance or from the outside, and temporarily allow traffic to respond without modifying the inbound rules.

If you want your EC2 instance to accept traffic from the internet, you must open up inbound ports. If you have a web server, you might need to accept HTTP and HTTPS requests to allow that type of traffic into your security group. You can create an inbound rule that will allow port 80 (HTTP) and port 443 (HTTPS), as shown.

Expand the block below for security group inbound rules.

- Security Group inbound rules
    - *Note: For users with screen readers, use table mode to read the table.
    
    | **Inbound rules** |  |  |  |
    | --- | --- | --- | --- |
    | **Type** | **Protocol** | **Port Range** | **Source** |
    | HTTP (80) | TCP (6) | 80 | 0.0.0.0/0 |
    | HTTP (80) | TCP (6) | 80 | ::/0 |
    | HTTPS (443) | TCP (6) | 443 | 0.0.0.0/0 |
    | HTTPS (443) | TCP (6) | 443 | ::/0 |
    

You learned earlier that subnets can be used to segregate traffic between computers in your network. Security groups can be used in the same way. A common design pattern is to organize resources into different groups and create security groups for each to control network communication between them.

## Example:

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713798000/P8kY5be_AfKIyOY6LQFXgQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/lFxYBoH9XzTcCsll_scxJIDNUzFAqjZbL.jpg

This example defines three tiers and isolates each tier with defined security group rules. In this case, internet traffic to the web tier is allowed over HTTPS. Web tier to application tier traffic is allowed over HTTP, and application tier to database tier traffic is allowed over MySQL. This is different from traditional on-premises environments, in which you isolate groups of resources with a VLAN configuration. In AWS, security groups allow you to achieve the same isolation without tying the security groups to your network.

## **Resources**

For more information, see the following resources.

- AWS user guide: [Configure Route Tables(opens in a new tab)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
- AWS user guide: [Example Routing Options(opens in a new tab)](https://docs.aws.amazon.com/vpc/latest/userguide/route-table-options.html)
- AWS user guide: [Working with Route Tables(opens in a new tab)](https://docs.aws.amazon.com/vpc/latest/userguide/WorkWithRouteTables.html)
- AWS user guide: [Control Traffic to Subnets Using Network ACLs(opens in a new tab)](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html)
- AWS user guide: [Control Traffic to Resources Using Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)

---

# Amazon VPC demonstration (module demonstration)

[Self-paced digital training on AWS - AWS Skill Builder](https://explore.skillbuilder.aws/learn/course/1851/play/85986/aws-technical-essentials;lp=1044)