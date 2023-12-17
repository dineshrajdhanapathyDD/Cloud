

# Getting Started with Cloud Operations

IT operations are at the heart of every organization. Operating in the cloud allows IT teams to focus on business outcomes, optimizing IT processes while accelerating software development and innovation.

These days, it’s no longer a question of whether your organization is moving to the cloud, but how fast you can move with security, visibility, control, and safety. Companies of every size have realized the benefits of moving to AWS cloud, including a lower cost of operations, stronger operational resilience, and a smaller carbon footprint. Organizations moving large portfolios of legacy applications, ITIL-based processes, and datacenters to the cloud want a secure and efficient way to manage their infrastructure and applications in the cloud, on-premises, and at the edge.

AWS Cloud Operations provides a model and tools for a secure and efficient way to operate in the cloud. You can transform your organization, modernize and migrate your applications, and accelerate innovation with AWS.

In this module, you acquire the knowledge that you need to start using cloud operations tools. You learn about the key elements of the AWS Well-Architected Framework, cost management tools, AWS cloud operations services, and explore how to configure them.




## Getting Started with Cost Estimation



 The workload that you evaluate is for a three-tier web application that consists of an Application Load Balancer, an Amazon EC2 instance, and an Amazon RDS instance. The skills that you learn will help you use AWS Pricing Calculator to estimate costs for your workloads.

