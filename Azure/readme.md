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
## <p align="center" id = "purpose">  Purpose | [Back to ToC](#toc) </p>

<p> 
This guide explains what cloud computing and Microsoft Azure are for educational purposes. The content is organized using the same sections as the official Microsoft course syllabus provided at https://learn.microsoft.com/en-us/training/courses/az-900t00
<br></br>
Much of the wording follows the language used in official Microsoft Learn guides and documentation. Please support the official release.
</p>


<br></br>
## <p align="center" id = "cloud"> What is Cloud Computing? | [Back to ToC](#toc) </p>
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
	High availability ensures IT resources remain accessible <b>if</b> needed.
	When designing solutions, it is important to consider availability guarantees. In Azure, these guarantees are defined by service-level agreements (SLAs) that specify the uptime for each service.  
	> Think: 	High availability is about staying up & focuses on avoiding downtime.
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
		Note: SaaS is usually a monthly or annual subscription

PaaS - <br>
	The cloud provider is responsible for the operating system, physical datacenter, physical hosts, and physical network. 
	In PaaS, the customer is responsible for accounts and identities.
	
	Common Examples:
	- Azure App Service
	- Azure SQL Database
	- Cosmos DB

IaaS - <br>
	Virtual networks are part of the IaaS cloud service.  
	For example, IaaS cloud computing model best categorizes Azure VMs.

Note: Both PaaS and IaaS use a consumption-based model, so you only pay for what you use.
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

## <p align="center" id = "architecture"> Azure Architecture & Services | [Back to ToC](#toc) </p>


## <p align="center" id = "management"> Azure Management and Governance | [Back to ToC](#toc) </p>


THE END! 
There you have it! You were able to successfully learn what is cloud computing and Azure.