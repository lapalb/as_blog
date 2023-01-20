---
layout: post
title: "AWS Cloud Practitioner"
tags:
 -
---
# AWS Certification

1. Certified Cloud Practitioner - 100 USD - CLF-C01 → 15th Jan
2. Developer - Associate - 150 USD - DVA-C01
3. Solution Architect - Associate  - 150 USD - SAA-C03 → 15th March
4. Solution Architect - Professional  - 300 USD - SAP-C02 → 20th May

Link: [https://aws.amazon.com/certification/](https://aws.amazon.com/certification/)

## Certified Cloud Practitioner

[Exam Guide:](https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf) 

[https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf](https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf)

![Screenshot 2023-01-02 at 5.02.14 PM.png](/as_blog/images/Screenshot_2023-01-02_at_5.02.14_PM.png)

![Screenshot 2023-01-02 at 4.59.34 PM.png](/as_blog/images/Screenshot_2023-01-02_at_4.59.34_PM.png)

---

**AWS Cost Explorer:** Free tool for AWS usage based cost forecasting

**AWS Quicksight**: Insightful Business Reporting

**AWS S3 Transfer Acceleration:** fast, easy, and secure transfers of files over long distances between your client and an S3 bucket. Transfer Acceleration takes advantage of Amazon CloudFront’s globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path.

**AWS Certificate Manager:** allows the web administrator to maintain one or several SSL/TLS certificates, both private and public certificates including their update and renewal so that the administrator does not worry about the imminent expiry of certificate

**AWS WAF:** web application firewall that lets you monitor the HTTP and HTTPS requests

**AWS Personal Health Dashboard** provides alerts for AWS services availability & performance which may impact resources deployed in your account

****AWS Config:**** AWS Config can be used to audit, evaluate configurations of AWS resources. If there are any operational issues, AWS config can be used to retrieve configurational changes made to AWS resources that may have caused these issues.

**AWS Database Migration Service:** helps you migrate databases to AWS quickly and securely. The source database remains fully operational during the migration, minimizing downtime to applications that rely on the database.

**Amazon Inspector** enables you to analyze the behavior of your AWS resources and helps you to identify potential security issues.

**Amazon CloudFront** supports country-level location-based web content personalization with a feature called Geolocation Headers.

**AWS Shield** – All AWS customers benefit from the automatic protections of AWS Shield Standard, at no additional charge. AWS Shield Standard defends against most common, frequently occurring network and transport layer DDoS attacks that target your web site or applications

**AWS Shield Advanced** – For higher levels of protection against attacks targeting your web applications running on Amazon EC2, Elastic Load Balancing (ELB), CloudFront, and Route 53 resources, you can subscribe to AWS Shield Advanced. AWS Shield Advanced provides expanded DDoS attack protection for these resources.

**Bastion host** is a server whose purpose is to provide access (SSH access) to a private network from an external network, such as the Internet. It is deployed in a public subnet.

**Internet Gateway** is a horizontally scaled, redundant, and highly available VPC component that allows communication between your VPC and the internet.

**NAT devices (NAT Gateway, Nat Instance)** allow instances in private subnets to connect to the internet, other VPCs, or on-premises networks. It is deployed in a public subnet.

**S3 Glacier Deep Archive** offers the lowest cost storage in the cloud, at prices lower than storing and maintaining data in on-premises magnetic tape libraries or archiving data offsite. Retriveal time is in days

EFS is a regional service.

**Amazon Athena** is a serverless, interactive query service that makes it easy to analyze data in Amazon S3 using SQL

**Amazon Connect** is an omni-channel cloud contact centre which can be setup easily & with low cost. It has following features which helps to provide customers a superior service ,Telephone as a service, High quality Audio, Omni-channel routing, Web & Mobile Chat, Task management, Contact Centre automation, Rules Engine.

**Amazon WorkSpaces** provides a secure managed service for virtual desktops for remote users. It supports both Windows & Linux based virtual desktops for a large number of users.

**Amazon Cognito** can be used to control access to AWS resources from an application.

**Amazon WorkLink** can be used by internal employees to securely access internal websites & applications using mobile phones.

**Lightsail** is packaged in a similar way than Virtual Private Server, making it easy for anyone to start with their own server. It has a simplified management console and many options are tuned with default values that maximize availability and security.

**Elastic Beanstalk** is a service for application developers that provisions an EC2 instance and a load balancer automatically. It creates the EC2 instance, it installs an execution environment on these machines and will deploy your application for you (Elastic Beanstalk support Java, Node, Python, Docker and many others)

**AWS CloudHSM** helps you meet corporate, contractual, and regulatory compliance requirements for data security.

**AWS Codestar:** Build and deploy appplication in AWS

**AWS Code9:** Cloud based IDE

**AWS Cloudguru:** Most expensive line of code

**Amazon Macie:** Tool to protect data in S3

## Analytics

### AWS Glue

AWS Glue is a serverless ETL (extract,transform, and load) service used to categorize data and move them between various data stores and streams.

![Screenshot 2023-01-06 at 5.09.03 PM.png](/as_blog/images/Screenshot_2023-01-06_at_5.09.03_PM.png)

### AWS Datalake

AWS Lake Formation is a cloud service that is used to create, manage and secure data lakes. It automates the complex manual steps required to create data lakes.

Lake Formation is pointed at the data sources, then crawls the sources and moves the data into the new Amazon S3 data lake.

### AWS Redshift

 → fast and petabyte-scale, SQL based data warehouse service used to analyze data easily.

 → supports Online Analytical Processing (OLAP) type of DB workloads, and alalyse them using quicksight

 →  automatically copy snapshots (automated or manual) of a cluster to another AWS Region

### Kinesis Data Streams

→ scalable real-time data streaming service, captures gigabytes of data from sources(website clickstreams, events streams(database and location-tracking), and social media stream)

![Screenshot 2023-01-06 at 5.20.03 PM.png](/as_blog/images/Screenshot_2023-01-06_at_5.20.03_PM.png)

### Amazon Kinesis Data Firehose

 → serverless service used to capture, transform, and load streaming data into data stores and analytics services.

→ synchronously replicates data across three AZs while delivering them to the destinations.

 → Kinesis Data Streams, CloudWatch events can be considered as the source(s) to Kinesis Data Firehose.

![Screenshot 2023-01-06 at 5.14.51 PM.png](/as_blog/images/Screenshot_2023-01-06_at_5.14.51_PM.png)

![Screenshot 2023-01-06 at 5.15.18 PM.png](/as_blog/images/Screenshot_2023-01-06_at_5.15.18_PM.png)

## Application Integration

### AWS Step Functions

→ serverless orchestration service, converts an application's workflow into a series of steps, by combining AWS Lambda functions and other AWS 

→ resembles state machine, output of one step is input for another

→ multiple automation features like routine deployments, upgrades, installations, migrations, patch management, infrastructure selection, and data synchronization

### Amazon EventBridge

→  serverless event bus service that connects applications with data from multiple sources.

### Amazon SNS

### Amazon SQS

→ scale up to 1-10000 messages per second, default retention period of messages is four days and can be extended to fourteen days. Messages have a fixed size of 256KB.

### AWS AppSync

→ serverless service used to build GraphQL API

### Simple Workflow Service

→ coordinate work amongst distributed application components.

AWS X-Ray is a service that allows visual analysis or allows to trace microservices based applications.

Amazon API Gateway is a service tha maintains and secures APIs at any scale. It is categorized as a serverless service of AWS.

![Screenshot 2023-01-06 at 5.41.15 PM.png](/as_blog/images/Screenshot_2023-01-06_at_5.41.15_PM.png)

---

Amazon GameLift is a fully managed service used to deploy, manage, and scale dedicated servers in the cloud for multiplayer games.

Priniciple of Least Privilege: Give user account only those privileges which are essential to perform its intended function.

![Screenshot 2023-01-08 at 4.45.22 PM.png](/as_blog/images/Screenshot_2023-01-08_at_4.45.22_PM.png)

| AWS Audit Manager | Continuously audit your AWS usage to simplify how you assess risk and compliance |
| --- | --- |
| AWS Certificate Manager | Easily provision, manage, deploy, and renew SSL/TLS certificates |
| Amazon Detective | Investigate potential security issues. collects log data from your AWS resources and uses machine learning, statistical analysis, and graph theory to help you visualize and conduct faster and more efficient security investigations. |
| Amazon GuardDuty | Intelligent threat protection for accounts and workloads, reduces risk using intelligent and continuous threat detection of your AWS accounts, data, and workloads. |
| AWS Secrets Manager | Easily rotate, manage, and retrieve database credentials, API keys, and other secrets throughout their lifecycle |
| AWS Security Hub | AWS Security and Compliance Centre |
| AWS Key Management Service | managed service that makes it easy for you to create and manage keys and control the use of encryption across a wide range of AWS services. KMS is a secure and resilient service that uses FIPS 140-2 validated hardware security modules to isolate and protect your keys. |
| AWS CloudHSM | WS CloudHSM provides cloud-based hardware security modules (HSMs) for generating and using your own encryption keys in the AWS Cloud. |
| Amazon Cognito | offers user pools and identity pools. User pools are user directories that provide sign-up and sign-in options for your app users. Identity pools provide AWS credentials to grant your users access to other AWS services. |
| AWS Global Accelerator | AWS Global Accelerator is a service that improves the availability and performance of your applications with local or global users. It provides static IP addresses that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions, and uses the AWS global network to optimize the path from your users to your applications. |
| AWS Cloud Map | Service discovery for cloud resources, Define user-friendly names for your cloud resources so that your applications can quickly and dynamically discover them. |
| AWS App Mesh | Easily monitor and control microservices, standardizes how your microservices communicate, giving you end-to-end visibility and helping to ensure high-availability for your applications. |
| Amazon API Gateway | Amazon API Gateway helps developers to create and manage APIs to back-end systems running on Amazon EC2, AWS Lambda, or any publicly addressable web service. With Amazon API Gateway, you can generate custom client SDKs for your APIs, to connect your back-end systems to mobile, web, and server applications or services. |
| AWS Config | provides a detailed view of the resources associated with your AWS account, including how they are configured, how they are related to one another, and how the configurations and their relationships have changed over time. |
| AWS Compute Optimizer | analyzes the utilization of your AWS compute resources. Based on its findings, it generates recommendations for your resources to reduce cost and improve performance. |
| AWS Control Tower | Set up and govern your multi-account AWS environment
Gain control over your AWS environment with prescriptive guidance. |
| AWS Systems Manager | Gain Operational Insight and Take Action on AWS Resources. View operational data for groups of resources, so you can quickly identify and act on any issues that might impact applications that use those resources. |
| Resource Groups | Find and group your AWS resources by using queries.
You can create unlimited, single-region groups in your account, use your groups to view group-related insights, and automate tasks on group resources. Groups can be based on resource types and tag queries, or AWS CloudFormation stacks. |
| AWS IQ | Complete projects faster with AWS Certified freelancers and AWS partners. Connect with experts quickly and pay directly through AWS. |
| AWS Support | AWS Support helps customers to get quick support from AWS support personnel for any queries on AWS resources or products. |
| AWS Professional | AWS Professional Services is a global team of experts which provides assistance for deploying high performance computing systems using various services in AWS cloud. This team of experts works along with the customer team in achieving goals for business needs by adopting best practices within AWS cloud. |
| AWS Managed services | AWS Managed services can be used to operate AWS infrastructure in a secure & optimised way. |
|  |  |

6 Pillars of Well Architected Framework

![Screenshot 2023-01-11 at 9.17.21 PM.png](/as_blog/images/Screenshot_2023-01-11_at_9.17.21_PM.png)

### AWS Inspector

Monitor Host and Network Configuration of EC2 based on 4 paramater

1. CVEs
2. Network Reachability
3. Security Best Practice
4. CIS OS Configuration benchmark.

For Host scanning, we have to install Inspector agent

### AWS GuardDuty

Analyses Logs from {Cloudtrail, DNS Query}

use ML to fine abnormalities(Sudden privelege escalation, Launching instance in other region)

**AWS Trusted Advisor check**

Cost optimization
Performance
Security
Fault tolerance
Service limits

Amazon EC2 Auto Scaling uses termination policies that determine which Amazon EC2 instance to be terminated first. Based upon different criteria, it terminates instances. Following are some of the pre-defined termination policies.

1. Default
2. AllocationStrategy
3. OldestLaunchTemplate
4. OldestLaunchConfiguration
5. ClosestToNextInstanceHour
6. NewestInstance
7. OldestInstance

### Important Points!

→ Cost Explorer does usage based forecasting, data is available upto 12 months

→ 200 Routing Table per VPC

→ 128 Tib data in Aurora

→ CloudHSM to be used instead of KMS for full control on Hardware

→ Security groups are only permissive, while Policy JSON rule can both allow deny

---

## In-depth Services

### AWS Certificate Manager

→ handles the complexity of creating, storing, and renewing public and private SSL/TLS X.509 certificates and keys that protect AWS websites and applications.

→ provide certificates for your [integrated AWS services](https://docs.aws.amazon.com/acm/latest/userguide/acm-services.html) either by issuing them directly with ACM or by [importing](https://docs.aws.amazon.com/acm/latest/userguide/import-certificate.html) third-party certificates into the ACM management system

→ You can also [export](https://docs.aws.amazon.com/acm/latest/userguide/export-private.html) ACM certificates signed by AWS Private CA for use anywhere in your internal PKI.

AWS offers two options to customers deploying managed X.509 certificates.

→ **AWS Certificate Manager (ACM)**

→ AWS Private CA

ACM is integrated with the following services:

- **Elastic Load Balancing**
- **Amazon CloudFront** – To use an ACM certificate with CloudFront, you must request or import the certificate in the US East (N. Virginia) region.
- **AWS Elastic Beanstalk**
- **Amazon API Gateway**
- **AWS CloudFormation**

### KMS

![https://miro.medium.com/max/400/1*OXx1g7iCGJ3hFxta_WwGoA.png](https://miro.medium.com/max/400/1*OXx1g7iCGJ3hFxta_WwGoA.png)

KMS Logo — [https://bit.ly/3av1eyN](https://bit.ly/3av1eyN)

- KMS is a managed service that allows you to create and control encryption keys (C*ustomer Master Keys*).
- Can integrate with most other AWS services to increase security and make it easier to encrypt your data.
- Allows you to control access to the keys using things like IAM policies or key policies.
- Provides you with a central place to manage all keys.
- Encrypt/decrypt up to 4KB.
- Pay per API call.
- Validated under **FIPS 140–2** **(Level 2 )** security standard.

**Types of Customer Master Keys (CMKs)**

1. **Customer Managed CMKs** → Keys that you have created in AWS, that you own and manage. You are responsible for managing their key policies, rotating them and enabling/disabling them.
2. **AWS Managed CMKs** → These are free and are created by an AWS service on your behalf and are managed for you. However, only that service can use them.
3. **AWS Owned CMKs** → owned and managed by AWS and shared across many accounts.

### CloudHSM

- Dedicated cloud-based hardware security module for creating, using and managing your own encryption keys in AWS.
- Conforms to **FIPS 140–2 (level 3)** security standard
- No access to the AWS managed component and AWS does not have visibility or access to your keys.
- Works with industry standard APIs, there are no AWS APIs for HSM
- CloudHSM runs within a VPC in your account
- Keys are irretrievable if lost and can not be recovered.

### ****AWS IAM & Billing****

IAM is global

**Users** → Individual users, e.g. employees

**Groups** → A collection of users. Groups allow you to define permissions for all the users within it.

**Policies** → Determine what a user, group or role can or cannot do. Policy Documents are in JSON format.

**Roles** → Allows one service to access another service.

**AWS Budgets** → Lets you quickly create custom budgets that will automatically alert you when your cost exceeds entered amount.