![Web-based application diagram](https://labs.vocareum.com/web/2931918/1597667.0/ASNLIB/public/docs/lang/en_us/images/CostEstimation01.png) _The preceding diagram includes a load balancer, an EC2 instance, and an RDS instance._

### Objectives

After completing this lab, you will know how to do the following:

-   Estimate AWS Costs using AWS Pricing Calculator.


## Task 1: Launch the AWS Pricing Calculator

In this task, you launch AWS Pricing Calculator and begin to create an estimate.

1.  Open a new web browser tab.
2.  In the address bar enter the following URL: [https://calculator.aws/#/](https://calculator.aws/#/)
3.  Choose **Create estimate**.

![1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a524ac11-359f-4abb-b7c3-12cd93176c83)


## Task 2: Add and configure services in AWS Pricing Calculator

In this task, you use AWS Pricing Calculator to explore AWS services and create an estimate for the cost of your use case, a three-tier web application.

### Add the load balancer to the estimate

4.  On the **Select service** page, in the **Find Service** search box, enter `Elastic Load Balancing`.

![2](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/cdd796a3-ad65-48fb-8a21-e198f3bce1b0)


5.  In the **Elastic Load Balancing** card, choose **Configure**.

![3](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/5883406d-3aa3-4762-8099-0043a47847fb)

6.  In the **Description** section, configure the following options:

-   For **Description**, enter `Load Balancer`.
-   For **Select location type**, choose **Region**.
-   For **Select region**, choose **US West (Oregon)**.

![5](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/7c45e2a4-fa30-4213-9191-a141455b838e)


7.  For **Elastic Load Balancing**, turn on **Application Load Balancer**.
    
8.  In the **Application Load Balancer** section, choose **Load Balancer in AWS Region**.
    
9.  In the **Service settings** section, for **Number of Application Load Balancers**, enter `1`.

![6](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a0227008-3dec-4711-a4c4-0737420043a8) 
    
11.  In the **Load Balancer Capacity Units (LCUs)** section, configure the following options:
    
    Note: The load balancer metrics that are used to estimate cost, such as processed bytes and connection duration, are typically provided by the team that developed and tested the application. These numbers vary based on the application profile.
    

-   Skip **Processed bytes (Lambda functions as targets)** because you are using EC2 instances.
-   For **Processed bytes (EC2 Instances and IP addresses as targets)**, enter `0.36`. From the dropdown list, choose **GB per hour**.

![7](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/5d1228f2-dc2c-4b20-8a4d-263964e62d8f)

-   For **Average number of new connections per ALB**, enter `100`. From the dropdown list, choose **per second**.
-   For **Average connection duration**, enter `3`. From the dropdown list, choose **minutes**.
-   For **Average number of requests per second per ALB**, enter `400`.
-   For **Average number of rule evaluations per request**, enter `20`. 

![8](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/82595fdb-e529-4b2d-ab85-eef3e99f0165)

    Note: Load balancer listener rules determine how the load balancer routes requests. For example, the default rule only routes HTTP traffic on port 80 to the EC2 instances (targets).

12.  Choose **Save and add service**.


![9](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/4900d490-86f9-4bcd-97ff-8c7f27f3ab18)
    

### Add the EC2 instance to the estimate

13.  On the **Select service** page, in the **Find Service** search box, enter `EC2`.
14.  In the **Amazon EC2** card, choose **Configure**.
15.  In the **Description** section, configure the following options:

-   For **Description**, enter `EC2`.

![10](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/84fe7b04-4604-46eb-b84c-62fb4bdccc6d)
    
-   For **Select location type**, choose **Region**.
    
-   For **Select region**, choose **US West (Oregon)**.
    

16.  In the **EC2 instance specifications** section, for **Operating system**, choose **Linux**.

![11](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/8da7f204-5e98-499c-b083-86fdf1554f83)

17.  In the Workload section, configure the following options:

-   Choose **Daily spike traffic**.
-   Keep the settings for **Workload days** (Monday - Friday).

![12](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/1449a1a8-3c52-45b6-a9b2-ca1c6522c1c2)

-   For **Baseline**, enter `1`.
-   For **Peak**, enter `2`. **Note:** These settings indicate that this workload requires one instance at normal times and two instances during peak usage.
-   For **Duration of peak (hours,minutes)**, keep the default settings.

![13](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/65e423f3-d44c-449e-b6db-dceacef8c075)

18.  In the **EC2 instances** section, choose **t4g.small**.
19.  In the **Pricing strategy** section, choose **On-Demand**.


![14](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/84546cab-83f9-49d0-80c8-2d1a319ab5b7)
![15](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/674b12a9-950b-44bf-b13c-98860445c0cd)


20.  In the **Amazon Elastic Block Storage (EBS)** section, configure the following storage options:

-   For **Storage for each EC2 instance**, choose **General Purpose SSD (gp3)**.
-   For **General Purpose SSD (gp3) - IOPS**, keep the default setting.
-   For **General Purpose SSD (gp3) - Throughput**, keep the default setting.
-   For **Storage amount**, enter `30`. From the dropdown list, choose **GB**.

![16](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/bda8b642-78b8-471d-8af5-693c4f00843c)

21.  In the **Data transfer** section, configure the following options:

-   For **Inbound Data Transfer**:
    
    -   From the first dropdown list, choose **Internet (free)**.
    -   Enter `50`.
    -   From the last dropdown list choose **GB per month**.
-   For **Outbound Data Transfer**:
    
    -   From the first dropdown list, choose **Internet (0.05 USD - 0.09 USD per GB)**.
    -   Enter `200`.
    -   From the last dropdown list, choose **GB per month**.


![17](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/c282eb62-a38a-4a2f-8360-f46654e9dc56)

22.  Choose **Save and add service**.

![18](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/4d0e58fa-0a1a-49f7-b032-e3d24a5a2492)
    

### Add the RDS instance to the estimate

23.  On the **Select service** page, in the **Find Service** search box, enter `RDS`.
24.  In the **Amazon RDS for MySQL** card, choose **Configure**.

![19](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/0fb9251e-a4fa-42ec-834c-c8b8521d2d8a)

25.  In the **Description** section, configure the following options:

-   For **Description**, enter `Database`.
-   For **Select location type**, choose **Region**.
-   For **Select region**, choose **US West (Oregon)**.

26.  In the **MySQL instance specifications** section, configure the following options:

-   For **Quantity**, enter `1`.
-   From the dropdown list, choose **db.m6g.large**.

![20](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/585b8a8a-97f8-4b89-b4e2-3b698979ff0f)

-   For **Deployment option**, choose **Multi-AZ**.
-   For **Pricing model**, keep the default setting.

27.  Skip the **RDS Proxy** section.


![21](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/af2a6280-e5f2-48aa-9a77-423eeb83b160)

28.  In the **Storage** section, configure the following settings:

-   For **Storage for each RDS instance**, choose **General Purpose SSD (gp2)**.
-   For Storage amount, enter `100`. From the dropdown list, choose **GB**.

![22](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/12e06173-1d95-4966-b0b3-d82377046fbd)

29.  Skip the **Backup Storage** and **Snapshot Export** sections.
30.  Choose **Save and add service**.


![23](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e90aa137-38e2-4089-af38-878f3cb4f037)

  

## Task 3: Review and download the estimate

In this task, you review the cost estimate that the calculator generated, and you download a copy of the estimate into a comma-separated values (CSV) file. A CSV file can be opened in desktop tools such as Excel.

31.  Choose **View summary**.
32.  Review the overall costs that AWS Pricing Calculator generated for the services from the **My Estimate** page. AWS Pricing Calculator provides the total cost for the first 12 months. If needed, you can edit or delete the configuration of the services added by choosing the edit icon next to each service name.

![24](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/c5dd9073-8e2d-4a5b-9488-f0d4276ea19f) _The preceding screenshot is an example of the cost estimate summary._

    Note: The prices found in your estimate may vary as prices occasionally change.

33.  Choose **Export**, and then choose **CSV**.

![25](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/466da741-0748-4d17-b0cb-2b9c2a0653ad)

34.  In the **Export My Estimate to csv** dialog box, choose **OK**.
35.  Use your local file explorer to save the file.

## Task 4: Save and share the estimate

In this task, you share your estimate with others and save it.

Commonly, estimates need to be shared with others such as managers, project team members, or even customers.

36.  Choose **Share**.
    
37.  In the **Save estimate** dialog box, choose **Agree and continue**.

![26](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/be39504c-551a-45ec-8ebe-6ded1417c492)
    
38.  To copy the link for your estimate, choose **Copy public link**. https://calculator.aws/#/estimate?id=b93812bfd12e040b26dc7c96a7fd89096abb58d9


![27](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/871beefb-ba0d-4009-91b1-f10054dcaf71)


    
39.  To share the estimate, send the link to others using a communication tool such as email.
    
    **Note:** When you share an estimate, AWS Pricing Calculator automatically saves it and generates a URL to access it. AWS Pricing Calculator saves your estimate for 3 years.
    

## Summary

In this module, you created a cost estimate using AWS Pricing Calculator. You added the components that are required for a three-tier web application and defined the sizing requirements for each service. You previewed the annual cost estimate and generated a link to share the estimate with others.

Now, you know how to evaluate the potential costs of architectures before you deploy them. This helps you control your AWS costs and avoid unpleasant surprises such as unexpected or high monthly bills.


## Keytakeaway

By the end of this module you will be able to do the following:

- Describe cloud operation fundamental concepts.
-  Explain the Amazon Well-Architected Framework.
-  Describe AWS cost and free tier structures.
-  Describe the AWS cost management tools that are available.
- Identify support plans and explain the differences between them.
- Discuss AWS cloud operations services that are available to you, including AWS Trusted Advisor, AWS Health Dashboard, Amazon CloudWatch, AWS CloudTrail, AWS Organizations, AWS Systems Manager, and AWS Config.


**Credits : AWS Educate**