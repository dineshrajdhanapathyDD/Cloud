

# Getting Started with Networking

Computer networking refers to interconnected computing devices that can exchange data and share resources with each other. These networked devices use a system of rules, called communications protocols, to transmit information over physical or wireless technologies. Modern-day network solutions deliver more than connectivity. They are critical for the digital transformation and success of businesses today.

Amazon Virtual Private Cloud (Amazon VPC) is a service that you can use to provision a logically isolated section of the AWS Cloud. This section (called a virtual private cloud, or VPC) is where you can launch your Amazon Web Services (AWS) resources. With Amazon VPC, you have control over your virtual networking resources. These resources include the selection of your own IP address range, the creation of subnets, and the configuration of route tables and network gateways.

In this course, you acquire the knowledge you that you need to start using Amazon VPC. You learn about the key elements of Amazon VPC and explore how to configure them. You learn how to set up security for VPCs and learn about other AWS networking services.



### OBJECTIVES

-   Describe networking fundamental concepts.
-   Explain Amazon VPC features, benefits, and use cases.
-   Discuss how to configure public and private subnets.
-   Discuss how to configure route tables to direct traffic in your network.
-   Describe how to use an internet gateway and a virtual private gateway to allow traffic into your network.
-   Discuss how to configure security in a VPC by using network access control lists (network ACLs) and security groups.
-   Describe types of IP addressing, including use and benefits.
-   Identify ways to manage your VPC.


# Lab: Creating a Virtual Private Cloud


![1](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/f3961bd8-4ce3-474e-977f-063522fc1764)


### Objectives

you should be able to do the following:

-   Explain the basic components of a VPC
    
-   Deploy a basic VPC with public subnets
    
-   Deploy an EC2 instance into a VPC
    

 your architecture will look like the following example:

![AWS network diagram with an EC2 instance](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/cb249b2e-82d4-42af-a7ce-9ff0d62fcbc2) 

_In the preceding diagram, an EC2 instance is deployed into a VPC._

## Part 1: Exploring the default VPC

### Task 1: Explore the Example VPC configuration

you begin by exploring the Example VPC. The Example VPC is modeled after the default VPC that is automatically included with each AWS account.

A VPC is a virtual network that is dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS Cloud. You can launch AWS resources, such as Amazon Elastic Compute Cloud (Amazon EC2) instances, into the VPC.

![AWS region with a VPC](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/fcb1d885-3ca7-40a2-be55-cc0a5f3e4351)

_In the preceding diagram, an VPC is deployed into an AWS region._

5.  In the AWS Management Console on the **Services** menu, enter **VPC**. From the search results, choose **VPC**.



![2](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/e927a870-fd65-4527-bc1f-1e35f7d9673a)
    
6.  In the left navigation pane, choose **Your VPCs**.
    
    You find two VPCs: the default VPC and the Example VPC.
    
7.  Notice that the **Example VPC** is configured with the CIDR range of **172.31.0.0/16**.

![3](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/65859da8-68e6-4646-87d0-f229abdab163)
    
   - This CIDR range includes all addresses from 172.31.0.0 through 172.31.255.255, a total of 65,536 addresses.
    
   8.  Make a note of the **VPC ID** for the Example VPC. You will use it later in the lab.
![4](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/67ce778e-8521-4c5d-8cbd-26999eeef90b)
    

### Task2: Explore a Subnet

In this task, you explore a public subnet.

A subnet is a subrange of IP addresses in the VPC. AWS resources can be launched into a specified subnet. Use a _public subnet_ for resources that must be connected to the internet, and use a _private subnet_ for resources that must remain isolated from the internet.

![A VPC with multiple subnets](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/f80c37e0-8487-4d0c-87ef-56f45b8ba74c)

_The preceding diagram includes the Example VPC and four subnets that reside inside it._

9.  In the left navigation pane, choose **Subnets**.
    
    Notice that all of the subnets that begin with the name **Public Subnet** are associated with the same VPC, the Example VPC. Also notice that each subnet has an **IPv4 CIDR** range. Each subnet CIDR range is a distinct subset of the addresses available in the VPC. When designing your subnets, you must ensure that the CIDR ranges do not overlap with address ranges used in other subnets.

