# Azure Networking

## Azure Virtual Network(VNet)
- It is own private network in the cloud, it's like the local network(LAN) you might have at home or in an office
- You can use it to connect Azure resources like virtual machines(VMs), databases, and web apps securely
- Three basic parts
    1. The main overall network permitter
    2. The NSG(Network security group): Protect our resources on the network
    3. The subnet(this is where our vms live)
- It's a safe space where your stuff like virtual machines and apps can talk to each other securely, this is our larger main network


## Isolation and Security
- Your vNet is isolated from other networks in Azure, ensuring your resources are secure and private

## Resource Grouping
- You can put different Azure resources like virtual machines(VMs), databases, and web apps into the same vNet so they can communicate with each other

## Control
- You have control over the IP addresses, subnets, and security settings within your vNet and you can decide the layout and network IP addresses

## Connectivity
- You can connect your vNet to your on premises network, other vNets, or the internet, allowing for flexible and scalable networking options

## Subnets
- It is a smallet network within a larger virtual network(VNet)
- Think of rooms within a house, as each room represents a subnet, it's a smaller section of the vNet(the house) where you can group resources together, these resources could be virtual machines(VMs), databases, or other services, it helps keep things organized

## IP Address range
- Each subnet has its own rage of IP addresses, as this  helps organize and manage network traffic within the vNet

## Isolation and Security
- Subnets help isolate different parts of your network for security and performance reasons
- For example: You might have one subnet for web servers and another for databases, ensuring that only the web servers can directly access the databases

## What does subnet do?
1. Organize resources
2. Control traffic


## Network Security Groups(NSG)
- This is a crucial components in Azure for controlling inbound and outbound traffic to network interfaces(NIC), Virtual Machines(VMs), and subnet instances within Azure Virutal Networks(VNet)
- It works based on rules that you define, allowing or denying traffic based on several parameters like source IP address, destination IP address, port number, and protocol and these rules can be applied at the subnet level or directly to individual VMs
- It serve as a basic virtual firewall for your Azure resources, helping to secure your network traffic within Azure
- Apply the least privilege principle when creating security rules, allowing only necessary traffic, and regular audit and review NSG rules to ensure they meet current security requirements and remove any unnecessary rules
- Use clear and consistent naming conventions for NSGs and their rules to make management easier
You can use NSGs to allow or deny traffic to specific Azure ressources based on source IP address, destination IP address, port and protocol
- Whenever virtual machine is created, one NSG is automatically created and attached to the respective VM


## Azure Firewall
- A fully managed, stateful network security service designed to protect Azure Virtual Network(VNet) resources and provide centralized security for your environment
-  Analyzes the full context of traffic, application rules, network rules, leverages microsoft, threat intelligence to alert and block malicious traffic
- Provides a single point to  manage and monitor firewall rules for multiple v-Nets, works with TCP, UDP, HTTP/S, and other common protocols
- Integrates with Azure monitor, Azure Sentinel, and storage accounts for detailed logging and analytics, enforces compliance requirements across your Azure environment

## Azure NSG
- A basic, stateful network security control used to filter traffic at the network layer for Azure resources like VMs, load balancers, or subnets
- Controls inbound and outbound traffic to/from resources, and rules are based on source/destination IPs, ports and protocols
- Each rule has a priority(lower number have higher priority), determining the order of application and tracks connection state and applies rules only for new traffic flows
- Can be applied at the NIC or subnet level and is included as part of Azure VNet functionality with no additional charge


## Azure Firewall
- When you need advanced security features, centralized management, and protection against both inbound and outbound threats across multiple v-Nets

## Azure NSG
- when you need lightweight, cost-effective, and simple traffic filtering at the subnet or NIC level

- **In many cases, these two services are used together, with NSGs controlling traffic at the subnet or NIC level and Azure Firewall providing more advanced, centralized protection**

