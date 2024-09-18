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