![6](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/cf161772-5756-4358-90b1-79078bbed46b)
    
10.  From the list of subnets, choose the subnet named **Public Subnet 1**.

![7](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/4d7708d2-bae8-44a6-a178-ea97a66560a0) 

- This subnet uses the **IPv4 CIDR** range **172.31.0.0/20**.

- The VPC has a CIDR block of **172.31.0.0/16**, which includes all 172.31.x.x IP addresses. This subnet has a CIDR block of **172.31.0.0/20**, which includes addresses 172.31.0.0 through 172.31.15.255. These CIDR ranges might look similar, but the subnet is smaller than the VPC because of the **/20** in the CIDR range. This subnet uses the first 4,096 addresses available in the VPC. The console shows that only 4,091 addresses are available to use. This is because AWS always reserves five addresses in each subnet for IP networking purposes.

11.  Notice that the value for **Auto-assign public IPv4 address** is **Yes** which means that it is turned on.

![8](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/3f6be522-536b-4ccc-b0e6-a2f859a52bc0)
    
 -    This means that the subnet automatically assigns a public IP address for all instances that are launched into it.
    

### Task 3: Explore an internet gateway

In this task, you explore the VPC's internet gateway (IGW).

An _internet gateway_ allows communication between the resources in a VPC and the internet. It is a horizontally scaled, redundant, and highly available VPC component. It imposes no availability risks or bandwidth constraints on network traffic.

![A VPC with an internet gateway](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/47a6c696-1e0c-48eb-ae0f-0f508a4c0600)

_In the preceding diagram, an internet gateway provides access to the internet to two subnets that reside in the VPC._

An internet gateway serves the following two purposes:

-   To provide a target in route tables that connects to the internet
    
-   To perform network address translation (NAT) for instances that were assigned public IPv4 addresses
    

12.  In the left navigation pane, choose **Internet Gateways**.

![9](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/5737a8fe-33d0-423f-9067-e6fedf055c40)
    
13.  Locate the row containing the internet gateway named **Example Internet Gateway** and select it.



![10](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/092c7964-84eb-438f-87af-13ee1dbedb93)
    
  -  Notice that the **State** of the internet gateway is **Attached**. The internet gateway is attached to the VPC shown under **VPC ID**. This is the VPC ID of the Example VPC.
    

### Task 4: Explore a route table

In this task, you explore the route table used by the Example VPC.

You verified that an internet gateway exists and that it is attached it to the Example VPC. Before the subnets can access the internet gateway, the route table associated with the subnets must be configured to use the internet gateway.

A _route table_ contains a set of rules, called routes, that are used to determine where network traffic is directed. Each subnet in a VPC must be associated with a route table because the table controls the routing for the subnet. A subnet can be associated with only one route table at a time, but you can associate multiple subnets with the same route table.

To use an internet gateway, a subnet's route table must contain a route that directs internet-bound traffic to the internet gateway. If a subnet is associated with a route table that has a route to an internet gateway, it is known as a public subnet.

![Diagram of the VPC, public subnets, and the public route table](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/f21980ce-3d4b-4104-a02d-40394bb62d08)

_In the preceding diagram, the route table directs traffic locally inside the VPC, and sends public traffic to the internet gateway._

14.  In the left navigation pane, choose **Route Tables**.

![11](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/1186f6ec-1ffa-476d-9630-dc5874fa49c6)
    
15.  Locate the row containing the route table named **Public Route Table** and select it.
    



This route table is associated with the Example VPC.

16.  In the lower half of the page, choose the **Routes** tab.
    
   - There are two routes: a local route and a public route.

![12](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/4a506d4c-c13f-47ae-9037-1ee9484a149d)


    
  -  All traffic that is destined for 172.31.0.0/16 (which is the range of the Example VPC) is routed locally. This route allows all subnets in a VPC to communicate with each other.
    
   -  All public traffic (0.0.0.0/0) is routed to the internet gateway.
    
17.  Choose the **Subnet associations** tab.
    
18.  In the **Explicit subnet associations** section, notice that the subnet with the **IPv4 CIDR** 172.31.0.0/20 is included in the list. This is the same subnet you reviewed earlier.

