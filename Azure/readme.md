# <p align="center"> Learn Azure Cloud Computing </p>

## Resources/Related Links:
* [Study guide for Exam AZ-900](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-900)
* [AZ-900 Certifications Page](https://learn.microsoft.com/en-us/credentials/certifications/azure-fundamentals/?practice-assessment-type=certification)


<br></br>
## <p id = "toc"> Table of Contents </p>
1. [Purpose](#purpose)
2. [Describe Cloud Concepts](#cloud)
3. [Describe Azure architecture and services](#architecture)
4. [Describe Azure management and governance](#management)


<br></br>
# <p align="center" id = "purpose">  Purpose | [Back to ToC](#toc) </p>

<p> 
This guide explains what cloud computing and Microsoft Azure are for educational purposes. The content is organized using the same sections as the official Microsoft course syllabus provided at https://learn.microsoft.com/en-us/training/courses/az-900t00
<br></br>
Much of the wording follows the language used in official Microsoft Learn guides and documentation. Please support the official release.
</p>


<br></br>
# <p align="center" id = "cloud"> What is Cloud Computing? | [Back to ToC](#toc) </p>
[Source](https://learn.microsoft.com/en-us/training/paths/microsoft-azure-fundamentals-describe-cloud-concepts/)

<p>
Cloud computing is the delivery of IT computing services over the internet, including but not limited to:
	
	- virtual machines, 
	- storage, 
	- databases, 
	- networking, 
	- and advanced services like IoT, machine learning, and AI.

All cloud providers provide compute and storage services.
</p>


<b>Cloud Models | </b>
[Source](https://learn.microsoft.com/en-us/training/modules/describe-cloud-compute/5-define-cloud-models)

<p>

- Public Cloud  
	- Servers and storage are owned and operated by a third-party cloud service provider.
	- Services are offered over the internet and are available to anyone who wants to purchase them.
		> Think: Serverless Computing = Public Cloud
- Private Cloud
	- Servers are used by a single entity and may be hosted from your on site datacenter
	- Private cloud provides much greater control but at a higher cost.
</p>

<b>Benefits of Cloud Computing </b>

<p>

* High Availability -
	High availability ensures IT resources remain accessible -<b>if</b>- needed.  
	- When designing solutions, it is important to consider availability guarantees. In Azure, these guarantees are defined by service-level agreements (SLAs) that specify the uptime for each service.  
	> Think: High availability is about staying up & focuses on avoiding downtime.
* Fault Tolerance -
	Fault tolerance means the system can continue working even -<b>when</b>- parts of it fail. 
* Low Latency means fast response time. The lower the latency, the faster and smoother the user experience feels.
* Predicatability - Predictability in the cloud means being able to plan with confidence to avoid surprises. It applies to both cost and performance (e.g. an application behaves as expected in that it’s fast, stable, and handles load consistently).
* Elasticity is the automatic, real-time adjustment (up/down/in/out) of resources to match sudden, unpredictable workloads  
	> Elasticity = using more resources when you need them, and fewer when you don’t.
* Scalability is the ability to grow resources (up/out) for long-term, predictable demand, often requiring planning. 
	- Vertical scaling means upgrading one server with more CPU or RAM.
	- Horizontal scaling means adding more resources (e.g. adding servers or instances of resources such as virtual machines) so that the traffic is shared among them.
</p>

<p>

<b> Expenditures </b>
* Capital expenditures are one-time expenses that can be deducted over time.  
	> MS Learn Definition: Capital Expenditures refers to upfront costs incurred one time, such as hardware purchases.
* Operational expenditures are billed as you use services and a do not have upfront costs.
</p>


<b> Expense Models | [Source](https://learn.microsoft.com/en-us/training/modules/describe-cloud-compute/6-describe-consumption-based-model?ns-enrollment-type=learningpath&ns-enrollment-id=learn.wwl.microsoft-azure-fundamentals-describe-cloud-concepts) </b>

<p>

- Consumption based model - Charged only for what is used.  
	Think: Utilities e.g. "Try before you buy"  
	For instance, PaaS and IaaS use a consumption-based model, 
	so you only pay for what you use.

- Subscription model - Flat fee every time its used.
</p>


<b> Cloud Service Types | [Source](https://learn.microsoft.com/en-us/training/modules/describe-cloud-service-types/) </b>

<p>
For the exam, memorize the responsibilities of the shared responsibility model:

<img src = "./shared-responsibility-model.svg">
</p>

<p>

SaaS - <br>
	SaaS allows users to connect to and use cloud-based apps over the internet. 
	Common examples are Netflix and Office 365.	
> Note: SaaS is usually a monthly or annual subscription

PaaS - <br />
	The cloud provider is responsible for the operating system, physical datacenter, physical hosts, and physical network. 
	In PaaS, the customer is responsible for accounts and identities.
	
	Common Examples:
	- Azure App Service
	- Azure SQL Database
	- Cosmos DB

IaaS - <br />
	Virtual networks are part of the IaaS cloud service.  
	For example, IaaS cloud computing model best categorizes Azure VMs.

> Note: Both PaaS and IaaS use a consumption-based model, so you only pay for what you use.
</p>

<p> <br>
Recap:

- In SaaS, the cloud provider manages all aspects of the application environment, such as virtual machines, networking resources, data storage, and applications.
- With PaaS, users can focus on application development because the cloud provider handles all the platform management.  
- IaaS is the closest service model to managing physical servers.

Recap Examples:

- Azure App Services and Azure Cosmos DB are PaaS offerings.
- Azure SQL Database is also PaaS database engine.
- Microsoft Office 365 is a SaaS offering.
</p>

<br> <b> Good test questions: </b>

<div>
Q1: In a platform as a service (PaaS) model, which two components are the responsibility of the cloud service provider? 

Q2: You plan to build a new solution in Azure that will use platform as a service (PaaS) products.

What should you use to estimate the monthly costs?  
Answer: Planning 

Q3: Your organization is building a custom application.
	You need to focus on application development rather than configuration and management of servers.
	
Which cloud service model should you use?  
A:	Application development

Q4. Which type of cloud service model is typically licensed through a monthly or annual subscription?  
	A. SaaS

---	
Question: 
	Your organization is building a custom application.
	You need to focus on application development rather than configuration and management of servers.

	Which cloud service model should you use? Select only one answer.
	- infrastructure as a service (IaaS)
	- platform as a service (PaaS)
	- software as a service (SaaS)
	
	Answer: platform as a service (PaaS)
---

---
Question:
	What uses the infrastructure as a service (IaaS) cloud service model?

	Select only one answer.
	- Azure App Services
	- Azure Cosmos DB
	- Azure virtual machines
	- Microsoft Office 365
	
	Answer: Azure virtual machines
---

</div>

# <p align="center" id = "architecture"> Azure Architecture & Services | [Back to ToC](#toc) </p>

[Learn more here](https://learn.microsoft.com/en-us/training/paths/azure-fundamentals-describe-azure-architecture-services/)

### Core Components of Azure

<img src = "./account-scope-levels.png">

Must Memorize:

Management Group  
	└── Subscription  
    	└── Resource Group   
        	└── Resources  
			

- [Section on Azure Accounts](https://learn.microsoft.com/en-us/training/modules/describe-core-architectural-components-of-azure/)
- [Highlight Article](https://learn.microsoft.com/en-us/training/modules/describe-core-architectural-components-of-azure/6-describe-azure-management-infrastructure)

<p>
Creating an Azure account automatically provides one subscription, and more subscriptions can be added later if needed. So keep in mind: An Azure subscription is required to use Azure services.  

> Don't Forget! Using Azure does require an Azure subscription. 

Once a subscription is created, Azure resources can be created and managed i.e. an Azure resource cannot exist without a subscription, since subscriptions acts as the billing and management boundary. Note that resources can only be associated to only one subscription at a time. 

A resource is a manageable item that is available through Azure. Virtual machines, storage accounts, web apps, databases, and virtual networks are examples of resources. In short, everything created/provisioned in Azure is a resource, including a web app as described [here](https://learn.microsoft.com/en-us/training/modules/host-a-web-app-with-azure-app-service/3-exercise-create-a-web-app-in-the-azure-portal?pivots=csharp).
</p>

<p>
<img src = "./resource-group.png">
<br> Resources are combined and grouped into resource groups, which act as a logical container into which Azure resources like web apps, databases, and storage accounts, are deployed and managed. Each resource group contains the actual Azure resources.  

Since resource groups organize resources into a single unit, any action taken on the group, such as deleting it or managing access, applies to all resources within the group.
> Don't forget! Delete a resource group will delete all resources. Resources also inherit permissions assigned to the resource group.
 				
> NOTE: 1 resource group  can deploy multiple resources (even across regions). So one resource group can hold many resources, but each resource can only belong to one group.
			
Lastly, note that in Azure, subscriptions can be grouped into management groups, making management groups sit above subscriptions. They let you manage access, policies, and compliance for many subscriptions at once. Rules applied to a management group automatically affect all its subscriptions, and management groups can be nested for easier organization.

In short, Management groups manage access, policies, and compliance across multiple subscriptions. For example,"Everyone must use MFA” or “No resources outside these regions”
</p>

### Azure Hierarchy Example:
- 1 management group → enforces security rules for all subscriptions  
- 3 subscriptions → Finance, Engineering, Marketing  
- Each subscription has multiple resource groups, one per project
- A resource can be a virtual machine running a team’s development environment


---
Question: True/False?
An account may be associated with multiple subscriptions. 	[Source](https://learn.microsoft.com/en-us/training/modules/describe-core-architectural-components-of-azure/6-describe-azure-management-infrastructure)

	A: TRUE

<img src = "./subscriptions.png">

<br> 
Question:
What logical container is used to combine and organize Azure resources?

	A: Resource Group

Question:
Which two components can be created in an Azure subscription?

	A: Resources/ Resource Group

Question:
What is an Azure Storage account named storage001 an example of?
	
	A: A resource [Source](https://learn.microsoft.com/en-us/training/modules/describe-core-architectural-components-of-azure/3-get-started-azure-accounts)

Question:
What can you use to allow a user to manage all the resources in a resource group?
	
	A: RBAC

Question:
	For which resource does Azure generate separate billing reports and invoices by default? 	

	A: Subscription
	Azure creates a separate billing report and invoice for each subscription, making it easier to organize and manage costs.

---

## Describe Azure physical infrastructure

[Source](https://learn.microsoft.com/en-us/training/modules/describe-core-architectural-components-of-azure/5-describe-azure-physical-infrastructure?ns-enrollment-type=learningpath&ns-enrollment-id=learn.wwl.azure-fundamentals-describe-azure-architecture-services)

<img src = "./region-pairs.png">

MUST MEMORIZE:  
Geography -> Regions -> Availability Zones -> Data Centers

Datacenter = Floors/rooms inside the building (with resources arranged in racks, with dedicated power, cooling, and networking infrastructure).

Availability Zone = Building
> Each availability zone is made up of one or more datacenters.  

> An availability Zone protects against datacenter level failures  
Remember: When you think of Availability Zones, AUTOMATICALLY think that it's used to protecting or managing data centers!

Region = City
> Regions contains at least one, but potentially multiple availability zones that are nearby. Azure regions are designed to offer low-latency network connections for services hosted within those regions.

> List of Azure regions can be found [here](https://learn.microsoft.com/en-us/azure/reliability/regions-list)

Geography = Country / legal boundary

> Remember: Geography > Regions > Zones > Data Centers.

- Example - 
East US has Zone 1, Zone 2, Zone 3 — all in East US, but isolated from each other.
Same region, separate datacenters” ✅
East US ↔ West US
---

Region pairs allow the replication of Azure resources across geographies to help ensure that a secondary region is available in case of any disaster at the primary region.

In short, in a region pair, a region is paired with another region in the same geography.

Geo-distribution can allow you to deploy apps and data to regional datacenters around the globe, thereby ensuring that your customers always have the best performance in their region. 

An availabilty set protects against VM Failures.




### Azure Compute & Network Services

MEMORIZE:
	To manage Azure VMS using the Azure portal:
	<br>portal.azure.com

Azure VMs are managed via portal.azure.com
	Note: By default, azure vms can't communicate with one another.

Virtual machines are software emulations of physical computers. They include a virtual processor, memory, storage, and networking resources. Virtual machines host an operating system, and you can install and run software just like on a physical computer.
>	Note: If VM Is stopped, you still get charged.

Every Azure VM needs an OS disk to boot up with every OS disk being stored on Azure Disk Storage. Without an OS Disk, the VM cannot boot! 
<br> So No disk = no VM.

Each VM has: 
- OS Disk - Windows or Linux (required) 
- Data Disks - Can be added for apps/extra storage, but they’re optional.
 

### Containers (e.g. AKS / Container Apps) 
[Source](https://learn.microsoft.com/en-us/training/modules/describe-azure-compute-networking-services/5-containers?ns-enrollment-type=learningpath&ns-enrollment-id=learn.wwl.azure-fundamentals-describe-azure-architecture-services)

Containers allows you to run multiple applications on a single host, without needing to manage an operating system for each one.
All containers running on a given host use the same OS kernel (the core part of the operating system). This is different from virtual machines, which each run their own full operating system

```
For example, we can use containers to run multiple instances of a web application on a single machine.

During big sales like Black Friday, instead of setting up new VMs to handle extra traffic, you can:

- Spin up more containers to launch new instances of your store app.
- Each container will handle a portion of the incoming web traffic, allowing the app to scale quickly.
```

## Azure Functions
[Source](https://learn.microsoft.com/en-us/training/modules/describe-azure-compute-networking-services/6-functions)

Azure Functions is a serverless computing service that runs your code only when needed, without requiring VMs or containers. It activates in response to events like a request or a timer, and automatically stops when done.

You only pay for the time your function runs. It scales up or down based on demand.

Functions can be:
- Stateless: Each event is like starting fresh.
- Stateful (Durable Functions): Tracks info between events.

It’s great for running small tasks and is flexible if your app needs change.

## Azure App Service
[Source](https://learn.microsoft.com/en-us/training/modules/describe-azure-compute-networking-services/7-describe-application-hosting-options)

Azure App Service is a serverless platform for building and hosting web apps, APIs, mobile backends, and background jobs. It handles infrastructure for you, offering automatic scaling and high availability. App Service supports multiple programming languages (Java, PHP, Python, .NET, etc.) and both Windows and Linux.

## Azure virtual networking
- Service endpoints are used to expose Azure services to a virtual network, 
providing communication between the two. 
- ExpressRoute is used to connect an on-premises network to Azure. 
- NSGs allow you to configure inbound and outbound rules for virtual networks and virtual machines. 
- Peering allows you to connect virtual networks together.
> You can link virtual networks together by using virtual network peering. Peering enables resources in each virtual network to communicate with each other.


VPN gateway?  
It connects an on-premises datacenter to an Azure virtual network
A VPN gateway is a type of virtual network gateway. Azure VPN Gateway instances are deployed to a dedicated subnet of a virtual network. You can use them to connect on-premises datacenters to virtual networks through a Site-to-Site (S2S) VPN connection.
 
Service endpoints are used to expose Azure services to a virtual network, providing communication between the two. 
ExpressRoute is used to connect an on-premises network to Azure. 
NSGs allow you to configure inbound and outbound rules for virtual networks and virtual machines. 
Peering allows you to connect virtual networks together.

Site-to-Site VPN provides encrypted connectivity over the internet, 
while ExpressRoute provides a private (more secure), dedicated connection to Azure.

Site-to-Site 
Azure VPN -> On-Premises VPN

## Azure Storage
LRS = Locally Redundant Storage (datacenter)

ZRS = Zone-redundant storage (Zone)

GRS = Geo-redundant storage (Geographical Region)

[Source](https://learn.microsoft.com/en-us/training/modules/describe-azure-storage-services/3-redundancy)


### Azure Storage Services
- Azure Blob storage - text/binary data 
- Azure Disk Storage provides disks for Azure virtual machines. 
- Azure Files supports mounting file storage shares via the Server Message Block Protocal (SMB).
	- Azure Files offers fully managed file shares in the cloud that are accessible via industry-standard SMB and NFS protocols.
	- Azure Files is like a backend file server
		It's like a folder, but specifically for applications. 
- Azure Queue storage - storing large number of messages (e.g. HTTP or HTTPS calls)
- Table storage = stored large amounts of structured data e.g. NOSQL DATA 


### AZURE DATA STORAGE TIER - Storage tiers
[Source](https://learn.microsoft.com/en-us/azure/storage/blobs/access-tiers-overview)

Storage tiers let you choose how often your data is accessed, so you can balance cost vs speed.

- The Hot storage tier is optimized for storing data that is accessed frequently. 
- The Cool access tier is the "Goldilocks" option, where data is stored in a way that it can tolerate slightly lower availability but still requires high durability, retrieval latency, and throughput characteristics similar to hot data.
- Cold tier - An online tier optimized for storing data that is rarely accessed or modified, but still requires fast retrieval. Data in the cold tier should be stored for a minimum of 90 days. The cold tier has lower storage costs and higher access costs compared to the cool tier.
- The Archive storage tier stores data offline and offers the lowest storage costs, but also the highest costs to rehydrate and access data. 


In Short:
- More access = higher cost
- Less access = lower cost



--- 
Question:
Which Azure Blob storage service tier has the highest storage costs and the fastest access times for reading and writing data?  
Answer: The Hot tier is optimized for storing data that is accessed frequently.

Question:
Which storage tier in Azure Storage delivers the highest cost of data?  
Answer: HOT

Question:
What is the LOWEST cost to store data?  
Answer: Archive

Question:
Which storage service should you use to store thousands of files containing text and images for Storage Type?  
Answer: Azure Blob Storage

## Describe Azure identity, access, and security
Microsoft Entra ID is a cloud-based identity service that manages sign-ins and access to Microsoft and third-party apps, and integrates with on-premises Active Directory.

### Conditional Access 
[Source](https://learn.microsoft.com/en-us/training/modules/describe-azure-identity-access-security/5-conditional-access)  

Conditional Access is a tool that Microsoft Entra ID can use which provides identity signals to determine information about authentication attempts, and then determine whether to block access or require additional verifications, such as MFA.


---

Very simple example of conditional access

- Employee signs in from the office - Allowed
- Same employee signs in from a new country - Require MFA

Conditional Access overall shows how and if a user can sign in, based on certain conditions.
When someone tries to sign in, Azure can look at:
	- Who the user is (user/group)
	- What they’re trying to access (app/resource)
	- Where they’re signing in from (location)
	- What device they’re using
	- Risk level (suspicious sign-in or not)

---

### Azure Role-Based Access Control (RBAC) 
[Source](https://learn.microsoft.com/en-us/training/modules/describe-azure-identity-access-security/6-role-based-access-control)

This lets you control who can access Azure resources and what they can do. It uses roles to give permissions which applys the principle of least privilege. This means users are given only the permissions they need to complete their tasks. Instead of managing individual permissions, Azure RBAC uses predefined roles (like Reader, Owner) that grant specific access levels to resources.

What can you use to allow a user to manage all the resources in a resource group?
	Azure role-based access control (RBAC)

### Zero Trust Model 
[Source](https://learn.microsoft.com/en-us/training/modules/describe-azure-identity-access-security/7-describe-zero-trust-model)  

Zero Trust is a security model that assumes breaches are inevitable and verifies every request, regardless of where it originates, to protect resources.

Remember:  
	- Verify Explicity  
	- Use Least Priveleage of Access/Privelage
		-  The principle of least privilege means restricting access to information to only the level that users need to perform their work. 
	- Assume Breach  


### Defense in Depth
[Source](https://learn.microsoft.com/en-us/training/modules/describe-azure-identity-access-security/8-describe-defense-depth)

Provides several layers of protection to prevent information from being accessed by unauthorized users. A defense in depth strategy uses a series of mechanisms to slow the advancement of an attack that aims to gain unauthorized access to data

The perimeter layer is about protecting an organization's resources from network-based attacks. 

A DDoS attack attempts to overwhelm and exhaust an application's resources.



# <p align="center" id = "management"> Azure Management and Governance | [Back to ToC](#toc) </p>

Azure Advisor provides RECOMMENDATIONS to reduce the cost of Azure resources. So Azure Advisor evaluates Azure resources and makes recommendations
	
	For instance, cost of resources do change!


THE END! 
There you have it! You were able to successfully learn what is cloud computing and Azure.