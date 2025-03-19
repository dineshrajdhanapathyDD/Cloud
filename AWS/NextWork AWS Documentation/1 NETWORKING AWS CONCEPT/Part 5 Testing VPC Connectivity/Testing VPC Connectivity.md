☁️ Step #1 : Set up your VPC basics

 ⬆️ Step #2 : Connect to NextWork Public Server

 🤝 Step #3 : Test connectivity between your EC2 instances

 🛜 Step #4 : Test VPC connectivity with the internet

🗑️ Before You Go: Delete Your Resources

# Testing VPC Connectivity


WHAT YOU'LL NEED

-   An AWS account -  [Create one here!](https://github.com/dineshrajdhanapathyDD/Cloud/blob/main/AWS/NextWork%20AWS%20Documentation/5%20AWS%20BASIC/legendary-aws-account-setup.pdf))

-   Part 1 of this series -  [Build a Virtual Private Cloud](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%201%20Build%20a%20Virtual%20Private%20Cloud)
-   Part 2 of this series -  [VPC Traffic Flow and Security](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%202%20VPC%20Traffic%20Flow%20and%20Security)

-   Part 3 of this series -  [Creating a Private Subnet](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%203%20Creating%20a%20Private%20Subnet%20in%20Your%20Amazon%20VPC)

-   Part 4 of this series -  [Launching VPC Resources](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%204%20Launching%20VPC%20Resources)

KEY CONCEPTS

-   [Amazon VPC](https://www.youtube.com/watch?v=Pazb3rS_Ers)
-   [Amazon EC2](https://youtu.be/fHY1naCZ9Y0?feature=shared)

## ⚡️ 30 second Summary

Welcome to your fifth AWS networking project!

**In your first four networking projects, you've created:**

1.  ☁️ An Amazon VPC (amazing!)
    
2.  🥅 A public subnet (woohoo!)
    
3.  🚪 An internet gateway (go you!)
    
4.  🚏 A route table (so good!)
    
5.  👮‍♀️ A security group (say whaaat!)
    
6.  📋 A Network ACL, aka Network Access Control List (super cool!)
    
7.  🚷 A private subnet (no way!)
    
8.  🚧 A private route table (you superstar!)
    
9.  🚔 A private network ACL (hot damn!)
    
10.  💻 EC2 instances in your public and private subnets (huuuuuuuge!)
    

  
  

If you haven't done the previous project in our networking series,  **Launching VPC Resources**, we'd highly recommend doing that first. This project starts right where the previous one leaves off.

![What you've learnt from your first four networking projects of this series!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/architecture-past.png)

What you've learnt from your first four networking projects of this series!

  

In  **Testing VPC Connectivity,**  we're going to level up by testing our VPC's  **connectivity**  - you'll learn all about this in a minute!

  
  

**Get ready to:**

1.  ⬆️ Connect to your Public Server from the AWS Management Console.
    
2.  🤝 Test connectivity between your EC2 instances.
    
3.  🛜 Test VPC connectivity with the internet.
    

![Today's game plan - we're putting your network's connectivity to the test!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/architecture-today.png)


  
### ☁️ Step #1

### Set up your VPC basics

  

Let's dive straight into and start from where we left off in the last project!

**In this step, you're going to:**

1.  Set up your VPC, subnet, internet gateway, route table, security group, network ACLs.
    
2.  Set up a private subnet, a route table and network ACLs.
    
3.  Launch EC2 instances and set up your private security group.
    

  
  

What a list, you're going to crush it!

  
  

**Set up your VPC in minutes**

Lucky for us, now that we've learnt about the VPC wizard, let's learn how to use it to set up our VPC in minutes.

![Step 1: Yup! We can set up most of this in a single step.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-architecture-past.png)

Step 1: Yup! We can set up most of this in a single step.

  

-   [Log in to your AWS Account.](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26state%3DhashArgsFromTB_ap-southeast-2_fffdf5be4bb1a27e&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=m-aiqeB2UZeXTGXNyugMP8L64zd_AGUxJl4HLnA-X1o&code_challenge_method=SHA-256)
    
-   Head to your  **VPC**  console.
    
-   From the left hand navigation bar, select  **Your VPCs.**
    
-   Select  **Create VPC.**
    
-   We previously stuck to creating a VPC only, but this time let's select  **VPC and more.**
    
-   Under  **Name tag auto-generation**, enter  `NextWork`
    

> 💡  **What does name tag auto-generation do?**  
> Name tag auto-generation is a nifty feature that tags all your VPC resources with a name based on what you enter.
> 
> If you type in  `NextWork`, all your resources will have that in their name tags, making it super easy to track and manage everything linked to your VPC. You'll see this in action soon!

-   The VPC's  **IPv4 CIDR block**  is already pre-filled to  `10.0.0.0/16`
    
-   For  **IPv6 CIDR block**, we'll leave in the default option of  **No IPv6 CIDR block.**
    
-   For  **Tenancy**, we'll keep the selection of  **Default.**
    

> 💡  **What does tenancy mean?**  
> Tenancy in AWS refers to the type of hardware your instances run on. Yup, hardware. After all, the EC2 instances you'll launch into your VPC are hosted in a data centre in your chosen Availability Zone!
> 
> You have two options:
> 
> -   **Default:**  Your instances share hardware with other AWS customers. This is the standard option and is cost-effective because you’re sharing resources.  
>       
>     
> -   **Dedicated:**  Your instances run on hardware that's dedicated to you only. For example, imagine a healthcare company that needs to ensure the highest level of security for patient data. They might choose dedicated tenancy to make sure their servers are completely isolated from other customers, helping them meet compliance standards and keep sensitive information secure. Dedicated does come at a higher cost!
>     

-   For  **Number of Availability Zones (AZs)**, we'll use just  **1**  Availability Zone.
    
-   Make sure the  **Number of public subnets**  chosen is  **1**.
    
-   Make sure the  **Number of private subnets**  chosen is also  **1**.
    
-   Update your public and private subnets' CIDR blocks:
    
    -   Update your public subnet CIDR block to  `10.0.0.0/24`
        
    -   Update your private subnet CIDR block to  `10.0.1.0/24`
        

> 💡  **Why do the subnets' default CIDR blocks finish in /20 by default?**  
> Great observation! The default /20 subnet provides 4,096 IP addresses, which is a good middle ground for most use cases. Typically the norm is to use  **8 /16 /24 /32:**
> 
> -   `/8`: Provides 16,777,216 IP addresses (usually for very large networks, not subnets).
>     
> -   `/16`: Provides 65,536 IP addresses (often used for VPCs).
>     
> -   `/24`: Provides 256 IP addresses (commonly used for smaller subnets).
>     
> -   `/32`: Provides just one IP address (used for specific instances).
>     
> -   The /20 size offers a balance between too few and too many IP addresses, making it useful for most network setups without overwhelming you with an excessive number of IPs.
>     

![Step 1: Your subnets' CIDR blocks.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step4.5.png)

Step 1: Your subnets' CIDR blocks.

  

-   Next, for the  **NAT gateways ($)**  option, make sure you've selected  **None.**  As the dollar sign suggests, NAT gateways cost money!
    

![Step 1: Make sure you select None for NAT gateways!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step4.6.png)

Step 1: Make sure you select None for NAT gateways!

  

> 💡  **What are NAT gateways, how are they different from internet gateways?**  
> NAT (Network Address Translation) gateways let instances in  **private**  subnets access the internet for updates and patches, while blocking inbound traffic.
> 
> For example, NextWork Private Server in your private subnet might need to download security updates. By using a NAT gateway, the server can access these updates securely while remaining protected from external threats!
> 
> On the other hand, internet gateways let instances in  **public**  subnets communicate with the internet both ways i.e. both inbound and outbound traffic.

-   Next, for the  **VPC endpoints**  option, select  **None.**
    

> 💡  **What are VPC endpoints?**  
> Normally, to access some AWS services like S3 from your VPC, your traffic would go out to the public internet.
> 
> But, VPC endpoints let you connect your VPC privately to AWS services without using the public internet. This means your data stays within the AWS network, which can improve security and reduce data transfer costs.
> 
> There are many types of VPC endpoints, and the  **S3 Gateway**  endpoint is the most common and useful one - many applications need to access S3 for storing or retrieving data after all! The endpoints for other AWS services can be added later, but this setup tool simplifies the initial setup by focusing on S3.
> 
>   
> 💡  **Why does traffic to some services like S3 go out to the public internet by default?**  
> Not all AWS resources are automatically placed inside your VPC! While your compute resources (like EC2 instances) reside within your VPC, S3 buckets and some other AWS services exist outside your VPC because they're designed to be highly available and accessible from anywhere.
> 
> That's why VPC endpoints, like the S3 Gateway endpoint, exist to create a private connection between your VPC and S3. Having a VPC endpoint means your instances can now access services like S3 directly without routing through the public internet, which makes sure your data stays within the AWS network for security.
> 
> That's your teaser on VPC endpoints, we will get into them in detail we learn about endpoints later in this series! 👀

-   You can leave the  **DNS options**  checked.
    

![Step 1: You can leave the DNS options checked!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step4.8.png)

Step 1: You can leave the DNS options checked!

  

> 💡  **What are DNS hostnames and resolution?**  
> When you enable  **DNS hostnames**, your EC2 instances can have human-readable names, like  **denzelnextwork.compute-1.amazonaws.com**, instead of just numeric IP addresses. This makes it simpler to identify and connect to your instances.
> 
> When you enable  **DNS resolution**, AWS takes care of translating these hostnames to their corresponding IP addresses so that network requests can find the correct instance. This is particularly useful in environments where IP addresses might change - hostnames can stay consistent, so references to your resource would still point to the right thing.

-   Select  **Create VPC.**
    

![Step 1: Your VPC workflow updates faaassst](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step4.9.png)

Step 1: Your VPC workflow updates faaassst

  

-   Select  **View VPC**.
    
-   Select the  **Resource map**  tab.
    

![Step 1: You can still see your VPC's resource map!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step4.10.png)

Step 1: You can still see your VPC's resource map!

  

-   Note how name tag auto-generation, which you enabled in the set up page, is at work now - all of your VPC's resources have  `NextWork`  at the start of the name!
    
-   Within your resource map, click on your  **public subnet.**
    
-   Oooo, now you get to see how your public subnet is connected to a  **public route table**  and an  **internet gateway.**  Perfect - that's exactly how we'd set it up from scratch.
    

![Step 1: A highlighted relationship map for your public subnet!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step4.11.png)

Step 1: A highlighted relationship map for your public subnet!

  

**Validate and rename your resources**

Let's tidy up our resources' names! Take 3 minutes to rename your:

-   **VPC**
    
    -   Select  **Your VPCs**  from the left hand navigation panel.
        
    -   Hover over  **NextWork-vpc**  and select the pencil icon.
        
    -   Rename your VPC to  `NextWork VPC`
        
    -   Select  **Save.**
        

![Step 1: Rename your VPC!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step4.12.png)

Step 1: Rename your VPC!

  

-   **Subnets**
    
    -   Select  **Subnets**  from the left hand navigation panel.
        
    -   Rename your public subnet i.e.  **NextWork-subnet-public1-xxx**  to  `NextWork Public Subnet`
        
    -   Rename your private subnet i.e.  **NextWork-subnet-private1-xxx**  to  `NextWork Private Subnet`
        

  
  

-   **Route tables**
    
    -   Select  **Route tables**  from the left hand navigation panel.
        
    -   Rename your public route table i.e.  **NextWork-rtb-public**  to  `NextWork Public Route Table`
        
    -   Rename your private route table i.e.  **NextWork-rtb-private1-xxx**  to  `NextWork Private Route Table`
        

  
  

-   **Internet gateway**
    
    -   Select  **Internet gateways**  from the left hand navigation panel.
        
    -   Rename your internet gateway i.e.  **NextWork-igw**  to  `NextWork IG`
        

  
  

-   **Network ACLs**
    
    -   Select  **Network ACLs**  from the left hand navigation panel.
        
    -   Select  **Create network ACL**  on the top right.
        
    -   For the name, enter  `NextWork Private NACL`
        
    -   Select  **NextWork VPC**.
        
    -   Select  **Create network ACL**.
        
    -   Select the checkbox next to  **NextWork Private NACL.**
        
    -   Switch tabs to  **Subnet associations.**
        
    -   Select  **Edit subnet associations.**
        
    -   Select your  **private**  subnet.
        
    -   Select  **Save changes.**
        
    -   To tidy up your network ACLs' naming conventions, let's also rename your VPC's default NACL to  `NextWork Public NACL`  
        _🧠 Hint: the other network ACL with just 1 subnet associated is your VPC's default network ACLs!_
        
    -   Observe the  **Inbound rules**  and  **Outbound rules**  tabs for your private network ACL.
        

> 💡  **Why are they both denying all traffic?**  
> Remember that custom network ACLs start with denying all inbound and outbound traffic! We'll leave these settings for now - let's customise them later in this networking series, when we know exactly which traffic source we're wanting to allow.

![Step 1: All inbound and outbound traffic is denied for your Private NACL!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step2.11.png)

Step 1: All inbound and outbound traffic is denied for your Private NACL!

  

-   **Security groups**
    
    -   Select  **Security groups**  from the left hand navigation panel.
        
    -   Yay default security groups have already been set up for us! Their names are  **default**  and...  **default.**  😅
        
    -   Select either one of the two and observe its inbound rules.
        
    -   Hmmm these  **default**  security groups don't quite have the same inbound rules as the ones we used to set up ourselves.
        
    -   Let's create new security groups instead of using these default ones.
        
    -   Choose **Create security group**.
        
    -   Security group name: `NextWork Public Security Group`
        
    -   Description:  `A Security Group for the NextWork VPC Public Server`
        
    -   VPC: **NextWork VPC.**
        
    -   Under the  **Inbound rules**  panel, choose **Add rule.**
        
    -   Type:  `HTTP`
        
    -   Source: `Anywhere-IPv4`
        
    -   At the bottom of the screen, choose **Create security group.**
        

  
  

WOOO! Well done on setting up your VPC. Now it's time to see your VPC in action...

  
  

**Launch a new EC2 instance in NextWork Public Subnet**

Let's kick things off by launching an EC2 instance in your public subnet.

![Step 1: Let's launch a public EC2 instance.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step2.0.png)

Step 1: Let's launch a public EC2 instance.

  

-   Head to the  **EC2 console**  - search for  `EC2`  in the search bar at the top of screen.
    

![Step 1: Search for EC2.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step3.1.png)

Step 1: Search for EC2.

  

-   Select  **Instances**  at the left hand navigation bar.
    
-   Select  **Launch instances**.
    
-   Since your first EC2 instance will be launched in the public subnet, let's name it  `NextWork Public Server`
    
-   For the  **Amazon Machine Image,**  select  **Amazon Linux 2023 AMI.**
    
-   For the  **Instance type,**  select  **t2.micro.**
    

![Step 1: Select a Free Tier eligible AMI and instance type.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step3.3.png)

Step 1: Select a Free Tier eligible AMI and instance type.

  

-   For the  **Key pair (login)**  panel, select  **NextWork key pair.**
    
    -   NOTE: If you've never created  **NextWork key pair**, or you've deleted it, all you have to do is:
        
        -   Select  **Create new key pair.**
            
        -   For the  **Key pair name**, use  `NextWork key pair`
            
        -   Keep the  **Key pair type**  as  **RSA**.
            
        -   Keep the  **Private key file format**  as  **.pem**.
            
        -   Select  **Create key pair**.
            

> 💡  **What is a key pair? Why do we need one?**  
> Key pairs are a powerful tool that help engineers directly access their virtual machines, like EC2 instances.
> 
> How key pairs work is that they consist of two cryptographic keys: one private and one public. The public key is installed on the virtual machine, and the private key remains with the user. When you attempt to connect, the machine uses the public key to create an encrypted challenge that can only be decrypted with the private key, ensuring secure and authenticated access.
> 
>   
> 💡  **Directly access a virtual machine? What does that mean?**  
> Directly accessing a virtual machine means logging into and managing the operating system or software of the machine as if you were using it in front of you, but over the internet.
> 
> You might've launched an EC2 instance before without ever needing a key pair, and that would be because your interactions were managed through higher-level AWS services e.g. AWS Lambda, AWS CodeBuild that take care of accessing your EC2 instance for you!
> 
> In this project, we're needing to directly access this EC2 instance because we are running connectivity tests in the next step. Direct access to the instance is required to run our tests directly on the instance's terminal.
> 
>   
> 💡  **Psstt... just so you know 👀**  
> We're later going to use an EC2 tool that lets us get direct access to your EC2 instance  _without_  having to create your own key pair. Buttttt we're creating one in this step so you can learn about key pairs!

-   At the  **Network settings**  panel, select  **Edit**  at the right hand corner.
    

> 💡  **Why are we editing the Network settings?**  
> By default, all resources are launched into the default VPC that AWS has set up for your account. We need to tell AWS that we actually want to launch this instance in  **NextWork VPC**  and the  **NextWork Public Subnet**!

-   Select  **NextWork VPC**  from the drop-down in the VPC list.
    
-   Select your public subnet.
    
-   Update the  **Auto-assign public IP**  setting to  **Enable.**
    
-   For the  **Firewall (security groups)**  setting, we've already created a security group - let's use that!
    
-   Choose  **Select existing security group.**
    
-   Select  **NextWork Public Security Group.**
    
-   Select  **Launch instance.**
    
-   Click into your instance once it's successfully launched.
    

![Step 1: Great success with launching your EC2 instance!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step3.7.png)

Step 1: Great success with launching your EC2 instance!

  

-   Select the checkbox next to your instance, and a  **Details**  panel pops up!
    
-   Switch the tab to  **Networking**.
    
-   Notice how NextWork Public Server has a Public IPv4 address, a subnet, an Availability zone, and a VPC ID.
    

![Step 1: NextWork Public Server's Networking details.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step3.8.png)

Step 1: NextWork Public Server's Networking details.

  

> 💡  **What do all this information mean?**  
> As a quick recap:  
>   
> 
> -   The  **Availability Zone**  is the specific area within your AWS Region that your instance is hosted.
>     
> -   The  **VPC ID**  identifies that within the AWS Region you're using, the Public Server belongs in your  **NextWork VPC**.
>     
> -   The  **NextWork Public Subnet**  determines the range of IP addresse within NextWork VPC that can be assigned to your EC2 instance. Because this subnet has a route to an internet gateway, your VPC has opened up communication between all resources in the subnet and the internet.
>     
> -   The  **Public IPv4 address**  is the external IP address assigned to your EC2 instance. This address is globally unique, so no other server has the same public IPv4 address on the internet! Having a public IPv4 address means your instance can communicate with the internet and be accessible from outside your private AWS network.
>     

  
  

**Launch a new EC2 instance in NextWork Private Subnet**

Let's follow similar steps to launch your  **private**  subnet!

![Step 1: Let's launch a private EC2 instance.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step3.0.png)

Step 1: Let's launch a private EC2 instance.

  

-   Select  **Launch instances**  again.
    
-   Name:  `NextWork Private Server`
    
-   Amazon Machine Image (AMI):  **Amazon Linux 2023 AMI**
    
-   Instance type:  **t2.micro**
    
-   Key pair:  **NextWork key pair**
    
-   At the  **Network settings**  panel, select  **Edit.**
    
-   Network:  **NextWork VPC**
    
-   Subnet:  **NextWork Private Subnet**
    
-   **Firewall (security groups):**  Select  **Create security group.**
    
    -   For  **Security group name,**  let's use  `NextWork Private Security Group`
        
    -   For  **Description**, we'll replace the default value with  `Security group for NextWork Private Server.`
        
    -   Notice that under the  **Inbound Security Group Rules**  section, there is a rule with  **Type**  set to  **ssh**.
        

> 💡  **What is SSH?**  
> SSH, or Secure Shell, is the protocol we use for secure access to a remote machine. When you connect to the instance, SSH verifies you possess the correct private key corresponding to the public key on the server, ensuring only authorized users can access the instance.
> 
> In terms of network communication, SSH is also as a type of network traffic. Once SSH has established a secure connection between you and the EC2 instance, all data transmitted (including your commands and the responses from the instance) is encrypted. This encryption makes SSH an ideal method for securely exchanging confidential data e.g. login credentials!
> 
>   
> 💡  **How common is it for developers to use SSH?**  
> SSH is  _extremely_  common and is the standard way for developers to securely log in from their computer to another remote computer (e.g., an EC2 instance).
> 
> More and more organizations try to reduce the use of SSH and prefer infrastructure as code (IaC) and automated deployments to reduce the need for direct access (and minimize human error and security risks), but SSH access is still essential for many administrative, testing, and troubleshooting scenarios. For example, developers today use SSH to troubleshoot a live issue, perform manual updates, or configure system settings that are not easily automated.
> 
>   
> 💡  **What is this yellow banner saying?**  
> 
> ![Step 1: A yellow banner pops up!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step3.9.png)
> 
> Step 1: A yellow banner pops up!
> 
> This popup says "Rules with source of 0.0.0.0/0 allow all IP addresses to access your instance. We recommend setting security group rules to allow access from known IP addresses only."
> 
> AWS is concerned that the default security rule, i.e. with the source being  `0.0.0.0/0`, allows any IP address to access your resource using SSH.
> 
> We were okay with allowing HTTP traffic from  `0.0.0.0/0`  for our  **public**  subnet, but the  **private**  subnet is a different story!

-   Change the  **Source type**  from  **Anywhere**  to  **Custom.**
    
-   In the  **Source**  drop down, scroll down and select  **NextWork Public Security Group.**
    

> 💡**What does it mean to select NextWork Public Security Group instead of Anywhere as our source?**  
> Choosing the  **NextWork Public Security Group**  as the source means only resources that are part of the NextWork Public Security Group can communicate with your instance. This restricts access to a much smaller group of trusted resources, rather than allowing potentially any IP address on the internet (`0.0.0.0/0`) to access your instance. A great move for securing a private subnet!

![Step 1: Select the NextWork Public Security Group as your source.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/ec2-high-step3.10.png)

Step 1: Select the NextWork Public Security Group as your source.

  

-   Select  **Launch instance.**
    

  
  

Fantastic! You've done an incredible job setting up your VPC and EC2 instances.

Now let's dive into what's next for your network. 🤿

### ⬆️ Step #2

### Connect to NextWork Public Server

  

Let's try talking to NextWork Public Server!

  
  

**In this step, you're going to:**

-   Set up a connection to your Public Server  _(let's gooooo!)_
    
-   Troubleshoot a connection issue  _(activate detective mode!)_
    

![Step 2: Let's test the connectivity from you to your Public Server.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step2.0.png)

Step 2: Let's test the connectivity from you to your Public Server.

  

-   Still in your  **EC2**  console, select  **Instances**  from the left hand navigation panel.
    
-   Select the checkbox next to  **NextWork Public Server.**
    
-   Select  **Connect**.
    

> 💡  **What does connectivity mean? Why is it important?**  
> Connectivity is all about how well different parts of your network talk to each other and with external networks. It's essential because connectivity is how data flows smoothly across your network, powering everything from simple web hosting on the Internet to complex operations e.g. Netflix using over 100,000 EC2 instances to power its streaming platform. Solid connectivity is the backbone of any system that relies on network interactions, making every communication and operation reliable and efficient.
> 
>   
> 💡  **What connectivity are we setting up and testing?**  
> Now that we've set up a public server and a private server, let's test whether we can get your EC2 instances to talk to each other despite being in different subnets. Connectivity testing often involves fine-tuning your security group settings and network ACLs to make sure the right traffic can flow in and out of your instances as you'd expect!

-   Keep all of the default settings.
    

![Step 2: Use EC2 Instance Connect.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.1.png)

Step 2: Use EC2 Instance Connect.

  

> 💡  **What is EC2 Instance Connect?**  
> EC2 Instance Connect is a shortcut way to get direct SSH access to your EC2 instance!
> 
> When you use SSH to connect to an EC2 instance, you usually have to:
> 
> -   Generate a key pair (public and private keys).
>     
> -   Associate the public key with your EC2 instance.
>     
> -   Securely store the private key on your local machine.
>     
> -   Set up an SSH client (a software that can handle the SSH protocol, such as Terminal on a Mac or Linux computer), provide it your private key, and establish a secure connection to your EC2 instance.
>     
> 
>   
> **EC2 Instance Connect**  is an alternative way to use SSH - Instance Connect lets you securely connect to your EC2 instances directly using the AWS Management Console. You're still using SSH, but with all the key management handling it for you. This takes away a lot of the complexity of setting up SSH.
> 
> Here's how EC2 Instance Connect works:
> 
> -   It generates a one-time-use SSH key pair on your behalf when you initiate a connection.
>     
> -   It automatically links the public key to the EC2 instance.
>     
> -   It allows the key to be used for a short period (typically 60 seconds), after which it is automatically deleted.
>     
> 
> ![Step 2: EC2 Instance Connect manages key pairs for us.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.1.5.png)
> 
> Step 2: EC2 Instance Connect manages key pairs for us.
> 
>   
> 
>   
> 💡  **What do Public IP address and Username mean on the Instance Connect set up page?**
> 
> -   **Username:**  This is the user account that you will log into on your EC2 instance. It's just like a physical computer - when you switch on your laptop, you usually have to enter a password to log into a specific user account! The default username is usually "ec2-user".
>     
> -   **Public IP address:**  This is the external IP address assigned to your EC2 instance! You'll use this address to tell EC2 Instance Connect the destination when setting up your SSH connection. Having a Public IP address is a must when connecting to an EC2 instance over Instance Connect - that's why it was so important to enable automatically assigning a public address to your Public Subnet's resources!
>     

-   Select  **Connect.**
    
-   Oh no! We've failed to connect to our instance?!
    

![Step 2: Oh snap! An error 👀](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.2.png)

Step 2: Oh snap! An error 👀

  





Let's investigate what happened by reviewing our security settings.

Look at you go, this is an iconic move for anyone testing their VPC's connectivity!

-   Head back to your  **VPC console.**
    
-   Select  **Subnets**  from the left hand navigation panel.
    
-   Select the checkbox next to  **NextWork Public Subnet.**
    
-   Hmm let's take a look! Investigate the  **Route table**  and  **Network ACL**  tabs - what do you see?
    

![Step 2: Your public subnet's route table.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.3.png)

Step 2: Your public subnet's route table.

  

![Step 2: Your public subnet's network ACLs.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.4.png)

Step 2: Your public subnet's network ACLs.

  

> 💡 Everything looks good! Our Network ACL allows all traffic in and out, and our route table is correctly setting up a route to the Internet Gateway.

-   Hmmm that leaves one more thing to investigate...
    
-   Head into the  **Security groups**  page from the left hand navigation bar.
    
-   Select the checkbox next to  **NextWork Public Security Group.**
    
-   Select the  **Inbound rules**  tab.
    
-   Aha! Mystery solved.
    

![Step 2: NextWork Public Server's security group's inbound rules.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.5.png)

Step 2: NextWork Public Server's security group's inbound rules.

  

> 💡  **Mystery solved?! How are our inbound rules the cause of our connectivity issue?**  
> The security group associated with NextWork Public Server lets in all inbound  **HTTP**  traffic, but this is not how we're trying to access our Public Server!
> 
> We're trying to access NextWork Public Server using  **SSH**  through EC2 Instance Connect, which is a different traffic type.

-   In the  **Inbound rules**  tab, select  **Edit inbound rules.**
    
-   Select  **Add rule.**
    
-   For your new rule, configure the  **Type**  as  **SSH.**
    
-   Then, under  **Source type**, select  **Anywhere-IPv4.**
    

> 💡  **What am I doing here? Why do we select Anywhere-IPv4?**  
> In this step, you are updating NextWork Public Server's security group so it can let in SSH traffic. Choosing  **Anywhere-IPv4**  as the source lets in SSH connections from  **any**  IPv4 address.
> 
> It's generally not best practice to set SSH access to "Anywhere-IPv4" due to security risks - this setup exposes your server to potential unauthorized access from any location.
> 
> But, we're using it in this instance (pun intended) as EC2 Instance Connect picks from  **various IP address ranges**  (not just a single IP) to initiate SSH access. Setting the source to  **Anywhere-IPv4**  makes sure that EC2 Instance Connect will be successful, no matter which IP address it's using.
> 
> If this was a long-term project, we'd search for the specific CIDR block of IP addresses that EC2 Instance Connect uses and restrict inbound SSH traffic to that range.

![Step 2: Select Anywhere IPv4.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.6.png)

Step 2: Select Anywhere IPv4.

  

-   Select  **Save rules.**
    
-   With that modified, refresh your EC2 console's  **Instances**  page.
    
-   Select your  **Public Server**  and select  **Connect**  again.
    
-   Phew! Success.
    

![Step 2: Woah! We're in - welcome to NextWork Public Server!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.7.png)

Step 2: Woah! We're in - welcome to NextWork Public Server!

  

> 💡  **Wow this is my first time connecting to an EC2 instance! What am I seeing here?**  
> Woohooo welcome to your very first peek into an Amazon EC2 instance connection! Let’s break down what you’re seeing here.
> 
> This screen with text and a blinking cursor is called a  **terminal**  or  **command line interface (CLI).**  Think of it as a way to talk directly to your computer using text commands, like you're texting with your computer!
> 
> Historically, before we had the colorful icons and windows that you can click on with a mouse, everyone used terminals like this to interact with computers. Now, we use the terminal for specific/advanced tasks (beyond opening folders or renaming files), especially when dealing with servers or programming. Using the terminal/CLI can be much faster and more powerful than clicking through menus, and it's absolutely used by engineers today.
> 
> The text  **ec2-user@ip-10-x-x-xxx**  on the screen tells you  **who**  you are (the ec2-user) and  **where**  you are (on a computer with the address 10.0.0.xxx). Bonus points to you if you can figure out where you can find this IP address in your EC2 console!





### 🤝 Step #3

### Test connectivity between your EC2 instances

  

Awesome, we've figured out how to connect with our Public Server!

Let's see if we can connect with our  _Private_  Server from here.

  
  

**In this step, you're going to:**

-   Get your Public Server to talk to your Private Server  _(hellooo!)_
    
-   Troubleshoot another connection issue  _(detective mode stays on!)_
    

> 💡  **What does it mean to connect to our Private Server from our Public Server?**  
> When our servers "talk" or connect, it usually means the public server is sending or requesting data from the private server.
> 
> This could be for various reasons, such as fetching private information (e.g. retrieving screenshots that a NextWork student uploaded into a project guide), or updating databases (e.g. a student updates their profile photo in the NextWork community).

![Step 3: Let's test the connectivity from your Public Server to your Private Server.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step3.0.png)

Step 3: Let's test the connectivity from your Public Server to your Private Server.

  

-   Leave open the  **EC2 Instance Connect**  tab, but head back to your  **EC2**  console in a new tab.
    
-   Select  **NextWork Private Server**.
    
-   Copy your private server's  **Private IPv4 address.**
    

![Step 3: Copy NextWork Private Server's private IPv4 address.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.8.png)

Step 3: Copy NextWork Private Server's private IPv4 address.

  

-   Switch back to the  **EC2 Instance Connect**  tab.
    
-   Run  `ping [the Private IPv4 address you just copied]`  in terminal.
    
    -   Your final result should look similar to something like  `ping 10.0.1.227`
        
    -   Don't know where to enter this prompt? Look for the  `$`  sign at the bottom line of the black window, and type in your command after the $ sign.
        

> 💡  **What does ping mean?**  
> **Ping**  is a common computer network tool used to check whether your computer can communicate with another computer or device on a network.
> 
> Think of it like sending a tiny message that says "hello, are you there?" to another computer, or like checking if someone's home by ringing their doorbell.
> 
> When you "ping" a specific IP address address (i.e. another server's address), your server (in this case, NextWork Public Server) sends a small packet of data to that address (NextWork Private Server), asking for a response. Ping will tell you whether you get a response back and how long it took to get a response.
> 
> If you receive a response quickly, it means the connection between your computer and the other computer is good. If it takes a long time or you get no response, there might be a problem with the connection!

-   You should see a response similar to this:
    

![Step 3: Do you get a single line as the response too?](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.9.png)

Step 3: Do you get a single line as the response too?

  



> 💡  **What does this response mean? Is it a good response?**  
> This single line indicates that your Public Server has sent out a ping message... and that's about it.
> 
> Usually, when you ping another computer successfully, you should see  **several**  replies back instantly. Each reply tells you how long it took for the message to go to the Private Server and come back.
> 
> If you don't get any replies (that's our situation right now), or if the replies stop suddenly, it's usually a sign that there's a problem with the connection.
> 
> ![Step 3: Your Public Subnet isn't hearing a response back ](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step3.ping.png)
> 
> Step 3: Your Public Subnet isn't hearing a response back
> 
> 💡  **Why is there a problem with the connection between my servers?**  
> One common reason for these issues is that the target machine (i.e. NextWork Private Server) or its network might be blocking the type of messages used in ping, which are known as  **ICMP (Internet Control Message Protocol) traffic.**
> 
> Blocking ICMP traffic is often done to prevent network attacks, like attackers can overwhelming a server with ping messages so it can't respond to real users wanting to use your application. Fair enough that ICMP traffic is blocked by default!

-   To resolve this connectivity error, let's investigate whether NextWork Private Server is allowing in ICMP traffic.
    

> ⏸️  **Pause and have a think - where do you think you can investigate this?**  
> Up til now, you've learnt about internet gateways, subnets, route tables, IPv4 addressing, security groups and route tables...
> 
> Which of these would you need to configure for NextWork Private Server to receive ICMP traffic?
> 
> Hmmm!  
> 🤔  
> 🤔  
> 🤔

-   ▶️ Alright, resuming now!
    
-   Leave open the  **EC2 Instance Connect**  tab, but head back to your  **VPC**  console in a new tab.
    
-   In the VPC console, select the  **Subnets**  page.
    
-   Select  **NextWork Private Subnet.**
    
-   Let's investigate the  **Route tables**  and  **Network ACL**  tabs for your private subnet.
    
-   Aha! Mystery solved.
    

![Step 3: NextWork Private Server's network ACLs.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.10.png)

Step 3: NextWork Private Server's network ACLs.

  

> 💡  **Mystery solved?! How are the Route tables and Network ACLs the cause of our connectivity issue?**  
> Our route table is set up perfectly (zero issues there!), but the  **Network ACL**  tab shows us that  **all**  traffic inbound and outbound are denied.
> 
> This means even if our route table correctly directs the ping to NextWork Private Server, the network ACL is checking the ping traffic at the entrance of your private subnet. If it finds that ICMP traffic is not allowed, it stops the ping there.
> 
> This blockage could be the reason why you observed only one line in the ping response - the single line records NextWork Public Server's first attempt to communicate (i.e. a ping message is sent), but there are no replies back from NextWork Private Server.

-   Let's resolve that by clicking on the link to your  **NextWork Private NACL.**
    
-   Select the checkbox next to  **NextWork Private NACL.**
    
-   Select the  **Inbound rules**  tab.
    
-   Select  **Edit inbound rules.**
    
-   Let's add a new rule to let NextWork Public Server ping NextWork Private Server.
    
-   Select  **Add new rule.**
    
-   Assign  `100`  as the rule number.
    
-   Change the  **Type**  to  **All ICMP - IPv4**.
    

> 💡  **What is ICMP - IPv4?**  
> When you set a rule for  **All ICMP - IPv4**, you're allowing all types of ICMP messages for IPv4 addresses. This covers a wide range of operational messages that are essential for diagnosing network connectivity issues, ping requests and responses are just one type of ICMP messages.
> 
> You might notice that ICMP is not limited to IPv4; there is also ICMP for IPv6 , which functions similarly but is tailored specifically for IPv6 networks.

-   Set the  **Source**  to traffic coming from your public subnet -  `10.0.0.0/24`
    
-   Select  **Save changes.**
    

![Step 3: Allow inbound ICMP traffic.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.11.png)

Step 3: Allow inbound ICMP traffic.

  

-   Let's apply the same to Outbound rules.
    
    -   Rule number:  `100`
        
    -   Type:  **All ICMP - IPv4**.
        
    -   Source:  `10.0.0.0/24`
        
-   Before we finish, let's check the security groups! Select  **Security groups**  from the left hand navigation panel.
    
-   Select  **NextWork Private Security Group.**
    
-   Check your  **Inbound rules**  tab - does this security group allow ICMP traffic? (Nope!)
    

![Step 3: NextWork Private Server's security group's inbound rules.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.12.png)

Step 3: NextWork Private Server's security group's inbound rules.

  

> 💡  **Why does it matter whether my security group is allowing ICMP traffic too?**  
> Now that your private network ACLs allow ICMP traffic, ICMP messages can enter your public subnet. However, these messages still need to be let in by your  **NextWork Private Security Group**  to reach your private server.
> 
> Imagine the ICMP ping as a delivery car that needs to deliver the ping message to a specific house (NextWork Private Server) in a gated neighbourhood (your private subnet). It's allowed through the big security checkpoint (the network ACL) into the neighbourhood, but it still needs to pass a final check with the security guard (security group) at the house's door.
> 
> So if your security group isn't allowing in ICMP traffic too, the ping message wouldn't reach your private server!
> 
> ![Step 3: If your Private Security Group wasn't allowing inbound ICMP traffic too.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.11.5.png)
> 
> Step 3: If your Private Security Group wasn't allowing inbound ICMP traffic too.
> 
>   

-   Select  **Edit inbound rules.**
    
-   Select  **Add rule.**
    
-   For  **Type**, select  **All ICMP - IPv4.**
    
-   For  **Source**, select  **NextWork Public Security Group**.
    

![Step 3: Allow traffic from the NextWork Public Security Group.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.13.png)

Step 3: Allow traffic from the NextWork Public Security Group.

  

> 💡  **Hmmm, we didn't pick NextWork Public Security Group as the source for the network ACL... why is the source different here?**  
> Good catch! Notice how we can select traffic from the  **NextWork Public Security Group**  as a source here, which is much more granular and exclusive than the private NACL, which allows in all traffic from your public subnet.
> 
> NACLs typically have a broader scope since its settings would affect all resources in your subnet.
> 
> **We can also illustrate this with an example scenario.**  How should you set up your private network ACLs and security groups if you had two servers in each subnet, and each public server only needs to talk to one of the private servers?
> 
> Your private network ACL is on the subnet level so it would need to allow in traffic from both public servers. However, since security groups are only on the instance level, it can have much more granular inbound rules.
> 
> ![Step 3: The difference in scope between NACLs and security groups for larger networks.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.12.5.png)
> 
> Step 3: The difference in scope between NACLs and security groups for larger networks.
> 
>   

-   Select  **Save rules.**
    
-   Revisit the  **EC2 Instance Connect**  tab that's connected to NextWork Public Server.
    
-   Woah! Lots of new lines coming through in the terminal.
    

![Step 3: New responses from your ping are here!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.14.png)

Step 3: New responses from your ping are here!

  

> 💡  **What do these new lines mean?**  
> The multiple new lines appearing in your terminal are a sign of successful communication between the two EC2 instances - wohoooo!
> 
> Each line represents a reply from the ping command you sent. This means that the ICMP (Internet Control Message Protocol) traffic is now successfully reaching the private server, thanks to the adjustments you made in the network ACLs and Security Groups. Nice!
> 
> ![Step 3: Your Public Server now gets replies from the Private Server!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step3.ping2.png)
> 
> Step 3: Your Public Server now gets replies from the Private Server!
> 
>   
> 
> **Extra for Experts:**  Curious about what each part of the ping message means? The output typically shows several pieces of information:
> 
> -   **Time:**  Each line includes the time in milliseconds it took for the ping message to travel from your server to the target and back. This is a measure of the latency or delay in the network communication.
>     
> -   **TTL (Time to Live):**  This value indicates the lifespan of the packet as it travels; it decreases by one for each router it passes through. Once TTL reaches zero, the data packet containing the ping message is automatically dropped from the network.
>     
> -   **Sequence number:**  This helps in identifying each ping request and matching it to its corresponding reply, ensuring that the responses correspond to the specific requests sent.
>     



### 🛜 Step #4

### Test VPC connectivity with the internet

  

Since your NextWork Public Route Table has a route from the NextWork Public Subnet to an internet gateway, you can validate that resources in NextWork Public Subnet can access the internet!

  
  

**In this step, you're going to:**

-   Get your Public Server to talk to the internet  _(off we go!)_
    
-   Troubleshoot an error response  _(awesome learnings here!)_
    

![Step 4: Let's test the connectivity from your Public Server to the public internet!](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step4.0.png)

Step 4: Let's test the connectivity from your Public Server to the public internet!

  

-   Quit the ping command by pressing  `Control + C`  on your keyboard.
    
-   Let's enter a new command!
    
-   Type in  `curl example.com`  in the prompt, i.e. right after the $ sign at the bottom line of the black window.
    
-   You should see a response similar to this!
    

![Step 4: The response from running `curl example.com`.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step5.1.png)

Step 4: The response from running `curl example.com`.

  

> 💡  **What does curl mean?**  
> Just like ping,  **curl**  is a tool to test connectivity in a network. Where ping checks if one computer can contact another (and how long messages take to travel back and forwth),  **curl**  is used to transfer data to or from a server. That means on top of checking connectivity, you can use curl to grab data from, or upload data into other servers on the internet!
> 
>   
> 💡  **What does the output say?**  
> When you use the  `curl`  command followed by a website address, e.g.  `example.com`, the command sends an HTTP request to the server that hosts the website. This request tells the server that you want to retrieve the HTML content of the website. The website's server then processes this request and sends back the data as a response.
> 
> The curl command outputs this data to your terminal, so what you're seeing is the raw HTML from the server!

-   This output confirms that your  **Public Sever**  instance can talk with the internet.
    
-   This wouldn't be possible if NextWork Public Subnet, your internet gateway and your security settings weren't set up properly... nice work!
    
-   Now let's run  `curl nextwork.org`
    

![Step 4: The response from running `curl nextwork.org`.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step5.2.png)

Step 4: The response from running `curl nextwork.org`.

  

> 💡  **What does this output mean?**  
> The output  **Found**  typically means that the website at the URL you entererd has moved to a new URL! This is true -  `nextwork.org`  currently redirects requests to the first project on our web app, which has a different URL!

-   Now let's try running curl with the URL that your terminal returned. Run  `curl https://learn.nextwork.org/projects/aws-host-a-website-on-s3`
    

![Step 4: The response from running curl https://learn.nextwork.org/projects/...](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step5.3.png)

Step 4: The response from running curl https://learn.nextwork.org/projects/...

  

> 💡  **Woah that's heaaaaps more data coming through now! What does this response say?**  
> Just like the previous example using curl  `example.com`, curl has fetched the complete HTML content of NextWork's web app (specifically, the first project on the web app), which is why you now see a large amount of HTML data.
> 
> Nice work, you've just used your Public Server to fetch all the HTML code necessary to render a webpage!




  
  

Congratulations!! That was a massive success in testing your VPC's connectivity between your subnets and with the external internet.

😮‍💨 All Done

### Nice work!

  
```
You've just completed today's project and  **set up your very own VPC AND tested VPC connectivity.**


  
🗑️ Before You Go

### Delete Your Resources

  



✋  **STOP**

Before diving into the steps for deleting your resources, why not challenge yourself to delete everything in this project on your own?

Keeping track of your resources, and deleting them at the end, is absolutely a skill that will help you reduce waste in your account.

  
  

🛑  **STEPS BELOW:**

**Public and Private Servers:**

-   In your  **EC2 console**, select the checkboxes next to both instances.
    
-   Select the  **Instance state**  dropdown, and select  **Terminate instance**.
    
-   Select  **Terminate**.
    

![Step 6: Delete your EC2 instances.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step8.1.png)

Step 6: Delete your EC2 instances.

  

**VPC:**

-   In your  **VPC console**, select the checkbox next to  **NextWork VPC**.
    
-   Select the  **Actions**  dropdown.
    
-   Select  **Delete VPC**.
    
-   If you get stopped from deleting your VPC because  **network interfaces**  are still attached to your VPC - delete all the attached network interfaces first!
    

> 💡  **What is a network interface?**  
> Network interfaces get created automatically when you launch an EC2 instance. Think of them as a component that attaches to an EC2 instance on one end and your VPC on another - so that your EC2 instance is connected to your network and can send and receive data! Network interfaces are usually deleted automatically with your EC2 instance, but on some occassions it'd be faster to delete them manually.

-   Type  `delete`  at the bottom of the pop up panel.
    
-   Select  **Delete**.
    

![Step 6: Delete your VPC.](https://learn.nextwork.org/projects/static/aws-networks-connectivity/high-step8.2.png)

Step 6: Delete your VPC.

  

Now visit each of the pages below!

**Refresh**  your the page before checking if the resource you created today is still in your account. They should be automatically deleted with your VPC, but it's always a good idea to check anyway:

1.  Subnets
    
2.  Route tables
    
3.  Internet gateways
    
4.  Network ACLs
    
5.  Security groups

```

Nice Work!

THAT'S NETWORKING PROJECT FIVE...

DONE!!!!! 🥳

**Today you've learnt how to:**

-   ⬆️ **Connect to your Public Server with EC2 Instance Connect:** You used EC2 Instance Connect in your AWS Management Console to securely SSH into your EC2 instance without the hassle of managing SSH keys. This also required a cheeky update to your Public Server's security group settings.  
      
    
-   🤝 **Test EC2 connectivity with ping:** You made sure that your public and private servers can communicate with each other using the ping command. You also had to update your Private Server's NACL settings to make this work!  
      
    
-   🛜 **Verify VPC internet access with curl:** You confirmed that your virtual network can reach the internet by using the curl command to fetch data directly from web servers, even grabbing entire HTML files in the process.


### 👏 All done!