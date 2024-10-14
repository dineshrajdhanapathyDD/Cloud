## 1. Which AWS service can be used to reduce compliance scope by offloading the responsibility of managing and securing physical infrastructure, network infrastructure, and hypervisors?

Amazon EC2 is a web service that provides resizable compute capacity in the cloud. By using Amazon EC2, AWS customers can reduce their compliance scope by offloading the responsibility of managing and securing physical infrastructure, network infrastructure, and hypervisors. This allows customers to focus on their core business instead of worrying about the underlying infrastructure.

[Documentation](https://aws.amazon.com/ec2/)

### Amazon Elastic Compute Cloud (EC2)

## 2. What are the different types of cloud deployment models that can be used for each execution?

The different types of cloud deployment models are On-Premise, Public, and Hybrid Cloud. In private cloud, services are provided on a private network, while in public cloud, services are provided over a public network. In hybrid cloud, the services are maintained on both private and public networks at the same time. Hence, option A is the correct answer. “Infrastructure as a Service (IaaS), Platform as a Service (PaaS)…” refers to the different types of cloud service models, not cloud deployment models. Cloud Native, Multi-Cloud, and Hybrid Cloud are cloud strategies and not deployment models. Infrastructure as Code (IaC), Functions as a Service (FaaS), and Containers as a Service (CaaS) , which are cloud application development services, not cloud deployment models.

[Documentation](https://aws.amazon.com/types-of-cloud-computing/)

### ans- On-Premise, Public, and Hybrid Cloud

## 3. Which AWS service is designed to provide scalable, stateful firewall protection for your Virtual Private Cloud (VPC)?

AWS Network Firewall is a managed service that allows you to deploy essential network protections for all of your Amazon Virtual Private Clouds (VPCs). It is designed to provide scalable, stateful firewall protection for your VPCs, helping to protect your network against unauthorized and malicious access, and ensuring data privacy and integrity. The service can be customized with fine-grained policies to meet the specific security requirements of your applications, facilitating robust network security and compliance.

While AWS WAF is focused on protecting web applications from various attacks, AWS Shield is a managed DDoS protection service, and Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS.

### ans- AWS Network Firewall

## 4. In the context of AWS End User Computing, which service allows you to stream desktop applications securely to a web browser?

Amazon AppStream 2.0 is a fully managed non-persistent desktop and application virtualization service that allows you to stream desktop applications to any computer running a web browser. This service is designed to provide users with instant access to their desktop applications from anywhere, enhancing mobility and productivity. It securely delivers applications to a web browser, without downloading or installing them locally, thus maintaining security and compliance.

While Amazon WorkSpaces offers a cloud-based virtual desktop experience, AWS Lambda is a serverless compute service, and AWS Elastic Beanstalk is an easy-to-use service for deploying and scaling web applications and services.

### ans - Amazon AppStream 2.0

## 5. What is the behavior of Reserved Instances in AWS Organizations on each execution?

Reserved Instances in AWS Organizations provide capacity reservation and significant discounts on your Amazon EC2 usage. These benefits are applicable across all the accounts in your AWS Organization. The billing benefit applies to usage in all of your accounts. So, if you have Reserved Instances in your master account, the reservations automatically apply to usage across all member accounts.

### ans - The Reserved Instances are shared between all accounts in the organization.

## 6. Which of the following is true about the different compute families on AWS?

The different compute families on AWS are designed to optimally support various types of workloads. Instances within a compute family share similar compute, memory, and network capabilities, while instances across different compute families have different specifications. For example, the M family is optimized for general-purpose workloads, while the C family is optimized for compute-intensive workloads. Similarly, the R family is optimized for memory-intensive workloads, and the X family is optimized for high-performance computing. Therefore, similar capabilities is the correct answer.

“…identical compute, memory, and network capabilities…” is incorrect because there are different compute families on AWS with different specifications.

“…only one compute family available on AWS” is incorrect because there are multiple compute families available on AWS.

“…optimized for the same size of workload” is incorrect because instances within a compute family are optimized for different-sized workloads, not the same workload.

[Documentation](https://aws.amazon.com/ec2/instance-types/)

### ans - Instances within a compute family have similar compute, memory, and network capabilities but with different capacities.

## 7. Which of the following statements is true about AWS Pricing API?

AWS Pricing API is a free service that provides customers with real-time pricing information for various AWS services, along with all the possible combinations offered by the services. This enables customers to make informed decisions about the cost of using a particular configuration or combination of services.

### ans - AWS Pricing API provides real-time pricing information for services.

## 8. Which AWS service utilizes machine learning to discover, classify, and protect sensitive data?

### ans - Amazon Macie

## 9. Which AWS resource provides on-demand downloads of AWS security and compliance documents?

AWS Artifact is a portal that provides access to AWS compliance reports, so customers can track the security and compliance controls in place that are relevant to their data. One of the controls that AWS Artifact provides is the list of recognized available compliance controls for HIPAA, SOCs, and other regulations. Amazon Glacier, Amazon EC2, and AWS Lambda are all AWS services, but they do not provide access to the AWS Artifact portal or compliance reports.

### ans  - AWS Artifact

## 10. What is consolidated billing in AWS?

Consolidated billing is a feature of AWS Organizations that allows multiple AWS accounts to be billed together as a single entity, simplifying payment and cost allocation for organizations with multiple accounts. This feature can help organizations gain a better overall view of their AWS usage and reduce administrative overhead.

A feature that bills different services separately for each AWS account is incorrect as consolidated billing bills the same services together for all accounts.

A feature that allows billing in different regions and currencies is incorrect as consolidated billing does not allow billing in different regions and currencies.

A feature that applies a discount to the billing of a single AWS account is incorrect as consolidated billing does not apply a discount to a single AWS account's billing.

[Documentation](https://aws.amazon.com/organizations/features/consolidated-billing/)

### ans  - A feature that allows multiple AWS accounts to be billed together as a single entity

## 11. In AWS, which security feature ensures that data is encrypted while being stored, providing an additional layer of data protection?

Encryption at Rest in AWS refers to the security feature that ensures data is encrypted while being stored, providing an additional layer of data protection. It helps in safeguarding the data from unauthorized access and meets regulatory compliance needs by encrypting sensitive data before it is saved to storage.

### ans - Encryption at Rest

## 12. Which AWS service facilitates the preparation, processing, and analysis of large datasets using machine learning?

AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it simple and cost-effective to categorize your data, clean it, enrich it, and move it reliably between various data stores. It also provides the Glue DataBrew, which allows data exploration and experimentation directly from AWS data lakes, data warehouses, and databases. It facilitates the preparation and loading of data for analytics and machine learning.

While AWS Data Pipeline is a web service for orchestrating regular data movements and data transformations, Amazon Lex is a service for building conversational interfaces into any application using voice and text. AWS Lambda, on the other hand, is a serverless compute service that lets you run your code without provisioning or managing servers.

### ans - AWS Glue

## 13. Which of the following is considered a best practice for Security and Compliance in the AWS Partner Systems Integrator domain?

The correct answer is: Conducting continuous monitoring and auditing of partner integrator access and activity. This is important as partner integrators may have access to sensitive customer data and systems. Continuous monitoring and auditing helps ensure that access is granted only as needed and that any unauthorized activity is quickly detected and addressed.

### ans - Conducting continuous monitoring and auditing of partner integrator access and activity

## 14. Which of the following is NOT a benefit of using Elasticity in AWS?

Elasticity refers to the ability of an IT infrastructure to quickly and easily scale resources up or down depending on demand. The benefits of Elasticity in AWS include cost savings, scalability, and high availability. However, Security is not a benefit of Elasticity. While Elasticity can help mitigate against failure, it is not the same as increasing security.

[Documentation](https://aws.amazon.com/elasticity/)

### ans - Security

## 15. What component of AWS Trusted Advisor performs security checks on each execution?

Security checks are a component of AWS Trusted Advisor on each execution. AWS Trusted Advisor scans your AWS environment and provides recommendations to help optimize cost, improve fault tolerance, increase performance, and enhance security. The Security check provides recommendations for securing your AWS resources, covering areas such as IAM, data protection, network security, and logging. Therefore, option D is the correct answer.

### ans - Security

## 16. Which AWS service provides a managed business email and calendar service, facilitating secure and easy control of both?

AWS WorkMail is a managed business email and calendar service with support for existing desktop and mobile email client applications. It gives users the ability to seamlessly access their email, contacts, and calendars using the client application of their choice, including Microsoft Outlook, native iOS and Android email applications, any client application supporting the IMAP protocol, or directly through a web browser. It integrates with your existing corporate directory and allows you to set up interoperability with Microsoft Exchange Server, thereby facilitating secure and easy control of both email and calendar.

Amazon WorkDocs is a fully managed, secure content creation, storage, and collaboration service. AWS Chime is a communications service that unifies communications, initiates video conferences, and facilitates file sharing. Amazon Connect is a cloud-based contact center solution.

### ans - AWS WorkMail

## 17. Which statement best describes the concept of least privileged access on each execution in AWS?

The concept of least privileged access on each execution in AWS means providing users with the minimum access privileges necessary to perform their job functions. This ensures that users have access only to the resources they need to perform their work and nothing more, reducing the risk of accidental or intentional misuse of resources. Providing users with access privileges beyond what they need can lead to security vulnerabilities. Providing the same access privileges to all users is not an effective approach since not all users require the same level of access. Providing users with unlimited access privileges is not a viable option since this could result in unauthorized access and misuse of resources.

[Documentation](https://aws.amazon.com/blogs/security/techniques-for-writing-least-privilege-iam-policies/)

### ans  - Providing users with the minimum access privileges necessary to perform their job functions

## 18. Which architecture approach is preferred in AWS Cloud Concepts for decoupling components: monolithic or decoupled?

Decoupling components is one of the key principles in cloud computing and AWS recommends using a decoupled architecture approach to gain benefits such as improved scalability, reliability, and flexibility. Decoupled architecture allows for loosely coupled services that can be modified and deployed independently without affecting the other parts of the stack. Monolithic architecture, on the other hand, presents several challenges such as increased complexity, slow downscaling, and inability to adapt to changing requirements. Therefore, AWS recommends using the decoupled architecture approach.

[Documentation](https://aws.amazon.com/blogs/architecture/introduction-to-aws-cloud-architecture-details/)

### ans - Decoupled

## 19. What is the primary purpose of designing for failure in AWS?

By designing for failure in AWS, you can minimize the impact of any failures or issues within your system. This is achieved through the use of features such as redundancy, backups, and fault tolerance, which help ensure that your system remains operational even if one or more components fail. This is particularly important in AWS, where complex systems can involve multiple services and components that could be affected by isolated failures. By designing for failure, you can reduce downtime, prevent data loss, and maintain the availability and reliability of your system.

[Documentation](https://aws.amazon.com/architecture/well-architected/)

### ans - To ensure that system downtime and data loss are minimized if a component or service fails

## 20. When is server-side encryption enabled on Amazon S3 objects?

Server-side encryption is enabled on Amazon S3 objects during each execution of the PUT operation for the S3 object. When an object is uploaded to S3, it can be automatically encrypted with AES-256 encryption or using AWS Key Management Service (KMS). This means that each time a file is uploaded to a bucket with server-side encryption enabled, the file will be encrypted as it's stored in S3.

[Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/default-encryption-faq.html)

### ans - On each execution of the PUT operation for the S3 object

## 21. What is the purpose of Amazon CloudFront's Edge locations?

Amazon CloudFront's Edge locations are used to cache frequently accessed content closer to end-users, reducing latency and delivering content quickly. This helps improve the performance of applications and ensures that users have a seamless experience. While AWS services may use Edge locations for additional functionality, such as AWS Lambda@Edge, their primary purpose is to serve as cache locations for CloudFront.

“…as data centers for AWS services” is incorrect because edge locations are not full data centers and only work for Edge services in AWS.

“…virtual private networking..” is incorrect because it refers to Amazon VPC, which is a separate networking service.

“To manage DNS records…” is incorrect because DNS management is handled by the Amazon Route 53 service.

[Documentation](https://aws.amazon.com/cloudfront/edge-locations/)

### ans - To cache frequently accessed content closer to end-users

## 22. Which of the following accurately describes AWS responsibilities regarding the AWS Shared Responsibility Model?

AWS provides a shared security model in which both AWS and the customer are responsible for different aspects of security and compliance. AWS is responsible for securing the infrastructure that hosts the customer's applications and data, while the customer is responsible for securing the actual applications and data within the infrastructure. AWS provides numerous security features and services such as network firewalls, encryption, and identity and access management to assist the customer in securing their data and applications within AWS.

### ans - AWS is responsible for securing the infrastructure and underlying services within the AWS cloud.

## 23. Which AWS service provides a comprehensive view of your high-priority security alerts and compliance status across AWS accounts?

AWS Security Hub gives you a comprehensive view of your high-priority security alerts and compliance status across your AWS accounts. It aggregates, organizes, and prioritizes your security alerts, or findings, from multiple AWS services, such as Amazon GuardDuty, Amazon Inspector, and Amazon Macie, as well as from AWS Partner solutions. The AWS Security Hub helps in centralizing security and compliance findings across AWS environments, making it easier for users to identify and manage potential security issues.

AWS WAF is a web application firewall that helps protect your web applications from various attacks by allowing you to configure rules based on IP protocol data. AWS Shield is a managed Distributed Denial of Service (DDoS) protection service that safeguards AWS applications. Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS.

### ans - AWS Security Hub

## 24. What is the recommended password policy in AWS for IAM users?

AWS allows customers to define their own password policies that meet their specific security requirements. While AWS does provide some best practices for password policies, such as requiring a length of at least 8 characters and encouraging the use of multi-factor authentication, it is ultimately up to the customer to define their own policy. Password rotation and complexity requirements can be set and enforced by IAM administrators.

[Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html)

### ans - It is recommended that Customers create their own password policy based on their needs.

## 25. What is the definition of economy of scale in AWS?

Economy of scale is a concept in which the average cost of production decreases as the volume of output increases. In AWS, this concept refers to the ability to decrease cost per unit of computing power as the size of an operation increases. This is made possible by the fact that AWS operates on a pay-per-use model, which means businesses only pay for the resources they use. As more resources are used, the overall cost decreases. Therefore, “The ability to decrease cost per unit…” is the correct answer.

“The increased cost of operating…” is incorrect because it suggests that the cost of operating additional resources increases, which is not the case with economy of scale. “The cost of computing power…” is incorrect because the cost of computing power is not constant and actually decreases with the increase in an operation's size. Lastly, “the increased cost of hosting larger quantities…” is incorrect because hosting larger quantities of data does not directly relate to economy of scale in AWS.

[Documentation](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html)

### ans - The ability to decrease cost per unit of computing power as the size of an operation increases

## 26. Which AWS service can aid in auditing and reporting on each action taken for resources in your environment?

AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. It enables you to log, monitor, and retain account activity related to actions across your AWS infrastructure, and it can aid in auditing and reporting on each execution of resources in your environment. Using CloudTrail, you can create detailed activity logs that can help you detect security threats and monitor your AWS account for undesirable activity.

[Documentation](https://aws.amazon.com/cloudtrail/)

### ans - AWS CloudTrail

## 27. What is the main difference between installing databases on Amazon EC2 and using AWS managed databases?

When running databases on Amazon EC2, users are responsible for managing the software, including patching and maintenance. In contrast, AWS managed databases, like Amazon RDS and Amazon Aurora, automatically apply patches and upgrades to the underlying infrastructure and software. This saves time and effort for database administrators and ensures that the databases are always running on the latest and most secure software.

[Documentation](https://aws.amazon.com/relational-database/managed-options/)

### ans  - Managed databases provide automatic software patching and upgrades, while databases installed on EC2 require manual updates.

## 28. Which service under AWS offers a portfolio of resources for startups, including AWS credits, training, and technical support?

AWS Activate for Startups is a program designed to provide startups with the resources they need to quickly get started on AWS, including AWS credits, training, technical support, and other benefits. It helps startups to build and scale their businesses by offering a range of resources including promotional credits, technical support, and training which can be pivotal in the early stages of startup development.

AWS IQ is a platform that connects AWS customers with certified AWS experts and consultants for hands-on help. AWS Managed Services (AMS) operates AWS on your behalf, providing a secure and compliant AWS Landing Zone, a proven enterprise operating model, on-going cost optimization, and day-to-day infrastructure management. AWS Support provides a range of plans that give you 24/7 access to Cloud Support Engineers.

### ans  - AWS Activate for Startups

## 29. Which AWS service centralizes the identity management process, helping you set up and manage AWS IAM configurations and settings?

AWS IAM Identity Center centralizes the identity management process, helping you set up and manage AWS IAM configurations and settings. It provides a unified location where you can manage your identity needs, including setting up federated access with AWS Single Sign-On, configuring AWS IAM settings, and understanding your AWS Organizations structure.

### ans - AWS IAM Identity Center

## 30. Which of the following scenarios/best fits for using Spot Instance pricing on each execution?

Spot instances are spare EC2 instances that are available at a discounted rate compared to On-Demand instances. They allow you to optimize your costs on workloads that can tolerate some level of interruption. Spot instances are ideal for workloads with flexible starting and stopping times, and high compute requirements, such as big data analytics, containerized applications, CI/CD, and web servers. In contrast, for workloads that require consistent and long-running compute capacity, On-Demand or Reserved Instances might be more economical.

[Documentation](https://aws.amazon.com/ec2/spot/)

### ans  - Workloads that can tolerate interruption, have flexible start or completion times, and require large amounts of compute resources at a lower cost.

## AWS services

## 1. In the AWS benefit called Stop Focusing on Data Centers, what is a business asked to focus on instead?

The "Stop Focusing on Data Centers" benefit of AWS means businesses can shift their focus away from managing infrastructure to focusing on their customers and business priorities.

Reference:  [https://d1.awsstatic.com/whitepapers/Introduction_to_AWS.pdf](https://d1.awsstatic.com/whitepapers/Introduction_to_AWS.pdf)

[Documentation](https://aws.amazon.com/what-is-cloud-computing/)

### ans- The Customer

## 2. Reservations are an economic construct where a business agrees to commit to using AWS for what duration or time frame?

AWS Reserved Instances provide discounts on Amazon EC2 pricing in exchange for upfront payment and commitment to use EC2 instances for 1 year or 3 years.

Reference:  [https://aws.amazon.com/ec2/pricing/reserved-instances/](https://aws.amazon.com/ec2/pricing/reserved-instances/)

[Documentation](https://aws.amazon.com/economics/)

### ans- 1 year or 3 years

## 3. What Cloud Deployment model is sometimes referred to as “Private Cloud”?

An on-premises or "on-prem" deployment model refers to a private data center. It is sometimes called a "private cloud." This is infrastructure dedicated to a single organization. The cloud deployment model refers to public cloud. A community cloud is public cloud for a dedicated community. A hybrid cloud combines public cloud and on-premises infrastructure.

[Documentation](https://d1.awsstatic.com/whitepapers/Introduction_to_AWS.pdf)

### ans - On-Premise

## 4. Name the AWS benefit that allows you to easily fix either over-sizing of an application server or an under-sizing of an application server?

The "Stop Guessing Capacity" benefit of AWS means the ability to scale computing resources up and down based on demand. This allows quickly fixing issues with over-provisioning or under-provisioning resources.

Reference:  [https://d1.awsstatic.com/whitepapers/Introduction_to_AWS.pdf](https://d1.awsstatic.com/whitepapers/Introduction_to_AWS.pdf)

[Documentation](https://aws.amazon.com/what-is-cloud-computing/)

### ans- Stop Guessing Capacity

## 5. In the AWS benefit called Trade Upfront Expense for Variable Expense, you often:

The "Trade CapEx for OpEx" benefit of AWS means switching from large upfront capital expenditures (CapEx) required to build and maintain on-premises infrastructure to the operating expense (OpEx) of paying only for what you use on AWS each month.  
Reference:  [https://d1.awsstatic.com/whitepapers/Proof%20Points_Migrating_Enterprise_Appilcations_to_AWS.pdf](https://d1.awsstatic.com/whitepapers/Proof%20Points_Migrating_Enterprise_Appilcations_to_AWS.pdf)

[Documentation](https://aws.amazon.com/what-is-cloud-computing/)

### ans -Move from using high-dollar data centers every few years to a pay-as-you-go service model every month

## 6. In Cloud Economics terms, what is another name for a lower price per unit when you use more units?

Volume discounts refer to lower unit pricing as volume increases. This is another term for "Benefit from Massive Economies of Scale" in cloud computing.

Reference:  [https://aws.amazon.com/economics/](https://aws.amazon.com/economics/)

[Documentation](https://aws.amazon.com/what-is-cloud-computing/)

### ans -Volume Discounts

## 7. Which of the following is a benefit of using Traditional IT over Cloud Computing?

A benefit of traditional IT compared to cloud computing is having more direct control over infrastructure. With on-premises data centers, organizations have full control and responsibility over hardware, software, networking, security, and operations. Cloud computing provides less direct control as much of the infrastructure is managed by the service provider.  
Reference:  [https://d1.awsstatic.com/whitepapers/Introduction_to_AWS.pdf](https://d1.awsstatic.com/whitepapers/Introduction_to_AWS.pdf)

[Documentation](https://aws.amazon.com/what-is-cloud-computing/)

### ans - Increase Control over Infrastructure

## 8. Which of the following is NOT a general service category in the AWS console?

The major service categories in AWS are:

1.  Compute: Services such as EC2, Lambda, Elastic Beanstalk, etc.
2.  Storage: Services such as S3, EBS, Glacier, etc.
3.  Databases: Services such as RDS, DynamoDB, Redshift, etc.
4.  Networking & Content Delivery: Services such as VPC, Route 53, CloudFront, etc.  
    "Data and Memory Storage" is not a category used by AWS to classify their services.

[Documentation](https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS_Certified_Cloud_Practitioner_Exam_Guide.pdf)

### ans - Data and Memory Storage


## 1. Which of the following best describes AWS WAF?

The correct answer is "A service that protects your web applications from common web exploits". AWS WAF is a web application firewall that helps protect your web applications from common web attacks, such as SQL injection, cross-site scripting (XSS), and cross-site request forgery (CSRF). It allows you to create rules to block or allow traffic based on configurable conditions and rule sets.

### ANS - A service that protects your web applications from common web exploits

## 2. Which of the following statements best describes the purpose of AWS CloudTrail?

The correct answer is "AWS CloudTrail enables you to track user activity and API usage in your AWS account". AWS CloudTrail is a service that provides governance, compliance, operational auditing, and risk auditing of your AWS account. It records API calls and events for your AWS account and delivers log files containing this information to an Amazon S3 bucket or sends them to Amazon CloudWatch Logs. CloudTrail allows you to monitor and log actions taken by users, services, and resources in your account, providing visibility into who did what, when, and from where.

### ANS - AWS CloudTrail enables you to track user activity and API usage in your AWS account.

## 3. What is the main purpose of AWS Firewall Manager?

The correct answer is "Centrally manage firewall rules and security group configurations". AWS Firewall Manager is a security management service that allows you to centrally configure and manage firewall rules and security group settings across multiple AWS accounts and resources. It helps ensure consistent security controls and compliance across your organization.

### ans  - Centrally manage firewall rules and security group configurations

## 4. What is the primary purpose of Amazon GuardDuty?

The correct answer is "Real-time threat detection and continuous monitoring". Amazon GuardDuty is a managed threat detection service that continuously monitors and analyzes events and logs from various AWS data sources, such as VPC Flow Logs, CloudTrail logs, and DNS logs. It uses machine learning algorithms and threat intelligence to identify potential security threats and malicious activity in your AWS environment.

### ans - Real-time threat detection and continuous monitoring

## 5. Which of the following features allows you to apply policies and settings across multiple AWS accounts in AWS Organizations?

The correct answer is Organizational Units (OUs). In AWS Organizations, you can create Organizational Units to group accounts and apply policies and settings at different levels of your organization's hierarchy. OUs provide a way to organize and manage multiple accounts within an organization and simplify the application of policies and controls across those accounts.

### ans - Organizational Units (OUs)

### 6. Which of the following actions can be logged by AWS CloudTrail? (Choose two.)

The correct answers are "User authentication events" and "S3 bucket object-level operations". AWS CloudTrail can log user authentication events, such as successful or failed login attempts, and it can also log S3 bucket object-level operations, such as object uploads, downloads, and deletions.

### ans - User authentication events,S3 bucket object-level operations

## 7. What is the main purpose of Amazon Cognito?

The correct answer is "Authenticate and authorize users for your applications". Amazon Cognito is a fully managed service that provides authentication, authorization, and user management for web and mobile applications. It allows you to securely authenticate users, manage user profiles, and control access to your applications.

### ans - Authenticate and authorize users for your applications

## 8. What is the primary purpose of Amazon Macie?

The correct answer is "Discover, classify, and protect sensitive data stored in AWS". Amazon Macie is a security service that uses machine learning to automatically discover, classify, and protect sensitive data stored in AWS. It helps identify sensitive data such as personally identifiable information (PII) and intellectual property, and it provides recommendations for improving data protection and access controls.

### ans  - Discover, classify, and protect sensitive data stored in AWS



## AWS Technology part-1

## 1. Which of the following statements is true about Network Access Control Lists (NACLs) in AWS?

Network Access Control Lists (NACLs) in AWS operate at the subnet level, controlling both inbound and outbound traffic. They provide an additional layer of security for VPCs by allowing or denying traffic based on rules. For more information, refer to the official AWS documentation on NACLs: Network Access Control Lists (NACLs)

### ans- NACLs operate at the subnet level

## 2. Which of the following is a characteristic of Amazon EC2 instances?

Amazon EC2 instances are provisioned on shared tenancy hardware, allowing for efficient resource utilization. However, EC2 also offers dedicated instances and dedicated hosts for customers who require isolated hardware resources. For more details, see the official AWS documentation on Amazon EC2 instances: Amazon EC2 Instances

### ans - Shared tenancy for efficient resource utilization

## 3. Which of the following statements accurately describes a public subnet in Amazon VPC?

The correct answer is "A public subnet is a subnet with an internet gateway attached". An internet gateway allows resources within a public subnet to communicate with the internet, making the subnet accessible from the internet.

### ans - A public subnet is a subnet with an internet gateway attached.

## 4 . What is the primary purpose of AWS Direct Connect?

The correct answer is "To connect on-premises data centers to the AWS Cloud". AWS Direct Connect provides a dedicated network connection between an organization's on-premises data centers and AWS, allowing for secure and reliable data transfer.

### ans - To connect on-premises data centers to the AWS Cloud

## 5. Which of the following statements accurately describes AWS Global Infrastructure's approach to data center redundancy?

The correct answer is "It uses multiple Availability Zones within each region for high availability and fault tolerance". Each AWS region is designed with multiple physically separated Availability Zones (AZs) that are interconnected through low-latency links. This design provides fault tolerance and allows customers to architect highly available applications.

### ans - It uses multiple Availability Zones within each region for high availability and fault tolerance.

## 6. Which of the following storage classes in Amazon S3 provides the lowest cost per GB?

The Glacier storage class in Amazon S3 provides the lowest cost per GB. It is designed for long-term archival storage where retrieval times are less critical. For more information, refer to the official AWS documentation on Amazon S3 storage classes: Amazon S3 Storage Classes

### ans - Glacier

## 7. Which of the following is a valid use case for using multiple Amazon VPCs within an AWS account?

The correct answer is "To isolate development, testing, and production environments". Using multiple Amazon VPCs allows you to segregate and isolate different environments, such as development, testing, and production, within the same AWS account. This separation provides enhanced security and control over the network traffic and resources associated with each environment.

### ans - To isolate development, testing, and production environments


## AWS Technology part-2

## 1. Which AWS service provides a fully managed, relational database service?

Amazon Relational Database Service (RDS) is a fully managed service that provides a relational database in the cloud. It supports popular database engines such as MySQL, PostgreSQL, Oracle, SQL Server, and MariaDB. With RDS, you can focus on your application, while AWS handles the management of database instances, backups, patching, and replication. For more information, refer to the official AWS documentation on Amazon RDS: Amazon RDS Documentation

### ans - Amazon RDS

## 2. What is the purpose of AWS Application Discovery Service?

AWS Application Discovery Service is designed to help you plan application migrations to the cloud by discovering and collecting data about your on-premises applications and their dependencies. It provides insights into the applications' configuration, usage patterns, and interdependencies.

### ans - To discover and collect data about on-premises applications and dependencies

## 3. What is an example of a rehost migration strategy in AWS?

Rehost migration strategy, also known as lift-and-shift, involves replicating the application environment as-is on AWS without making any changes to the application code. It is a common approach to quickly migrate applications to AWS with minimal modifications.

### ans  - Replicating the application environment on AWS

## 4. Which AWS service provides a fully managed NoSQL database service?

Amazon DynamoDB is a fully managed NoSQL database service provided by AWS. It offers seamless scalability, high availability, and low latency for applications that require fast and predictable performance. DynamoDB supports both key-value and document data models. For more information, refer to the official AWS documentation on Amazon DynamoDB: Amazon DynamoDB Documentation

### ans - Amazon DynamoDB

## 5. What is AWS CloudFormation primarily used for?

AWS CloudFormation is a service that helps you provision and manage AWS resources in a predictable and automated way. It allows you to define your infrastructure as code using templates and then deploy and manage the resources defined in those templates. For more information about AWS CloudFormation, you can refer to the official AWS documentation: AWS CloudFormation

### ans - Provisioning and managing AWS resources

## 6. Which AWS service provides a fully managed solution for migrating applications from on-premises environments to AWS?

AWS MGN is a fully managed service that simplifies and accelerates the migration of applications from on-premises environments to AWS. It provides automated replication, scheduling, and orchestration capabilities to streamline the migration process.

### ans - AWS Application Migration Service

## 7. Which of the following statements best describes AWS OpsWorks?

AWS OpsWorks is a configuration management service that helps you automate the deployment and management of applications. It provides features for defining application architecture, managing instances, and automating tasks. OpsWorks supports multiple configuration management tools, including Chef and Puppet. For more information about AWS OpsWorks, you can refer to the official AWS documentation: AWS OpsWorks

### ans - A configuration management service for deploying and managing applications

## 8. What is the purpose of AWS Migration Hub?

AWS Migration Hub is designed to help you track the progress and status of your application migrations to AWS. It provides a centralized view of your migration tasks, allowing you to monitor the migration process and identify any issues or delays.

### ans - To track the progress of application migrations to AWS

## 9. What is the purpose of the repurchase migration strategy in AWS?

Repurchase migration strategy involves replacing the existing application or software with a different vendor's solution. This strategy is commonly used when the current application or software no longer meets the business requirements or when a better alternative is available.

### ans - To replace existing software with a different vendor's solution

## 10. Which of the following statements accurately describes a key difference between Amazon RDS and Amazon Aurora?

Amazon RDS is a fully managed relational database service that provides high availability and durability for databases. It offers automated backups, automated software patching, and automatic failover capabilities. On the other hand, Amazon Aurora is a MySQL and PostgreSQL-compatible database engine that is built for better performance and scalability compared to traditional database engines. Aurora achieves this through an architecture that utilizes distributed storage and replication. It also offers features like read replicas and automatic scaling.

### ans - Amazon RDS is designed for high availability and durability, while Amazon Aurora offers better performance and scalability.

## 11. Which AWS service can be integrated with Auto Scaling to distribute incoming traffic across multiple instances?

Elastic Load Balancer (ELB) can be integrated with Auto Scaling to distribute incoming traffic across multiple instances within an Auto Scaling group. ELB helps ensure that the load is balanced across instances and improves the availability and fault tolerance of the application. For more details about integrating Auto Scaling with Elastic Load Balancer, you can refer to the official AWS documentation: Integration with Elastic Load Balancer

### ans - Elastic Load Balancer


### Billing and Pricing


## 1. What are the typical charges associated with transferring data into a VPC or AWS service?

When you transfer data into an Amazon VPC or an AWS service, you typically do not incur any data transfer charges. AWS does not charge for inbound data transfer. However, outbound data transfer can incur charges.

[Documentation](https://aws.amazon.com/ec2/pricing/on-demand/)

### ans - No data transfer charges

## 2. Which AWS support plan is the lowest you can choose and still get access to all of the Trusted Advisor Health Checks?

The AWS Business support plan is the lowest tier that provides access to all Trusted Advisor checks. The Developer support plan only includes a subset of Trusted Advisor checks. The Enterprise and Enterprise On-Ramp plans provide additional features beyond Trusted Advisor, such as access to solutions architects, service quotas increases, and a service health dashboard.

[Documentation](https://aws.amazon.com/premiumsupport/trustedadvisor/)

### ans - Business

## 3. What are the typical charges associated with transferring data from an Availability Zone to another Availability Zone within the same region?

When transferring data between Availability Zones within the same region, there are typically data transfer charges. AWS does charge for inter-AZ data transfer. No Charge, Maximum Price, and Small fee are incorrect as they suggest no or various types of fees, whereas AWS does not typically charge for this type of data transfer.

[Documentation](https://aws.amazon.com/ec2/pricing/on-demand/)

### ans - Normal price as data transfer charges

## 4. In the context of cost optimization with AWS, what should be prioritized?

Cost optimization in AWS often involves choosing managed services over unmanaged services whenever feasible. Managed services reduce the operational burden by handling many of the underlying administrative tasks, thus potentially reducing overall costs. Unmanaged services may require additional resources and time, increasing costs.

[Documentation](https://aws.amazon.com/pricing/cost-optimization/)

### ans - Managed services over unmanaged services when possible

## 5. On what frequency or time frame are most Amazon EC2 instances typically billed?

Most Amazon EC2 instances are charged on a per-second basis with a minimum of 60 seconds. This flexible pricing allows businesses to pay only for the compute time they use, making it cost-effective for workloads with variable compute requirements. The per-second billing applies to instances launched in On-Demand, Reserved, and Spot form. Dedicated Hosts are billed per hour.

[Documentation](https://aws.amazon.com/ec2/pricing/)

### ans - Per Second/Per Minute

## 6. Which type of Elastic Block Store (EBS) hard drive generally carries the highest cost per GB?

AWS Elastic Block Store (EBS) provides different types of volumes that cater to different needs. Among these, Provisioned IOPS Solid State Drive (SSD) is typically the most expensive on a per GB basis. This is because it delivers high performance for I/O intensive workloads and allows users to specify both volume size and the number of I/O operations per second (IOPS) the volume can support.

[Documentation](https://aws.amazon.com/ebs/pricing/)

### ans - Provisioned IOPS Solid State Drive

## 7. Which of the following Amazon EC2 options can provide up to a 90% discount on on-demand costs?

Amazon EC2 Spot Instances allow you to take advantage of unused EC2 capacity in the AWS cloud. Spot Instances are available at up to a 90% discount compared to On-Demand prices. Spot Instances can significantly lower your AWS costs but are subject to availability and can be interrupted by AWS with two minutes of notification when AWS needs the capacity back.

[Documentation](https://aws.amazon.com/ec2/spot/)

### ans - Spot

## 8. Which Amazon EC2 option should be chosen for cost-effectiveness while testing an application for 6 months?

If you're testing an application for a limited period of time (like 6 months), On-Demand Instances would likely be the most cost-effective choice. On-Demand Instances let you pay for compute capacity by the hour or second (minimum of 60 seconds) with no long-term commitments. This frees you from the costs and complexities of planning, purchasing, and maintaining hardware and transforms what are commonly large fixed costs into much smaller variable costs.

[Documentation](https://aws.amazon.com/ec2/pricing/on-demand/)

### ans - On-Demand

## 9. Which AWS Support plan gives you access to a dedicated Technical Account Manager for incident management and single-point escalation?

The AWS Enterprise Support plan provides access to a Technical Account Manager (TAM) who acts as a single point of contact for incident management and escalation. The TAM has a deep understanding of your workloads and environment and helps coordinate AWS resources to resolve critical issues. The Developer and Business Support plans do not include a TAM. The Enterprise On-Ramp plan includes limited access to a TAM for advisory purposes but not for incident response.

[Documentation](https://aws.amazon.com/premiumsupport/features/#Technical_Account_Manager)

## ans - Enterprise

## 10. Which Amazon EC2 pricing model is most suitable for an application that can withstand interruptions and recover gracefully?

Amazon EC2 Spot Instances are best suited for applications that can withstand interruptions and recover gracefully. These instances let you take advantage of unused EC2 capacity in the AWS cloud at steep discounts compared to On-Demand prices. Spot Instances are ideal for various fault-tolerant and flexible applications such as big data, containerized workloads, CI/CD, web servers, high-performance computing (HPC), and test & development workloads.

[Documentation](https://aws.amazon.com/ec2/spot/)

### ans - Spot


### full exam

## 1. Which AWS service provides a comprehensive view of your high-priority security alerts and compliance status across AWS accounts?

AWS Security Hub gives you a comprehensive view of your high-priority security alerts and compliance status across your AWS accounts. It aggregates, organizes, and prioritizes your security alerts, or findings, from multiple AWS services, such as Amazon GuardDuty, Amazon Inspector, and Amazon Macie, as well as from AWS Partner solutions. The AWS Security Hub helps in centralizing security and compliance findings across AWS environments, making it easier for users to identify and manage potential security issues.

AWS WAF is a web application firewall that helps protect your web applications from various attacks by allowing you to configure rules based on IP protocol data. AWS Shield is a managed Distributed Denial of Service (DDoS) protection service that safeguards AWS applications. Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS.

### ans - AWS Security Hub

## 2. Which of the following statements is true regarding Availability Zones in AWS?

Availability Zones are separate data centers that are interconnected through high-speed communication links within a single region. They are designed to provide virtually independent cloud computing resources that are distinct from each other in terms of power, network, and physical location. This allows AWS to minimize the impact of failures or disasters, ensuring high availability and reliability for customer applications and workloads.

“…share a single point of failure.” is incorrect because, by design, Availability Zones don't share a single point of failure. “…running on the same server.” is incorrect because Availability Zones are separate data centers, not instances running on the same server. “…for use in specific regions.” is incorrect because AWS provides Availability Zones in several regions across the globe.

[Documentation](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/RegionsAndAZs.html)

### ans - Availability Zones are physically isolated from each other within a single region.

## 3. What is the recommended password policy in AWS for IAM users?

AWS allows customers to define their own password policies that meet their specific security requirements. While AWS does provide some best practices for password policies, such as requiring a length of at least 8 characters and encouraging the use of multi-factor authentication, it is ultimately up to the customer to define their own policy. Password rotation and complexity requirements can be set and enforced by IAM administrators.

[Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html)

### ans - It is recommended that Customers create their own password policy based on their needs.

## 4. Which of the following statements accurately defines the role of operational expenses (OpEx) on each execution in AWS?

Operational expenses (OpEx) are the costs associated with running and maintaining a workload on AWS. These expenses include the costs of compute resources, storage, data transfer, and other operational costs. OpEx costs are often used to measure the ongoing costs of a workload or service on AWS. These costs can be managed and optimized using AWS tools such as AWS Cost Explorer, AWS Budgets, and AWS Trusted Advisor.  
“…with setting up a workload on AWS.” is incorrect because it defines the initial costs associated with setting up a workload on AWS as OpEx costs; these costs are actually termed as capital expenses (CapEx). “…with purchasing new hardware for a workload on AWS.” is incorrect as it talks about the costs associated with purchasing new hardware for a workload which is not related to OpEx costs. Finally, “…with upgrading the software for a workload on AWS.” is incorrect because it talks about the costs associated with upgrading the software which is not related to OpEx costs.

### ans - Operational expenses (OpEx) are the costs associated with running and maintaining a workload on AWS.

## 5. Which of the following scenarios/best fits for using Spot Instance pricing on each execution?

Spot instances are spare EC2 instances that are available at a discounted rate compared to On-Demand instances. They allow you to optimize your costs on workloads that can tolerate some level of interruption. Spot instances are ideal for workloads with flexible starting and stopping times, and high compute requirements, such as big data analytics, containerized applications, CI/CD, and web servers. In contrast, for workloads that require consistent and long-running compute capacity, On-Demand or Reserved Instances might be more economical.

[Documentation](https://aws.amazon.com/ec2/spot/)

### ans - Workloads that can tolerate interruption, have flexible start or completion times, and require large amounts of compute resources at a lower cost.

## 6. What are the different types of cloud deployment models that can be used for each execution?

The different types of cloud deployment models are On-Premise, Public, and Hybrid Cloud. In private cloud, services are provided on a private network, while in public cloud, services are provided over a public network. In hybrid cloud, the services are maintained on both private and public networks at the same time. Hence, option A is the correct answer. “Infrastructure as a Service (IaaS), Platform as a Service (PaaS)…” refers to the different types of cloud service models, not cloud deployment models. Cloud Native, Multi-Cloud, and Hybrid Cloud are cloud strategies and not deployment models. Infrastructure as Code (IaC), Functions as a Service (FaaS), and Containers as a Service (CaaS) , which are cloud application development services, not cloud deployment models.

[Documentation](https://aws.amazon.com/types-of-cloud-computing/)

### ans - On-Premise, Public, and Hybrid Cloud

## 7. Which AWS service allows developers to build, train, and deploy machine learning models quickly?

AWS SageMaker is a fully managed service that provides every developer and data scientist with the ability to build, train, and deploy machine learning models quickly. SageMaker removes the heavy lifting from each step of the machine learning process to make it easier to develop high-quality models.

While AWS Rekognition is used for image and video analysis, AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for users to prepare and load their data for analytics. AWS IAM, on the other hand, is used for secure control access to AWS services and resources.

### ans - AWS SageMaker

## 8. Which AWS service centralizes the identity management process, helping you set up and manage AWS IAM configurations and settings?

AWS IAM Identity Center centralizes the identity management process, helping you set up and manage AWS IAM configurations and settings. It provides a unified location where you can manage your identity needs, including setting up federated access with AWS Single Sign-On, configuring AWS IAM settings, and understanding your AWS Organizations structure.

### ans - AWS IAM Identity Center

## 9. What is the maximum size limit for a single archive in Amazon S3 Glacier?

Amazon S3 Glacier is a secure, durable, and low-cost storage service for data archiving. In S3 Glacier, you can upload archives of any size, from a few bytes to multiple terabytes. However, the maximum size of a single archive stored in S3 Glacier is 40 TB.

Option A (10 GB) is incorrect because it's too small compared to the actual limit. Option B (100 GB) is also incorrect as it's much smaller than the actual limit set by AWS. Option C (1 TB) is also not the correct answer as the actual limit is much higher than that.

### ans - 40 TB

## 10. Which of the following accurately describes AWS responsibilities regarding the AWS Shared Responsibility Model?

AWS provides a shared security model in which both AWS and the customer are responsible for different aspects of security and compliance. AWS is responsible for securing the infrastructure that hosts the customer's applications and data, while the customer is responsible for securing the actual applications and data within the infrastructure. AWS provides numerous security features and services such as network firewalls, encryption, and identity and access management to assist the customer in securing their data and applications within AWS.

### ans - AWS is responsible for securing the infrastructure and underlying services within the AWS cloud.

## 11. In AWS, which entity acts as a virtual firewall for controlling inbound and outbound traffic at the subnet level?

A Network Access Control List (Network ACL) is a virtual firewall for controlling inbound and outbound traffic at the subnet level in AWS. It contains a numbered list of rules that AWS processes in order to determine whether to allow or deny traffic to individual subnets. Network ACLs provide an additional layer of security, helping to control the traffic that is allowed to reach the instances that are in the subnets. It is essential in defining fine-grained access controls to ensure network security.

While a security group acts as a virtual firewall for your instance to control inbound and outbound traffic, AWS WAF protects web applications from various attacks, and AWS Shield is a managed DDoS protection service.

### ans - Network ACL

## 12. What is the AWS recommended approach for performing tasks that require the use of root accounts on each execution?

AWS best practice recommends that root accounts should be used only for account and service management tasks and never for day-to-day operational tasks. Assigning task-specific permissions to an IAM user allows an administrator to perform specific actions in the AWS account without the need for root account access. This approach provides an additional layer of control to prevent unauthorized or accidental access to resources.

[Documentation](https://aws.amazon.com/iam/features/manage-permissions/)

### ans - Assign task-specific permissions to an IAM user

## 13. What is the purpose of Amazon CloudFront's Edge locations?

Amazon CloudFront's Edge locations are used to cache frequently accessed content closer to end-users, reducing latency and delivering content quickly. This helps improve the performance of applications and ensures that users have a seamless experience. While AWS services may use Edge locations for additional functionality, such as AWS Lambda@Edge, their primary purpose is to serve as cache locations for CloudFront.

“…as data centers for AWS services” is incorrect because edge locations are not full data centers and only work for Edge services in AWS.

“…virtual private networking..” is incorrect because it refers to Amazon VPC, which is a separate networking service.

“To manage DNS records…” is incorrect because DNS management is handled by the Amazon Route 53 service.

[Documentation](https://aws.amazon.com/cloudfront/edge-locations/)

### ans - To cache frequently accessed content closer to end-users

## 14. What is the benefit of utilizing Pay-as-you-go pricing on AWS?

The benefit of utilizing Pay-as-you-go pricing on AWS is that you only pay for the resources you use, whether it be compute, storage, or other services. This allows for cost optimization and eliminates the need for upfront cost commitments.

[Documentation](https://aws.amazon.com/pricing/)

### ans - Pay only for the compute, storage, and other resources you use

## 15. In AWS, which feature allows you to define a set of permissions to determine what actions are allowed and denied by the entity assuming the role?

AWS IAM Roles allow you to delegate access with defined permissions, which determine what actions are allowed and denied by the entity assuming the role. Unlike IAM users, roles do not have permanent credentials; instead, they assume temporary security credentials, making them more secure for tasks such as cross-account access. IAM roles help in granting permissions that determine who can and cannot take action on specific resources, enhancing the security and manageability of AWS services.

### ans - AWS IAM Roles

## 16. Which of the following is considered a best practice for Security and Compliance in the AWS Partner Systems Integrator domain?

The correct answer is: Conducting continuous monitoring and auditing of partner integrator access and activity. This is important as partner integrators may have access to sensitive customer data and systems. Continuous monitoring and auditing helps ensure that access is granted only as needed and that any unauthorized activity is quickly detected and addressed.

### ans - Conducting continuous monitoring and auditing of partner integrator access and activity

## 17. What is the primary purpose of designing for failure in AWS?

By designing for failure in AWS, you can minimize the impact of any failures or issues within your system. This is achieved through the use of features such as redundancy, backups, and fault tolerance, which help ensure that your system remains operational even if one or more components fail. This is particularly important in AWS, where complex systems can involve multiple services and components that could be affected by isolated failures. By designing for failure, you can reduce downtime, prevent data loss, and maintain the availability and reliability of your system.

[Documentation](https://aws.amazon.com/architecture/well-architected/)

### ans - To ensure that system downtime and data loss are minimized if a component or service fails

## 18. Which of the following options is a benefit of using Dedicated Instances under Reserved Instances pricing?

Reserved Instances under Dedicated Instances pricing offer a higher discount for longer commitments than for shorter ones. The longer the commitment, the higher the discount offered for the hourly rate. This results in significant savings in costs in the long run for those who can commit to usage over an extended period. On the other hand, Spot Instances offer significant cost savings for workloads that are flexible in terms of time and can tolerate interruptions. Spot Instances pricing is market-driven and fluctuates based on supply and demand. However, they do not come with any commitment or guarantee of capacity.

[Documentation](https://aws.amazon.com/ec2/pricing/reserved-instances/)

### ans - Higher discounts for longer commitments

## 19. What is one of the key benefits of shifting technical resources to revenue-generating activities on AWS?

One of the key benefits of shifting technical resources to revenue-generating activities on AWS is increased focus on innovation and revenue growth. By allowing AWS to manage the infrastructure, technical resources can be freed up to focus on areas that add value to the business. This can include developing new products and features, improving existing ones, and finding new ways to drive revenue. The other answers are all incorrect, as they each lead to negative consequences that are the opposite of the intended benefit.

[Documentation](https://aws.amazon.com/cloud-concepts/)

### ans - Increased focus on innovation and revenue growth

## 20. Which of the following is true about the different compute families on AWS?

The different compute families on AWS are designed to optimally support various types of workloads. Instances within a compute family share similar compute, memory, and network capabilities, while instances across different compute families have different specifications. For example, the M family is optimized for general-purpose workloads, while the C family is optimized for compute-intensive workloads. Similarly, the R family is optimized for memory-intensive workloads, and the X family is optimized for high-performance computing. Therefore, similar capabilities is the correct answer.

“…identical compute, memory, and network capabilities…” is incorrect because there are different compute families on AWS with different specifications.

“…only one compute family available on AWS” is incorrect because there are multiple compute families available on AWS.

“…optimized for the same size of workload” is incorrect because instances within a compute family are optimized for different-sized workloads, not the same workload.

[Documentation](https://aws.amazon.com/ec2/instance-types/)

## ans- Instances within a compute family have similar compute, memory, and network capabilities but with different capacities.

## 21. Which of the following is NOT a benefit of using Elasticity in AWS?

Elasticity refers to the ability of an IT infrastructure to quickly and easily scale resources up or down depending on demand. The benefits of Elasticity in AWS include cost savings, scalability, and high availability. However, Security is not a benefit of Elasticity. While Elasticity can help mitigate against failure, it is not the same as increasing security.

[Documentation](https://aws.amazon.com/elasticity/)

### ans - Security

## 22. Which of the following is true about AWS Trusted Advisor?

AWS Trusted Advisor is a tool that provides real-time guidance to help you optimize performance, improve security, and reduce costs on your AWS infrastructure. It analyzes your AWS environment against best practices and recommends optimizations across five categories: cost optimization, performance improvement, security hardening, fault tolerance, and service limits.

The other options describe other AWS tools, such as AWS Security Hub, Amazon EC2 Instance Connect, and AWS Migration Hub, which are not focused on providing best practice guidance and optimization recommendations.

[Documentation](https://aws.amazon.com/trustedadvisor/)

### ans - It is a tool that helps customers optimize cost, security, performance, and fault tolerance through best practices.

## 23. What component of AWS Trusted Advisor performs security checks on each execution?

Security checks are a component of AWS Trusted Advisor on each execution. AWS Trusted Advisor scans your AWS environment and provides recommendations to help optimize cost, improve fault tolerance, increase performance, and enhance security. The Security check provides recommendations for securing your AWS resources, covering areas such as IAM, data protection, network security, and logging. Therefore, option D is the correct answer.

### ans - Security

## 24. What is the primary benefit of using parallel computing in AWS?

Parallel computing involves breaking down a large task into smaller tasks that can be executed simultaneously, thus reducing the overall processing time. The main benefit of using this approach in AWS is a significant increase in system performance. Other potential benefits include improved accuracy, reduced costs, and greater data processing capacity.

Increased cost efficiency is not the primary benefit of using parallel computing in AWS. While it may be a secondary or indirect benefit, the primary focus is on improved performance.

Improved security measures, has no direct relation to parallel computing. While security measures are important to consider when implementing any AWS solution, they are not directly related to the use of parallel computing.

Faster data backups, may be a potential benefit of parallel computing since it can accelerate data processing time, but it is not the primary benefit.

[Documentation](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html?pg=cloudessentials)

### ans - Enhanced performance

## 25. What is the definition of economy of scale in AWS?

Economy of scale is a concept in which the average cost of production decreases as the volume of output increases. In AWS, this concept refers to the ability to decrease cost per unit of computing power as the size of an operation increases. This is made possible by the fact that AWS operates on a pay-per-use model, which means businesses only pay for the resources they use. As more resources are used, the overall cost decreases. Therefore, “The ability to decrease cost per unit…” is the correct answer.

“The increased cost of operating…” is incorrect because it suggests that the cost of operating additional resources increases, which is not the case with economy of scale. “The cost of computing power…” is incorrect because the cost of computing power is not constant and actually decreases with the increase in an operation's size. Lastly, “the increased cost of hosting larger quantities…” is incorrect because hosting larger quantities of data does not directly relate to economy of scale in AWS.

[Documentation](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html)

### ans - The ability to decrease cost per unit of computing power as the size of an operation increases

## 26. Which AWS service can aid in auditing and reporting on each action taken for resources in your environment?

AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. It enables you to log, monitor, and retain account activity related to actions across your AWS infrastructure, and it can aid in auditing and reporting on each execution of resources in your environment. Using CloudTrail, you can create detailed activity logs that can help you detect security threats and monitor your AWS account for undesirable activity.

[Documentation](https://aws.amazon.com/cloudtrail/)

###  ans - AWS CloudTrail

## 27. What is the primary benefit of implementing elasticity in the cloud versus on-premises?

Implementing elasticity in the cloud versus on-premises has many benefits such as reduced costs, increased flexibility, and faster time to market. However, the primary benefit is that cloud resources have virtually unlimited capacity and can scale faster than on-premises resources. Whenever the demand for resources increases, cloud providers can provide additional capacity almost instantly, without the need for any physical infrastructure changes. This scalability is facilitated by the distributed nature of cloud computing and the flexibility of cloud providers. This makes cloud computing particularly effective for environments with rapidly changing demands, such as web applications.

[Documentation](https://aws.amazon.com/what-is-cloud-computing/elasticity/)

### ans - Cloud resources have virtually unlimited capacity and can scale faster than on-premises resources

## 28. In which scenario is On-Demand Instance pricing the best fit for AWS customers?

On-Demand Instance pricing is ideal for workloads with fluctuating demand and unpredictable spikes, as customers have the flexibility to pay for the time they use without any upfront costs or long-term commitments. This allows customers to scale capacity up or down as needed, without incurring excessive costs. In contrast, reserved instances or savings plan options might be more appropriate in case of predictable workloads, and Spot instances might be used when customers have a flexible budget and are willing to accept a higher level of instance failure rate due to interruptions or terminations with two-minute notification.

### ans - For workloads with fluctuating demand and unpredictable spikes

## 29. What is the behavior of Reserved Instances in AWS Organizations on each execution?

Reserved Instances in AWS Organizations provide capacity reservation and significant discounts on your Amazon EC2 usage. These benefits are applicable across all the accounts in your AWS Organization. The billing benefit applies to usage in all of your accounts. So, if you have Reserved Instances in your master account, the reservations automatically apply to usage across all member accounts.

### ans - The Reserved Instances are shared between all accounts in the organization.

## 30. Which of the following statements is true about AWS Pricing API?

AWS Pricing API is a free service that provides customers with real-time pricing information for various AWS services, along with all the possible combinations offered by the services. This enables customers to make informed decisions about the cost of using a particular configuration or combination of services.

### ans - AWS Pricing API provides real-time pricing information for services.

## 31. Which statement best describes the concept of least privileged access on each execution in AWS?

The concept of least privileged access on each execution in AWS means providing users with the minimum access privileges necessary to perform their job functions. This ensures that users have access only to the resources they need to perform their work and nothing more, reducing the risk of accidental or intentional misuse of resources. Providing users with access privileges beyond what they need can lead to security vulnerabilities. Providing the same access privileges to all users is not an effective approach since not all users require the same level of access. Providing users with unlimited access privileges is not a viable option since this could result in unauthorized access and misuse of resources.

[Documentation](https://aws.amazon.com/blogs/security/techniques-for-writing-least-privilege-iam-policies/)

### ans - Providing users with the minimum access privileges necessary to perform their job functions

## 32. Can the commitment of an EC2 Savings Plan in AWS be adjusted multiple times throughout its term?

### ans - No, once purchased, the commitment of an EC2 Savings Plan can't be changed.'



-----
## AWS Service questions:


## 1. Which AWS service provides a platform for deploying and managing applications in a fully managed environment?

Correct answer is “AWS Elastic Beanstalk”: AWS Elastic Beanstalk is a fully managed service that provides an easy-to-use platform for deploying and managing applications. It abstracts the underlying infrastructure and allows you to focus on writing code without worrying about server management. Elastic Beanstalk supports a variety of programming languages, platforms, and frameworks, making it suitable for a wide range of applications.

### ans - AWS Elastic Beanstalk

## 2. A company is using multiple AWS services to host their application, and they want to ensure that they optimize the environment by adhering to AWS best practices. Which of the following services is capable of inspecting your AWS environment and making recommendations to lower expenditures, improve system performance and reliability, and close security gaps?

Correct answer is “AWS Trusted Advisor”: AWS Trusted Advisor is an online tool that provides real-time guidance to help you provision your resources following AWS best practices. Trusted Advisor checks help optimize your AWS infrastructure, increase security and performance, reduce your overall costs, and monitor service limits.

### ans - AWS Trusted Advisor

## 3. Which AWS Support plan provides access to AWS documentation, whitepapers, and support forums, as well as 24/7 customer service for billing, account, and technical questions?

Correct answer is “Basic”: The Basic Support plan provides all customers with access to AWS documentation, whitepapers, and support forums, as well as a 24/7 customer service for billing, account, and technical questions.

### ans - Basic

## 4. Which of the following AWS pricing models allows customers to bid on unused EC2 capacity and run those instances for as long as their bid exceeds the current Spot Price?

Correct answer is “Spot Instances” : Spot Instances allow you to bid on unused EC2 capacity and run those instances for as long as your bid exceeds the current Spot Price. Spot Instances are available at up to a 90% discount compared to On-Demand instance prices.

### ans - Spot Instances

## 5. Which of the following is a best practice for securing data stored in Amazon S3?

Correct answer is “ Enable server-side encryption using AWS KMS-managed keys” : Server-side encryption is a method of encrypting data at rest in S3 buckets. When you use server-side encryption, your data is encrypted before it is saved to disk and decrypted when it is retrieved. AWS Key Management Service (KMS) provides a fully managed encryption service that makes it easy to create and control the encryption keys used to encrypt your data. By enabling server-side encryption with KMS-managed keys, you can ensure that your data is protected even if it is compromised.

### ans - Enable server-side encryption using AWS KMS-managed keys.

## 6. Which AWS billing tool provides interactive visualizations and analysis of your AWS costs and usage?

Correct answer is “Cost Explorer”: AWS Cost Explorer is a billing tool that provides interactive visualizations and analysis of your AWS costs and usage. It enables you to view, understand, and analyze your AWS spending patterns using customizable charts, graphs, and reports. Cost Explorer allows you to visualize your costs by services, usage types, regions, and more. It helps you identify cost drivers, monitor usage trends, and optimize your AWS spending.

### ans - Cost Explorer

## 7. What is the correct workflow for granting access to AWS resources using AWS Identity and Access Management (IAM)?

Correct answer is “Create an IAM group, create an IAM policy, and then attach the policy to the group”: When granting access to AWS resources using IAM, the best practice is to create an IAM group first, and then assign users to that group. Once you have created a group, you can then create an IAM policy that specifies the permissions that members of the group should have. Finally, you attach the policy to the group.

### ans - Create an IAM group, create an IAM policy, and then attach the policy to the group.

## 8. What is AWS SDK?

Correct answer is “A set of APIs for integrating AWS services with third-party applications”: The AWS SDK is a collection of software development kits (SDKs) that provide developers with APIs for integrating their applications with AWS services. The SDKs are available in multiple programming languages, including Java, Python, and Ruby, among others. Developers can use the SDK to build applications that interact with AWS services directly from their code without having to write low-level code to communicate with AWS APIs.

### ans- A set of APIs for integrating AWS services with third-party applications

## 9. Which AWS service is used for storing, managing, and deploying container images?

Correct answer is “AWS ECR”: AWS Elastic Container Registry (ECR) is a fully managed container registry service provided by AWS. It is used for storing, managing, and deploying container images, making it an integral part of container-based application development and deployment. With ECR, you can easily push and pull container images to and from the registry, control access to the images, and integrate it seamlessly with other AWS container services like Elastic Container Service (ECS) and Elastic Kubernetes Service (EKS).

### ans - AWS ECR

## 10. Which of the following AWS pricing models provides the most significant discount compared to On-Demand Instance pricing in exchange for a longer-term commitment?

Correct answer is “Reserved Instances”: Reserved Instances provide a significant discount (up to 75%) compared to On-Demand Instance pricing and provide a capacity reservation when used in a specific Availability Zone. You can choose between one-year or three-year terms, and you have the option to pay for the Reserved Instance upfront, partially upfront, or with no upfront payment.

### ans - Reserved Instances

## 11. Which AWS service provides a way to monitor and detect security incidents and vulnerabilities in your AWS environment?

Correct answer is “ Amazon GuardDuty”: Amazon GuardDuty is a threat detection service that continuously monitors and analyzes your AWS accounts and workloads for malicious or unauthorized activity. It uses machine learning, anomaly detection, and integrated threat intelligence to identify potential security issues. GuardDuty can detect a wide range of threats, including network-based attacks, compromised instances, and data exfiltration attempts.

### ans - Amazon GuardDuty

## 12. Which of the following actions will AWS charge you for?

Correct answer is “Transfer of EC2 files between two AWS Regions”: AWS charges for data transfer between two different regions. This is because data transfer out to a different region incurs costs associated with bandwidth and infrastructure.

### ans - Transfer of EC2 files between two AWS Regions

## 13. A customer is choosing the best AWS support plan which includes a designated Technical Account Manager. Which of the following should they choose?

Correct answer is “Enterprise”: The Enterprise support plan is the only AWS support plan that includes a designated Technical Account Manager (TAM). A TAM is your point of contact for AWS best practices and advice. They are technically capable and are your advocate within AWS to support your ongoing operational success.

### ans - Enterprise

## 14. Which of the following statements best describes multi-factor authentication (MFA) in the context of AWS security?

Multi-factor authentication (MFA) is a security feature that requires users to provide two or more forms of authentication before being granted access to AWS resources. This additional layer of security helps prevent unauthorized access to sensitive data and applications. With MFA, users are required to provide their primary password as well as a secondary form of authentication such as a security token, biometric information, or a smart card. MFA is an optional security feature for many AWS services, including AWS Management Console access.

## ans - MFA is an optional security feature that requires users to provide two or more forms of authentiaction before accessing AWS resources.

## 15. Which of the following benefits of cloud computing is best demonstrated by the ability to quickly scale up or scale down AWS resources based on demand?

Correct answer is “Stop guessing capacity”: The ability to quickly scale up or scale down AWS resources based on demand demonstrates the benefit of "Stop guessing capacity". In the cloud, you can provision the amount and type of resources that you actually need. If you need more, you can easily scale up. If you don't need as much, you can scale down.

### ans - Stop guessing capacity

## 16. Which of the following is an AWS service that provides managed security and compliance controls for your AWS resources?

Correct answer is “AWS Artifact”: AWS Artifact is a service that provides on-demand access to AWS compliance reports and other documents that help you meet regulatory and compliance requirements. This includes documents such as Service Organization Control (SOC) reports, Payment Card Industry (PCI) reports, and Health Insurance Portability and Accountability Act (HIPAA) reports. Artifact also provides access to the AWS Compliance Center, which contains information about AWS's compliance programs and certifications.

### ans - AWS Artifact

## 17. Which of the following best describes cloud computing?

All the options provided are different ways of describing cloud computing.

## ans - All of the options are correct

## 18. Under the Technology domain and concerning the AWS EBS service: Which type of AWS Elastic Block Store volume offers the lowest cost per gigabyte?

Correct answer is “Cold HDD (sc1)”: The Cold HDD (sc1) volumes are designed for infrequent access and offer the lowest cost per gigabyte of all EBS volume types.

### ans - Cold HDD (sc1)

## 19. Which of the following best describes the Least Privilege Principle in the context of AWS security?

Correct answer is “Access to AWS resources should be granted on a need-to-know basis”: The Least Privilege Principle is a security principle that states that users should only be given the minimum level of access necessary to perform their job function. This means that access to AWS resources should be granted on a need-to-know basis, and that users should not be given more permissions than they require. By following this principle, you can limit the potential damage that can be caused by a compromised account and reduce the risk of accidental or intentional misuse of resources.

## ans - Access to AWS resources should be granted on a need-to-know basis.

## 20. Which of the following provides you access to Reserved Instance (RI) purchase recommendations based on your past usage and indicate potential opportunities for savings as compared to On-Demand usage?

Correct answer is “AWS Cost Explorer”: AWS Cost Explorer has an RI Report that provides you with purchase recommendations. These recommendations are based on your past usage and can indicate potential opportunities for savings compared to On-Demand usage.

### ans - AWS Cost Explorer

## 21. Which of the following best describes the principle of "Loose Coupling" in cloud design?

Correct answer is “Designing systems with components that are independent and interact through specific interfaces”: "Loose Coupling" refers to designing systems where each component is independent and interacts with the others through specific, defined interfaces. This design principle helps ensure that a change or a failure in one component does not cascade to other components.

### ans - Designing systems with components that are independent and interact through specific interfaces

## 22. Which of the following is an AWS service that enables you to manage and control access to AWS resources across multiple accounts?

Correct answer is “AWS Organizations”: AWS Organizations is a service that enables you to centralize management of multiple AWS accounts. With Organizations, you can create groups of accounts and apply policies to those groups to manage access to resources and services across your organization. You can also use Organizations to automate account creation and management tasks.

### ans - AWS Organizations

## 23. Which of the following best describes the AWS Global Infrastructure?

Correct answer is “A worldwide network of Regions and Availability Zones”: The AWS Global Infrastructure is a worldwide network of Regions and Availability Zones. Regions are separate geographic areas that have multiple, isolated locations known as Availability Zones. Availability Zones are physically separate locations within an AWS Region that are engineered to be isolated from failures in other Availability Zones and provide inexpensive, low-latency network connectivity to other zones in the same Region.

### ans - A worldwide network of Regions and Availability Zones

## 24. Which of the following benefits of cloud computing is best demonstrated by the ability to pay only for the compute power, storage, and other resources you use, with no long-term contracts or upfront commitments?

Correct answer is “Trade capital expense for variable expense”: The ability to pay only for the compute power, storage, and other resources you use, with no long-term contracts or upfront commitments, demonstrates the benefit of "Trade capital expense for variable expense". With cloud computing, you can pay as you go and only pay for what you use.

### ans - Trade capital expense for variable expense

## 25. Using which AWS service can you consolidate billing across multiple AWS accounts, allowing easy access to cost reporting while maintaining the highest level of account security?

Correct answer is “AWS Organizations”: AWS Organizations allows you to consolidate billing across multiple AWS accounts. This provides you with centralized cost tracking and access to volume discounts, all while maintaining separate and secure resources for each account.

### ans - AWS Organizations

## 26. Which of the following AWS services provides a scalable, high-speed, low-latency platform for transferring data between users and data stored over the Internet?

Correct answer is “Amazon CloudFront”: Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment.

### ans - Amazon CloudFront