![13](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/f2b373e2-2e07-46fe-a222-d05fcfe797fc)
    
   -  All of the subnets in this list are public subnets because they have a route table entry that sends traffic to the internet through the internet gateway.
    

### Task 5: Explore a security group

In this task, you explore and update the security group used by the Example VPC subnets.

A _security group_ acts as a virtual firewall for instances to control inbound and outbound traffic. Security groups operate at the level of the elastic network interface for the instance. Security groups do not operate at the subnet level. Thus, each instance can have its own firewall that controls traffic. If you do not specify a particular security group at launch time, the instance is automatically assigned to the default security group for the VPC.


![Diagram of the VPC, public subnets, public route table, and security group rules](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/155c9022-e79e-4d77-b32c-1f56e08aab22)

_In the preceding diagram, the security group rules allow access to all ports for traffic that comes from the security group. The rules allow outbound access to the internet (0.0.0.0/0)._

In this task, you review the default security group that is associated with the Example VPC. Then, you update a custom security group to allow users to access resources using HTTP.

19.  In the left navigation pane, choose **Security Groups**.



![14](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/7d516227-d244-434b-87a2-700b6a768aa2)
    
20.  Locate the row containing the **default** security group for the Example VPC and select it.
    

- You will need to locate the Example VPC using the VPC ID you saved earlier.

21.  In the lower half of the page, choose the **Outbound rules** tab.
![15](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/c72d5a02-24d8-4062-9f01-7691715aa359)

    
    - You find one rule. This rule allows **All** protocols and **All** port ranges to send traffic to any IP address (0.0.0.0/0).
    
22.  Choose the **Inbound rules** tab.

![16](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/a8e7ead0-0bbf-4461-8979-3e7556de964b)
    
   -  You find one rule for incoming traffic. This rule allows incoming traffic to **All** protocols, and **All** port ranges from resources that use the default security group.
    
    - In a later step, you will test an EC2 instance that was deployed into the Example VPC when the lab started. For incoming traffic from sources outside your VPC to access this website, you must add a new security group rule. Because you should not make changes to the default security group, you create a new one. Then, you add a rule to your new security group to permit HTTP (port 80) traffic that comes from anywhere on the internet (0.0.0.0/0).
    

23.  Locate the row containing the **Web-Server-SG** security group for the Example VPC and select it.
    
24.  In the lower half of the page, choose the **Inbound rules** tab.
![17](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/56572f29-7752-42fa-9da7-1dfa25a13c52)

    
25.  Choose **Edit inbound rules**.
    
26.  Choose **Add rule**.
    
27.  Configure the following settings:
    
   -   For **Type**, choose **HTTP**.
        
    -   From the **Source type** dropdown list, choose **Anywhere IPv4**.
        
    -   For **Description**, enter `Allow web access`
        
28.  Choose **Save rules**.

![18](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/b18f9e30-4305-4c69-ba1b-80137b32bb01)
    

### Task 6: Identify an EC2 instance's VPC and Subnet

In this task you find the VPC and Subnet for an EC2 instance. You also test your Web-Server_SG security group configuration by confirming that you can access the EC2 instance from the internet.

![a diagram of and ec2 instance deployed into a public subnet](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/e13faf1f-d8a3-46ae-90e9-0d54efcbaf9c)
_In the preceding diagram, an EC2 instance is deployed into a public subnet in the default VPC. A security group is associated with the EC2 instance._

29.  On the **Services** menu, choose **EC2**.



![19](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/c6da6014-1caa-4d1a-bb4f-75bc55da6aec)
    
30.  Choose **Instances (running)**.
    
31.  Select **Web-Server**.


![20](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/a5435093-bc44-485d-9779-1884ff4870fe)
    
32.  In the Details tab, locate the value for **VPC ID**.
    
 -  This EC2 instance was deployed into the Example VPC that you explored.
    
33.  In the Details tab, locate the value for **Subnet ID**.

![21](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/41e194e1-19ae-4915-9b42-d6b85887c050)

    
 -  This EC2 instance was deployed into the Public Subnet 1 subnet, which is part of the Example VPC.
    
 -    When you launch an EC2 instance, both the VPC and the Subnet are defined for the instance. These configurations can't be changed. In a later task, you will explore the steps for creating a new EC2 instance.
    

