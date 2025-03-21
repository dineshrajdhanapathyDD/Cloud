
 ☁️ Step #1 : Set up your VPCs in Minutes
 
🌉 Step #2 : Create a Peering Connection

🚏 Step #3 : Update Route Tables

💻 Step #4 : Launch EC2 Instances

🐈 Step #5 : Connect to Instance 1

🐅 Step #6 : Connect to Instance 1 (round two!)

🧪 Step #7 : Test VPC Peering 

🗑️ Before You Go: Delete Your Resources

---

# VPC Peering

Worlds collide - let's get TWO VPCs to talk to each other!



WHAT YOU'LL NEED

-   An AWS account -  [Create one here!](https://github.com/dineshrajdhanapathyDD/Cloud/blob/main/AWS/NextWork%20AWS%20Documentation/5%20AWS%20BASIC/legendary-aws-account-setup.pdf))

-   Part 1 of this series -  [Build a Virtual Private Cloud](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%201%20Build%20a%20Virtual%20Private%20Cloud)
-   Part 2 of this series -  [VPC Traffic Flow and Security](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%202%20VPC%20Traffic%20Flow%20and%20Security)

-   Part 3 of this series -  [Creating a Private Subnet](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%203%20Creating%20a%20Private%20Subnet%20in%20Your%20Amazon%20VPC)

-   Part 4 of this series -  [Launching VPC Resources](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%204%20Launching%20VPC%20Resources)

-   Part 5 of this series -  [Testing VPC Connectivity](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%205%20Testing%20VPC%20Connectivity)

KEY CONCEPTS

-   [Amazon VPC](https://www.youtube.com/watch?v=Pazb3rS_Ers)
-   [Amazon EC2](https://youtu.be/fHY1naCZ9Y0?feature=shared)

## ⚡️ 30 second Summary

Welcome to your sixth AWS networking project!

**In your first five networking projects, you've created:**

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
    
11.  🧪 Connectivity tests to validate your VPC set up (let's GOOO!)
    

  
  

If you haven't done the previous project in our networking series,  **Testing VPC Connectivity**, we'd highly recommend doing that first. This project starts right where the previous one leaves off.

![What you've learnt from your first five networking projects of this series!](https://learn.nextwork.org/projects/static/aws-networks-peering/architecture-past.png)

What you've learnt from your first five networking projects of this series!

  

In this project,  **VPC Peering**  we're going to level up by setting up VPC Peering - we're going to play with TWO VPCs instead of one!

The best part? You still get to revise everything you've learnt from the previous project (but in a new scenario)... you'll see what this means in a minute!

  
  

**Get ready to:**

1.  ☁️ Set up multiple VPCs.
    
2.  🌉 Create a VPC peering connection - i.e. get two VPCs to talk to each other!
    
3.  👩‍🔬 Test VPC peering with connectivity tests.
    

![Today's game plan!](https://learn.nextwork.org/projects/static/aws-networks-peering/architecture-today.png)

  
### ☁️ Step #1

### Set up your VPCs in Minutes

  

Now that we've learnt about the VPC wizard from our previous projects, let's use it to set up TWO VPCs in minutes.

  
  

**In this step, you're going to:**

1.  Create two VPCs from scratch!
    
2.  Use the visual VPC resource map to create your VPCs supa fast 😎⚡️
    

![Step 1: Let's set up two VPCs in minutes.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step1.0.png)

Step 1: Let's set up two VPCs in minutes.

  



-   [Log in to your AWS Account.](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26state%3DhashArgsFromTB_ap-southeast-2_fffdf5be4bb1a27e&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=m-aiqeB2UZeXTGXNyugMP8L64zd_AGUxJl4HLnA-X1o&code_challenge_method=SHA-256)
    
-   Head to your **VPC** console - search for  `VPC`  at the search bar at top of your page.
    
-   From the left hand navigation bar, select **Your VPCs.**
    
-   Select **Create VPC.**
    
-   We previously stuck to creating a VPC only, but this time let's select **VPC and more.**
    

![Step 1: Select VPC and more.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step1.1.1.png)

Step 1: Select VPC and more.

  

**Create VPC 1**

-   Under **Name tag auto-generation**, enter `NextWork-1`
    
-   The VPC's **IPv4 CIDR block** is already pre-filled to `10.0.0.0/16`  - change that to  `10.1.0.0/16`
    

> 💡 **Why are we updating the CIDR block?**  
> Purely to make it easier to remember later! Since we're setting up 3 VPCs, it's easier to remember their CIDR blocks if their ranges match their names 😉
> 
> For example, 10.**1**.0.0/16 for VPC 1, then 10.**2**.0.0/16 for VPC 2, and so on...

-   For **IPv6 CIDR block**, we'll leave in the default option of **No IPv6 CIDR block.**
    
-   For **Tenancy**, we'll keep the selection of **Default.**
    

> 💡 **What does tenancy mean?**  
> Tenancy in AWS refers to the type of hardware your instances run on. Yup, hardware. After all, the EC2 instances you'll launch into your VPC are hosted in a data centre in your chosen Availability Zone!
> 
> You have two options:
> 
> -   **Default:** Your instances share hardware with other AWS customers. This is the standard option and is cost-effective because you’re sharing resources.
>     
> -   **Dedicated:** Your instances run on hardware that's dedicated to you only. For example, imagine a healthcare company that needs to ensure the highest level of security for patient data. They might choose dedicated tenancy to make sure their servers are completely isolated from other customers, helping them meet compliance standards and keep sensitive information secure. Dedicated does come at a higher cost!
>     

-   For **Number of Availability Zones (AZs)**, we'll use just **1** Availability Zone.
    
-   Make sure the **Number of public subnets** chosen is **1**.
    
-   For **Number of private subnets,** we'll keep thing simple today and go with  **0**  private subnets.
    
-   We updated our subnets' CIDR blocks in previous projects, but we don't need defined subnets for this one. Let's  **skip**  the  **Customize subnets CIDR**  for this project.
    

![Step 1: We're moving ahead with just one public subnet!](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step1.1.2.png)

Step 1: We're moving ahead with just one public subnet!

  

-   Next, for the **NAT gateways ($)** option, make sure you've selected **None.** As the dollar sign suggests, NAT gateways cost money!
    

![Step 1: Select None for the NAT gateways option.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step1.3.png)

Step 1: Select None for the NAT gateways option.

  

> 💡 **What are NAT gateways, how are they different from internet gateways?**  
> NAT (Network Address Translation) gateways let instances in **private** subnets access the internet for updates and patches, while blocking inbound traffic.
> 
> For example, a private database in a private subnet might need to download security updates. By using a NAT gateway, the server can access these updates securely while remaining protected from external threats!
> 
> On the other hand, internet gateways let instances in **public** subnets communicate with the internet both ways i.e. both inbound and outbound traffic.

-   Next, for the **VPC endpoints** option, select **None.**
    

> 💡 **What are VPC endpoints?**  
> Normally, to access some AWS services like S3 from your VPC, your traffic would go out to the public internet.
> 
> But, VPC endpoints let you connect your VPC privately to AWS services without using the public internet. This means your data stays within the AWS network, which can improve security and reduce data transfer costs.
> 
> That's your teaser on VPC endpoints, we will get into them in detail in the next project! 👀

-   You can leave the **DNS options** checked.
    

![Step 1: Leave DNS options checked.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step1.4.png)

Step 1: Leave DNS options checked.

  

-   Select **Create VPC.**  
      
    

![Step 1: Your VPC gets set up super fast!](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step1.5.png)

Step 1: Your VPC gets set up super fast!

  

-   Select **View VPC**.
    
-   Select the **Resource map** tab - nice, all of these resources have been set up for you in a flash!
    

  
  

**Set up VPC 2**

We're going to set up another VPC with  _slightly_  different settings - pay close attention!

-   Select **Create VPC.**
    
-   Select **VPC and more.**
    
-   Under **Name tag auto-generation**, enter `NextWork-2`
    
-   The VPC's **IPv4 CIDR block** should be unique! Make sure the CIDR block is NOT `10.1.0.0/16`  - it should be  `10.2.0.0/16`
    

> 💡 **Why do they need to be unique?**  
> Each VPC must have a unique IPv4 CIDR block so the IP addresses of their resources don't overlap. Having overlapping IP addresses could cause routing conflicts and connectivity issues!

![Step 1: Use a new name tag and CIDR block.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step1.2.png)

Step 1: Use a new name tag and CIDR block.

  

-   For **IPv6 CIDR block**, we'll leave in the default option of **No IPv6 CIDR block.**
    
-   For **Tenancy**, we'll keep the selection of **Default.**
    
-   For **Number of Availability Zones (AZs)**, we'll use just **1** Availability Zone.
    
-   Make sure the **Number of public subnets** chosen is **1**.
    
-   For **Number of private subnets,** we'll go with  **0**  for today's project. Let's keep it simple with just a single subnet!
    
-   For the **NAT gateways ($)** option, select **None.**
    
-   For the **VPC endpoints** option, select **None.**
    
-   You can leave the **DNS options** checked.
    
-   Select **Create VPC.**
    



### 🌉 Step #2

### Create a Peering Connection

  

Wooo now that you have two VPCs ready to go, let's bridge them together with a peering connection.

  
  

**In this step, you're going to:**

1.  Set up a connection link between your VPCs.
    

![Step 2: Let's set up a peering connection.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step2.0.png)

Step 2: Let's set up a peering connection.

  



-   Still in the VPC console, click on **Peering connections**  on the left hand navigation panel.
    

> 💡 **What is a peering connection?**  
> A VPC peering connection is a direct connection between two VPCs.
> 
> A peering connection lets VPCs and their resources route traffic between them using their  **private**  IP addresses. This means data can now be transferred between VPCs without going through the public internet.
> 
> Without a peering connection, data transfers between VPCs would use resources' public address - meaning VPCs have to communicate over the public internet.
> 
> ![](https://learn.nextwork.org/projects/static/aws-networks-peering/without-peering.png)
> 
>   

![Step 2: Select Peering connections.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step2.1.png)

Step 2: Select Peering connections.

  

-   Click on **Create peering connection** in the right hand corner.
    

![Step 2: Select Create peering connection.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step2.2.png)

Step 2: Select Create peering connection.

  

-   Name your  **Peering connection name**  as `VPC 1 <> VPC 2`
    
-   Select **NextWork-1-VPC**  for your  **VPC ID (Requester).**
    

> 💡 **What does Requester mean?**  
> In VPC peering, the  **Requester**  is the VPC that initiates a peering connection. As the requester, they will be sending the other VPC an  **invitation**  to connect!

![Step 2: Set the Requester.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step2.3.png)

Step 2: Set the Requester.

  

-   Under **Select another VPC to peer with,** make sure  **My Account** is selected.
    

> 💡 **Wow, I can peer with other Accounts?**  
> Yup, VPC peering can occur between VPCs in different AWS accounts!
> 
> This flexibility lets businesses collaborate securely by sharing resources across accounts without exposing them to the public internet.
> 
> You can also try this option in a project by peering with a friend or setting up a separate AWS account!

-   For **Region,** select  **This Region.**
    
-   For **VPC ID (Accepter)**, select **NextWork-2-VPC**
    

> 💡 **What does Accepter mean?**  
> In VPC peering, the  **Accepter**  is the VPC that receives a peering connection request! The Accepter can either accept or decline the invitation. This means the peering connection isn't actually made until the other VPC also agrees to it!

![Step 2: Set the Accepter.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step2.4.png)

Step 2: Set the Accepter.

  


-   Click on **Create peering connection.**
    
-   Your newly created peering connection isn't finished yet! The green success bar says the peering connection  **has been requested.**
    

![Step 2: A peering connection is requested.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step2.5.png)

Step 2: A peering connection is requested.

  

-   On the next screen, select **Actions** and then select **Accept request...**  Get ready to take a screenshot!
    



> 💡 **Why did I have to accept a request?**  
> You set up the VPC peering connection as VPC 1 (the Requestor), but don't forget that the Accepter needs to approve of it too!
> 
> By clicking  **Accept request,**  you were accepting the connection as VPC 2.

![Step 2: Select Accept request here.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step2.6.png)

Step 2: Select Accept request here.

  

-   Click on  **Accept request**  again on the pop up panel.
    
-   Click on **Modify my route tables now** on the top right corner.
    

![Step 2: Select Modify my route tables now.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step2.7.png)

Step 2: Select Modify my route tables now.

  

### 🚏 Step #3

### Update Route Tables

  

With a peering connection all set up ✅, now it's time for traffic in your VPCs to learn how to use it.

  
  

**In this step, you're going to:**

1.  Set up a way for traffic coming from VPC 1 to get to VPC 2.
    
2.  Set up a way for traffic coming from VPC 2 to get to VPC 1.
    



**Update VPC 1's route table**

-   Select the checkbox next to VPC 1's route table i.e. called  **NextWork-1-rtb-public.**
    
-   Scroll down and click on the **Routes** tab.
    
-   Click **Edit routes.**
    
-   Let's add a new route!
    

> 💡 **Why do I need to add a new route?**  
> Even if your peering connection has been accepted, traffic in VPC 1 won't know how to get to resources in VPC 2 without a route in your route table! You need to set up a route that directs traffic bound for VPC 2 to the peering connection you've set up.

-   Add a new route to  **VPC 2**  by entering the CIDR block `10.1.0.0/16` as our  **Destination**.
    
-   Under Target, select  **Peering Connection.**
    
-   Select  **VPC 1 <> VPC 2**.
    

![Step 3: Select your peering connection.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step3.1.png)

Step 3: Select your peering connection.

  

-   Click **Save changes.**
    
-   Oops! We've hit an error.
    

![Step 3: Oops! We've hit an error.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step3.2.png)

Step 3: Oops! We've hit an error.

  

> 💡 **What does this error message mean?**  
> The message says the destination you've put in has the same CIDR block as VPC 1's own CIDR block!
> 
> Whoops that was a typo - VPC 2's CIDR block is actually 10.**2**.0.0/16.
> 
> This is a key learning to take away: route tables cannot differentiate between local and remote destinations if they share the same CIDR block.
> 
> Imagine if we didn't set up VPC 2 with its own unique CIDR block in the previous step! We'd get into trouble here.

-   Let's fix that typo now! Select  **Back.**
    
-   Update your new route's  **Destination**  to `10.2.0.0/16`
    
-   Click  **Save changes**  again.
    
-   Confirm that the new route appears in VPC 1's **Routes** tab now!
    

![Step 3: Do you see a new route in VPC 1's route table?](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step3.3.png)

Step 3: Do you see a new route in VPC 1's route table?

  

**Update VPC 2's route table**

Challenge yourself - do you think you can set up the equivalent route in VPC 2's route table?

If you get stuck, use the same instructions above but make sure:

1.  The route table you're updating is  **NextWork-2-rtb-public.**
    
2.  The  **Destination**  is the CIDR block `10.1.0.0/16`
    

![Step 3: Update VPC 2's route table too.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step3.4.png)

Step 3: Update VPC 2's route table too.

  



### 💻 Step #4

### Launch EC2 Instances

  

Wooohooo, now it's time to launch EC2 instances into your architecture!

  
  

**In this step, you're going to:**

1.  Launch an EC2 instance in each VPC, so we can use them to test your VPC peering connection later.
    

![Step 4: EC2 instances have joined the party 🥳](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step4.0.png)

Step 4: EC2 instances have joined the party 🥳

  


**Launch an instance in VPC 1**

-   Head to the **EC2 console** - search for `EC2` in the search bar at the top of screen.
    
-   Select **Instances** at the left hand navigation bar.
    
-   Select **Launch instances**.
    
-   Since your first EC2 instance will be launched in your first VPC, let's name it `Instance - NextWork VPC 1`
    
-   For the **Amazon Machine Image,** select **Amazon Linux 2023 AMI.**
    
-   For the **Instance type,** select **t2.micro.**
    
-   For the **Key pair (login)** panel, select **Proceed without a key pair (not recommended).**
    

![Step 4: We shall proceed without a key pair.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step4.1.png)

Step 4: We shall proceed without a key pair.

  

> 💡 **Why aren't we setting up a key pair? Wasn't this step important in the last few projects?**  
> In previous projects, setting up a key pair was a key step for learning how SSH and directly accessing an EC2 instance works.
> 
> However, we've also learnt that with  **EC2 Instance Connect,**  AWS actually manages a key pair for us! We don't need to manage key pairs ourselves. Since we've already learnt how to set up key pairs twice in the last two projects, we don't need to do it again this time.

-   At the **Network settings** panel, select **Edit** at the right hand corner.
    

> 💡 **Why are we editing the Network settings?**  
> By default, all resources are launched into the default VPC that AWS has set up for your account. We need to tell AWS that we actually want to launch this instance in **NextWork-vpc-1!**

-   Under  **VPC**, select **NextWork-vpc-1**.
    
-   Under  **Subnet,**  select your VPC's public subnet.
    
-   Keep the **Auto-assign public IP** setting to  **Disable.**
    
-   For the **Firewall (security groups)** setting, Amazon VPC already created a security group for your VPC - let's use that!
    
-   Choose **Select existing security group.**
    
-   Select the  **default**  security group for your VPC.
    

![Step 4: Set up your EC2 instance's networking settings.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step4.2.png)

Step 4: Set up your EC2 instance's networking settings.

  

-   Select **Launch instance.**
    

  
  

**Launch an instance in VPC 2**

You know the drill - do you think you can set up an EC2 instance in VPC 2?

If you get stuck, use the same instructions above but make sure:

1.  The  **Name**  is `Instance - NextWork VPC 2`
    
2.  The  **VPC**  is **NextWork-vpc-2**.
    

![Step 4: You should see two EC2 instances once you're done.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step4.3.png)

Step 4: You should see two EC2 instances once you're done.

  



### 🐈 Step #5

### Connect to Instance 1

  

To test our VPC peering connection, we'll need to get one of our EC2 instances to try talk to the other.

  
  

**In this step, you're going to:**

1.  Use EC2 Instance Connect to connect to your first EC2 instance.
    
2.  Fix a connection error!
    

![Step 5: Do you still remember how to connect to an EC2 instance?](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step5.0.png)

Step 5: Do you still remember how to connect to an EC2 instance?

  


-   Still in your **EC2** console, select the checkbox next to  **Instance - NextWork VPC 1.**
    
-   Select **Connect**.
    

![Step 5: Oopsies! A new error shows up.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step5.1.png)

Step 5: Oopsies! A new error shows up.

  

> 💡 **Woah! An error - why can't I use EC2 Instance Connect?**  
> Check out the error message: "No public IPv4 address assigned. With no public IPv4 address, you can't use EC2 Instance Connect."
> 
> Can you tell which part of our EC2 instance set up caused this error?
> 
> Yup, keeping  **Disable**  for the  **Auto-assign IP address**  option in our EC2 instance's network settings caused this error!  
> 
> ![Step 5: We didn't assign a public IP address in the previous step 🙉](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step5.banner1.png)
> 
> Step 5: We didn't assign a public IP address in the previous step 🙉
> 
> That's a key learning to take away: If you want to connect to your instance over EC2 Instance Connect, then your instance must have a public IP address and be in a public subnet. This is because using EC2 Instance Connect connects to your server  **over the internet**  by default.
> 
> ![Step 5: EC2 Instance Connect works over the public internet.](https://learn.nextwork.org/projects/static/aws-networks-peering/ec2-instance-connect.png)
> 
> Step 5: EC2 Instance Connect works over the public internet.
> 
>   



-   Verify this by heading back to the  **Instances**  page in your EC2 console, and checking the Public IPv4 address field... it's empty!
    

![Step 5: No IPv4 address to be found 👀](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step5.2.png)

Step 5: No IPv4 address to be found 👀

  

-   On your EC2 console's left hand navigation panel, select  **Elastic IPs.**
    

![Step 5: Select Elastic IPs.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step5.3.png)

Step 5: Select Elastic IPs.

  

> 💡 **What are Elastic IPs?**  
> Elastic IPs are  **static**  IPv4 addresses that get allocated to your AWS account, and is yours to delegate to an EC2 instance.
> 
> An Elastic IP being  **static**  is a key word here! EC2 instances by default have  **dynamic**  IPs, which means their Public IPv4 addresses change every time they're restarted. Having an Elastic IP is like having a permanent address in a city, instead of having to move from location to location every time your instance restarts.
> 
>   
> 💡 **Why would someone use Elastic IPs?**  
> Elastic IPs are very popular tools for making sure an application stays available on the internet. Usually, an IP address change means a website's DNS record (i.e. the map that directs users visiting their domain to the right application/server) needs to be updated.
> 
> DNS updates take time to propogate across the internet - it can take hours and even days! So without an Elastic IP, a website would be down for its users if an EC2 instance restarts and the engineers have to change a DNS record. With an Elastic IP, the IP address associated with the EC2 instance is always constant - no DNS updates needed!
> 
>   
> 💡 **Why am I using an Elastic IP?**  
> Elastic IPs are also a great way to assign an instance a public IPv4 address after launching it! That's how we're using it in this step.

-   Select  **Allocate Elastic IP**  addresses.
    

![Step 5: Select Allocate Elastic IPs.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step5.4.png)

Step 5: Select Allocate Elastic IPs.

  

-   Leave all default options.
    



> 💡 **Woah, what does the Public IPv4 address pool setting do?**  
> 
> ![Step 5: The IPv4 address pool setting.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step5.banner2.png)
> 
> Step 5: The IPv4 address pool setting.
> 
> This setting is asking you to choose the  **source**  of the Elastic IP address. Since IPv4 addresses are unique on the internet, the IPv4 address you are allocated has to come from somewhere and can't overlap with other existing IPv4 addresses!
> 
> The default setting is  **Amazon's pool of IPv4 addresses**. Think of this as a public pool of all IPv4 addresses that Amazon has saved to allocate to AWS accounts, so you won't need to find one yourself.
> 
> If you have your own pool of IP addresses, you can also set those up in your AWS account and allocate an IPv4 address from there instead (this is called Bring Your Own IP, or BYOIP).

-   Select  **Allocate.**
    
-   Refresh your page, then select the new IP address you've set up.
    
-   Select the  **Actions**  dropdown, then select  **Associate Elastic IP address.**
    
-   Under  **Instance**, select  **Instance - NextWork VPC 1.**
    

![Step 5: Select your first instance.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step5.6.png)

Step 5: Select your first instance.

  

-   Click  **Associate**.
    

> 💡  **What about the Private IP address field? What does that do?**  
> 
> ![Step 5: The Private IP address field.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step5.banner3.png)
> 
> Step 5: The Private IP address field.
> 
> This setting isn't quite relevant to us since your EC2 Instance only has one private IP address, but it becomes very important if an EC2 instance has  **multiple**  private IPs.
> 
>   
> 💡  **An EC2 instance can have multiple private IPs?**  
> Absolutely! A single EC2 instance can have multiple private IP addresses.
> 
> This setup is just like how your personal computer can have different user accounts, each with its own settings and applications.
> 
> Here, having different IP addresses means the same server can have different network identities to host multiple applications at the same time! It’s an awesome way to maximize the use of a single EC2 instance while keeping applications separated with their own security and networking rules.

-   Awesome! Your EC2 Instance should have a public IP address now.
    
-   To check this, select  **Instances**  from the left hand navigation panel.
    
-   Select the checkbox next to  **Instance - NextWork VPC 1.**
    
-   Do you see a  **Public IPv4 address**  for your EC2 instance now?
    

![Step 5: Niceeeeee - your EC2 instance has a public IPv4 address now!](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step5.7.png)

Step 5: Niceeeeee - your EC2 instance has a public IPv4 address now!

  

Woohoo! Good to see that the Elastic IP address we've set up is now associated with our EC2 instance.



### 🐅 Step #6

### Connect to Instance 1 (round two!)

  

Phew looks like the IP address should be all resolved now... let's try connecting to your EC2 instance again!

  
  

**In this step, you're going to:**

1.  Use EC2 Instance Connect to connect to Instance 1 (one more time)!
    
2.  Fix (another) error.
    


-   Select **Connect.**
    
-   In the EC2 Instance Connect set up page, select  **Connect**  again.
    
-   Oh no! We've failed to connect to our instance?!
    

![Step 6: We failed to connect to our instance... 😭](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step6.1.png)

Step 6: We failed to connect to our instance... 😭

  

Do you remember the reason for this from your previous project? The troubleshooting steps are the same as last time!

You can challenge yourself to troubleshoot this on your own this time, orrrr read ahead for the instructions. 👇

-   Head back to your **VPC console.**
    
-   Select **Subnets** from the left hand navigation panel.
    
-   Select the checkbox next to **NextWork-1-subnet-public1...**
    
-   Hmm let's take a look! Investigate the **Route table** and **Network ACL** tabs - what do you see?
    

![Step 6: Check Instance 1's route table.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step6.2.png)

Step 6: Check Instance 1's route table.

  

![Step 6: Check Instance 1's network ACL.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step6.3.png)

Step 6: Check Instance 1's network ACL.

  

> 💡 Everything looks good! Our Network ACL allows all traffic in and out, and our route table is correctly setting up a route to the Internet Gateway.

-   Hmmm that leaves one more thing to investigate...
    
-   Copy the  **VPC ID**  of  **NextWork-1-vpc.**
    

![Step 6: Copy VPC 1's ID.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step6.4.png)

Step 6: Copy VPC 1's ID.

  

-   Head into the **Security groups** page from the left hand navigation panel.
    
-   Woah it's a bunch of nameless security groups!
    
-   To find the VPC 1's default security group, let's use the handy search bar.
    
-   Click into the search bar, and paste the ID you copied into the search bar. Make sure there aren't any empty spaces before your text.
    
-   Select the filter!
    

![Step 6: Paste VPC 1's ID into the search bar.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step6.5.png)

Step 6: Paste VPC 1's ID into the search bar.

  

-   Nice, that narrowed it nicely for us. Select the checkbox next to VPC 1's  **default**  security group.
    
-   Select the **Inbound rules** tab.
    

![Step 6: Check out VPC 1's security group's inbound rules.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step6.6.png)

Step 6: Check out VPC 1's security group's inbound rules.

  

-   Aha! Mystery solved.
    

> 💡 **Mystery solved?! How are our inbound rules the cause of our connectivity issue?**  
> The answer lies in the  **Source**  of your security group's inbound rules.
> 
> We're trying to access Instance - NextWork VPC 1 using SSH through EC2 Instance Connect, which is trying to connect to your instance over the internet.
> 
> Your default security group only allows inbound traffic from within the VPC, so traffic from the internet is being cut off!
> 
> **That's a key learning to take away:**  The default security group for a new VPC does not allow incoming traffic from outside of the VPC.
> 
> You have to allow inbound SSH traffic on port 22 yourself!

-   In the **Inbound rules** tab, select **Edit inbound rules.**
    
-   Select **Add rule.**
    
-   For your new rule, configure the **Type** as **SSH.**
    
-   Then, under **Source type**, select **Anywhere-IPv4.**
    
-   Select **Save rules.**
    

![Step 6: Your updated security group inbound rules.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step6.7.png)

Step 6: Your updated security group inbound rules.

  

-   With that modified, refresh your EC2 console's **Instances** page.
    
-   Select your **Instance-NextWork VPC 1** and select **Connect** again.
    
-   Select  **Connect**  in the EC2 Instance Connect setup page.
    
-   Phew! Success.
    

![Step 6: Phew! All connected now 😮‍💨](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step6.8.png)

Step 6: Phew! All connected now 😮‍💨

  

### 🧪 Step #7

### Test VPC Peering

  

Awesome, we've figured out how to connect with VPC 1's Instance!

Let's see if we can connect with VPC 2's instance from here.

**In this step, you're going to:**

1.  Get Instance 1 to send test messages to Instance 2.
    
2.  Solve connection errors until Instance 2 is able to send messages back.
    

![Step 7: Time to put your peering connection to the TEST.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step7.0.png)

Step 7: Time to put your peering connection to the TEST.

  



-   Leave open the **EC2 Instance Connect** tab, but head back to your **EC2** console in a new tab.
    
-   Select **Instance - NextWork VPC 2.**
    
-   Copy Instance - NextWork VPC 2's **Private IPv4 address.**
    

![Step 7: Copy the private IPv4 address.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step7.1.png)

Step 7: Copy the private IPv4 address.

  

-   Switch back to the **EC2 Instance Connect** tab.
    
-   Run `ping [the Private IPv4 address you just copied]` in the terminal.
    
    -   Your final result should look similar to something like `ping 10.0.1.227`
        
    -   Don't know where to enter this prompt? Look for the `$` sign at the bottom line of the black window, and type in your command after the $ sign.
        

> 💡 **What does ping mean?**  
> **Ping** is a common computer network tool used to check whether your computer can communicate with another computer or device on a network.
> 
> Think of it like sending a tiny message that says "hello, are you there?" to another computer, or like checking if someone's home by ringing their doorbell.
> 
> When you "ping" a specific IP address, your server (in this case, Instance - NextWork VPC 1) sends a small packet of data to the target server (Instance - NextWork VPC 2), asking for a response. Ping will tell you whether you get a response back and how long it took to get a response.
> 
> If you receive a response quickly, it means the connection between your computer and the other computer is good. If it takes a long time or you get no response, there might be a problem with the connection!

-   You should see a response similar to this:
    

![Step 7: Your first ping response.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step7.2.png)

Step 7: Your first ping response.

  

> 💡 **What does this response mean? Is it a good response?**  
> This single line indicates that your Instance - NextWork VPC 1 has sent out a ping message... and that's about it.
> 
> Usually, when you ping another computer successfully, you should see **several** replies back instantly. Each reply tells you how long it took for the message to go to the Instance - NextWork VPC 2 and come back.
> 
> If you don't get any replies (that's our situation right now), or if the replies stop suddenly, it's usually a sign that there's a problem with the connection.
> 
> ![](https://learn.nextwork.org/projects/static/aws-networks-peering/ping1.png)
> 
>   
> 
> 💡 **Why is there a problem with the connection between my servers?**  
> One common reason for these issues is that the target server (Instance - NextWork VPC 2) or its network might be blocking the type of messages used in ping, which are known as **ICMP (Internet Control Message Protocol) traffic.**
> 
> Blocking ICMP traffic is often done to prevent network attacks, like attackers can overwhelming a server with ping messages so it can't respond to real users wanting to use your application. Fair enough that ICMP traffic is blocked by default!

-   To resolve this connectivity error, let's investigate whether  **Instance - NextWork VPC 2**  is allowing inbound ICMP traffic.
    

  
  

_🧠 Hint: you've done the exact same troubleshooting in the previous project!_

Challenge yourself - can you solve this now without any guidance? Orrrr if you'd prefer, let's do this step by step together with the instructions below.

> ⏸️ **Pause and have a think - where do you think you can investigate this?**  
> Up til now, you've learnt about internet gateways, subnets, route tables, IPv4 addressing, security groups and route tables...
> 
> Which of these would you need to configure for Instance - NextWork VPC 2 to receive ICMP traffic?
> 
> Hmmm!  
> 🤔  
> 🤔  
> 🤔

▶️ Alright, resuming now!

-   Leave open the **EC2 Instance Connect** tab, but head back to your **VPC** console in a new tab.
    
-   In the VPC console, select the **Subnets** page.
    
-   Select VPC 2's subnet i.e.  **NextWork-2-subnet-public1-...**
    
-   Let's investigate the **Route tables** and **Network ACL** tabs for your public subnet.
    
-   The network ACL allows all types of inbound traffic from anywhere! So this looks perfectly fine.
    
-   Before we finish, let's check the security groups!
    
-   Copy the  **VPC ID**  of VPC 2.
    

![Step 7: Copy VPC 2's ID.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step7.3.png)

Step 7: Copy VPC 2's ID.

  

-   Select **Security groups** from the left hand navigation panel.
    
-   Paste the  **VPC ID**  in the search bar, and select the suggested filter.
    
-   Check your security group's **Inbound rules** tab - does this security group allow ICMP traffic from sources outside of VPC 2? (Nope!)
    
-   Aha! Mystery solved.
    

  
  

Let's fix this by letting inbound ICMP traffic from VPC 1.

-   Select **Edit inbound rules.**
    
-   Select **Add new rule.**
    
-   Change the **Type** to **All ICMP - IPv4**.
    

> 💡 **What is ICMP - IPv4?**  
> When you set a rule for **All ICMP - IPv4**, you're allowing  **all**  types of ICMP messages for IPv4 addresses. This covers a wide range of operational messages that are essential for diagnosing network connectivity issues, ping requests and responses are just one type of ICMP messages.
> 
> You might notice that ICMP is not limited to IPv4; there is also ICMP for IPv6 , which functions similarly but is tailored specifically for IPv6 networks.

-   Set the **Source** to traffic coming from VPC 1 - `10.1.0.0/16`
    
-   Select **Save rules.**
    

  
  

All updated!

![Step 7: Your updated security group inbound rules.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step7.4.png)

Step 7: Your updated security group inbound rules.

  

-   Revisit the **EC2 Instance Connect** tab that's connected to Instance - NextWork VPC 1.
    
-   Woah! Lots of new lines coming through in the terminal.
    

![Step 7: YAY ping replies are coming through now!](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step7.5.png)

Step 7: YAY ping replies are coming through now!

  

> 💡 **What do these new lines mean?**  
> The multiple new lines appearing in your terminal are a sign of successful communication between the two EC2 instances - wohoooo!
> 
> Each line represents a reply from the ping command you sent. This means that the ICMP (Internet Control Message Protocol) traffic is now successfully reaching Instance - NextWork VPC 2, thanks to the adjustments you made in the network ACLs and Security Groups. Nice!
> 
> ![](https://learn.nextwork.org/projects/static/aws-networks-peering/ping2.png)
> 
>   
> 
> **Extra for Experts:** Curious about what each part of the ping message means? The output typically shows several pieces of information:
> 
> -   **Time:** Each line includes the time in milliseconds it took for the ping message to travel from your server to the target and back. This is a measure of the latency or delay in the network communication.
>     
> -   **TTL (Time to Live):** This value indicates the lifespan of the packet as it travels; it decreases by one for each router it passes through. Once TTL reaches zero, the data packet containing the ping message is automatically dropped from the network.
>     
> -   **Sequence number:** This helps in identifying each ping request and matching it to its corresponding reply, ensuring that the responses correspond to the specific requests sent.
>     

**Congratulations!** You've set up a peering architecture that connects VPC 1 to VPC 2 AND validated it with ping - too cool 😎☁️🌉



😮‍💨 All Done

### Nice work!

  

You've just completed today's project and  **set up a successful peering connection between TWO VPCs.**

🗑️ Before You Go



### Delete Your Resources

✋  **STOP**

Before diving into the steps for deleting your resources, why not challenge yourself to delete everything in this project on your own?

Keeping track of your resources, and deleting them at the end, is absolutely a skill that will help you reduce waste in your account.

  
  

🛑  **STEPS BELOW:**

  
  
  

**Delete your EC2 Instances**

-   Head back to the  **Instances**  page of your EC2 console.
    
-   Select the checkboxes next to  **Instance - NextWork VPC 1**  and  **Instance - NextWork VPC 2.**
    
-   Select  **Instance state,**  then select  **Terminate Instance.**
    
-   Select  **Terminate**.
    

![Step 9: Delete your EC2 instances.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step9.1.png)

Step 9: Delete your EC2 instances.

  

  
  
  

**Delete your Elastic IP address**

-   Select  **Elastic IPs**  from the left hand navigation panel.
    
-   Select the IP address you've created.
    
-   Select Actions, then  **Release Elastic IP addresses.**
    

> **💡 What does it mean to release an Elastic IP address?**  
> When you release an Elastic IP address, that address returns to Amazon's pool of IPv4 address and will eventually get reallocated to another AWS user!

![Step 9: Delete your Elastic IP address.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step9.2.png)

Step 9: Delete your Elastic IP address.

  

-   Select  **Release.**
    

  
  
  

**Delete VPC Peering Connections**

-   Head back to your  **VPC**  console.
    
-   Select  **Peering connections**  from your left hand navigation panel.
    
-   Select the `VPC 1 <> VPC 2` peering connection.
    
-   Select  **Actions**, then **Delete peering connection.**
    

![Step 9: Delete your VPC peering connection.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step9.3.png)

Step 9: Delete your VPC peering connection.

  

-   Select the checkbox to **Delete related route table entries**.
    
-   Type `delete` in the text box and click **Delete.**
    

  
  
  

**Delete your VPCs**

-   Select  **Your VPCs**  from your left hand navigation panel.
    
-   Select  **NextWork-1-vpc,**  then  **Actions**, and  **Delete VPC.**
    

![Step 9: Delete your VPC.](https://learn.nextwork.org/projects/static/aws-networks-peering/high-step9.4.png)

Step 9: Delete your VPC.

  

-   Type `delete` in the text box and click **Delete.**
    
-   Note: if you get stopped from deleting your VPC because  **network interfaces**  are still attached to your VPC - delete all the attached network interfaces first!
    

> 💡  **What is a network interface?**  
> Network interfaces get created automatically when you launch an EC2 instance. Think of them as a component that attaches to an EC2 instance on one end and your VPC on another - so that your EC2 instance is connected to your network and can send and receive data! Network interfaces are usually deleted automatically with your EC2 instance, but on some occassions it'd be faster to delete them manually.

-   Select  **NextWork-2-vpc,**  then  **Actions**, and  **Delete VPC.**
    
-   Type `delete` in the text box and click **Delete.**
    

  
  
  

Other network components should be automatically deleted with your VPC, but it's always a good idea to check anyway:

1.  Subnets
    
2.  Route tables
    
3.  Internet gateways
    
4.  Network ACLs
    
5.  Security groups
    

Don't forget to  **refresh**  each page before checking if the resources are still in your account!


Nice Work!

THAT'S NETWORKING PROJECT SIX...

DONE!!!!! 🥳

**Today you've learnt how to:**

-   🌉 **Create a VPC peering connection:** You established a VPC peering connection setween two VPCs, enabling secure and direct communication while bypassing the public internet. This connection ensures private and efficient data transfer between the VPCs.  
      
    
-   🚏 **Update route tables for optimized traffic flow:** You updated the route tables within your VPCs to route traffic through your peering connection.  
      
    
-   💻 **Launch and test EC2 instances in peered VPCs:** You launched EC2 instances within each of your peered VPCs, and connectivity was tested to confirm that everything is functioning as expected.

### 👏 All done!

Content Credits - **Nextwork**