Next, you verify that you can reach the website that runs on the EC2 instance.

34.  From the **Details** tab, copy the **Public IPv4 address** address.
    
35.  Open a new browser tab, paste the IP address that you just copied, and then press Enter.
    

If you configured the security group rule correctly, the following message will appear: **Hello from your webserver!**.


![22](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/85721521-64d8-4bd5-9b9b-3323955edc66)


If the message does not appear, wait for 60 seconds and refresh the page to try again. It can take a couple of minutes for the EC2 instance to boot and run the script that installs the website.

## Part 2: Creating a VPC

Being able to use the **default** VPC when you are first learning about and working with AWS cloud is very convenient. However, in the real world, you often need to create custom VPCs to meet a customer's requirements. For example, a customer might have already used the CIDR range of the default VPC in their on-premises network configuration. A customer might also want to vary how many addresses are included in each subnet. Because it is not possible to change the CIDR ranges assigned to the VPC or its subnets, you need to create a new VPC for your customer.

In this scenario, you create a new VPC. Your customer provided the following network requirements for the VPC's CIDR ranges:

Top-level VPC

-   **VPC IPv4 CIDR** - 10.0.0.0/16
    

Availability Zones:

-   They need to deploy their resources to two Availability Zones.
    

Two public subnets:

-   **Public Subnet 1** - 10.0.0.0/24
    
-   **Public Subnet 2** - 10.0.1.0/24
    

Two private subnets:

-   **Private Subnet 1** - 10.0.2.0/24
    
-   **Private Subnet 2** - 10.0.3.0/24
    

The Example VPC that you explored earlier did not have any private subnets. Remember that the difference between a public subnet and a private subnet is whether or not they can be reached directly from the internet. The route table associated with a public subnet includes a route to an internet gateway, and the route table for a private subnet does not.

### Task 7: Create a custom VPC

You can configure the VPC by defining its IP address range and creating subnets. You can also configure route tables, network gateways, and security settings.

The VPC console provides a wizard that can automatically create several VPC architectures. You use this wizard to create a new VPC.

If the configuration of a setting is not mentioned in these steps, leave the default value.

36.  Return to the browser tab with the AWS console.
    
37.  In the AWS Management Console on the **Services** menu, enter **VPC**. From the search results, choose **VPC**.
    
38.  In the left navigation pane, choose **Your VPCs**.


![23](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/30b8232f-2856-4595-b2c0-213b8c9b4d7f)
    
39.  Choose **Create VPC** and configure the following settings:

![24](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/5d3a503a-28d5-4f0a-b5f8-17b96b1195ca)
    
   -   For **Resources to create**, choose **VPC and more**
        
   -   For **Name tag auto-generation**, enter `Lab`.
        
   -   For **IPv4 CIDR block**, ensure that the value is `10.0.0.0/16`.
        
   -   For **Availability Zones (AZs)**, choose **2**.
        
   -   For **Number of public subnets**, choose **2**.
        
   -   For **Number of private subnets**, choose **2**.
        
   -   Expand **Customize subnets CIDR blocks**.
        
   -   Update the subnet CIDR block values using the ranges provided by your customer.
        
40.  Take a moment to review the **Preview** diagram provided in the wizard.

![25](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/b7b99b4c-c591-4254-ba70-12cef420a852)
    
41.  Choose **Create VPC**.
    

![26](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/b36424fd-fc7c-480a-917b-4b72524120d7)


The wizard immediately starts creating your VPC. After it finishes, you have a VPC that has all of the components that you explored earlier: subnets, route tables, an internet gateway, and a default security group. The VPC wizard also automatically configures the routes in the route tables for both the public subnets and the private subnets.

Like the default security group you explored earlier, the default security group created by the wizard blocks incoming traffic from the internet. To reach a web server in the new VPC, you need to add a rule to this default security group.

42.  Choose **View VPC**.


![27](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/850b9b2d-fe40-45b5-93b7-05970f642f70)
    
   Recall that a VPC's **default** security group does not allow traffic from outside the VPC. Because you should not change the default security group, you add a new security group to your custom VPC.
    
43.  In the left navigation pane, choose **Security Groups**.


![28](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/494e79ec-28bb-4dea-b8f5-4be60ac6922a)

    
44.  Choose **Create security group**.
    
45.  For **Security group name**, enter `Web-Server2-SG`
    
46.  For **Description**, enter `Allows HTTP access`
    
47.  For **VPC**, clear the selection and then choose **Lab-vpc**.
    
48.  In the **Inbound rules** section, choose **Add rule**, and then configure the following settings:
    
  -   For **Type**, choose **HTTP**.
        
  -   From the **Source type** dropdown list, choose **Anywhere IPv4**.
       
  -   For **Description**, enter `Allow web access`.

![29](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/62f619ec-051a-41ac-9a63-2d35fca512b2)

        
49.  Choose **Create security group**.


![30](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/f9bd477b-39c8-489b-a931-d7ecae60d072)
    

### Task 8: Explore the configuration settings for launching an EC2 instance into your custom VPC

In this task, you explore the **Launch an instance** page, and enter the settings required to launch a new EC2 instance into your custom VPC. However, you will not complete the process and launch a new EC2 instance.

**Note:** In this lab, you do not have permission to create a new EC2 instance.

50.  On the **Services** menu, choose **EC2**.

![31](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/bedea5b5-0fa9-41fe-8b5a-db2ef448153c)
    
51.  In the **Launch instance** section, choose the **Launch instance** button. Configure the following options:
    
  -   In the **Name and tags** pane, in the **Name** text box, enter `Web-Server2`.
        
  -   Choose an Amazon Machine Image (AMI).
        
  -   In the **Application and OS Images (Amazon Machine Image)** section, choose **Amazon Linux**.
            
  -   From the list of Amazon Machine Images, select **Amazon Linux 2 AMI**.
            
        
        **Note:** Do not choose **Amazon Linux 2023 AMI**.
        
 -   Choose an Instance Type:
        
 -   Select **t2.micro**.
            
 -   In the **Key pair (login)** section, from the **Key pair name - _required_** dropdown list, choose **Proceed without a key pair (not recommended)**.

![33](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/6274389f-5862-4276-aed1-74d31d1c8a29)

        
  -   In the **Network settings** section, choose **Edit**.
        
  -   For **VPC - _required_**, choose **Lab-vpc**.
        
  -   For **Subnet**, choose the subnet with **public1** in the name.

  -   Additionally, we create the subnet.

![32](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/ac93774e-1b94-4a34-a334-b0bff571fc3f)
        
-   For **Auto-assign public IP**, choose **Enable**.

-   For **Firewall (security groups)**, choose **Select an existing security group**.
        
-   From the **Common security groups** dropdown list, choose the **Web-Server2-SG** security group.

![34](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/dc2fc63d-86f3-4603-b2b2-3aed22be36ba)


        
-   In the **Advanced Details** section, for **IAM instance profile**, choose **Work-Role**.
        
-   In the **Advanced Details** section, copy the following commands, and paste them into the **User data** text box:
       
``` 
        #!/bin/bash
        
        # Install Apache Web Server and PHP
        
        yum install -y httpd mysql
        
        amazon-linux-extras install -y php7.2
        
        # Download Lab files
        
        wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-EDNETW-1-60961/1-lab-getting-started-vpc/s3/inventory-app.zip
        
        unzip inventory-app.zip -d /var/www/html/
        
        # Download and install the AWS SDK for PHP
        
        wget https://github.com/aws/aws-sdk-php/releases/download/3.62.3/aws.zip
        
        unzip aws -d /var/www/html
        
        # Turn on web server
        
        chkconfig httpd on
        
        service httpd start
  ```  
![35](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/7110b8ed-03ce-4aba-a197-c3ba1596eeb6)


 -   Take a moment to review the settings you entered.
        
 -   In the **Summary** section, choose **Cancel**.
        

Well done! Now you know how to create a custom VPC, and how to deploy a new EC2 instance into it.



You have completed the lab.

52.  Choose End Lab at the top of this page, and then choose **Yes** to confirm that you want to end the lab.

![37](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/30389b85-16cb-454a-b047-f22e6a85a99e)
    



_Your feedback is welcome and appreciated._

**Credits : AWS Educate**
