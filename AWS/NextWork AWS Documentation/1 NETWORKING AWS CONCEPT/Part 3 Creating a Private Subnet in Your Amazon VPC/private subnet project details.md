
☁️ Step 1: Set up your VPC basics

🚷 Step #2: Set up a private subnet

🚧 Step #3: Set up a private route table

🚔 Step #4: Set up a private network ACL

🗑️ Before You Go: Delete Your Resources

# Creating a Private Subnet

Let's set up a private section in your VPC!


WHAT YOU'LL NEED

-   An AWS account -  [Create one here!](https://github.com/dineshrajdhanapathyDD/Cloud/blob/main/AWS/NextWork%20AWS%20Documentation/5%20AWS%20BASIC/legendary-aws-account-setup.pdf))

-   Part 1 of this series -  [Build a Virtual Private Cloud](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%201%20Build%20a%20Virtual%20Private%20Cloud)
-   Part 2 of this series -  [VPC Traffic Flow and Security](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%202%20VPC%20Traffic%20Flow%20and%20Security)

### AWS SERVICES

-   [Amazon VPC](https://www.youtube.com/watch?v=Pazb3rS_Ers)

## ⚡️ 30 second Summary

Welcome to your third AWS networking project!

**In your first two networking projects, you've created:**

1.  ☁️ An Amazon VPC (amazing!)
    
2.  🥅 A public subnet (woohoo!)
    
3.  🚪 An internet gateway (go you!)
    
4.  🚏 A route table (so good!)
    
5.  👮‍♀️ A security group (say whaaat!)
    
6.  📋 A Network ACL, aka Network Access Control List (super cool!)
    

  
  

If you haven't done the previous project in our networking series,  [VPC Traffic Flow and Security](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%202%20VPC%20Traffic%20Flow%20and%20Security), we'd highly recommend doing that first. This project starts right where the previous one leaves off.

![What you've learnt from parts 1 and 2 of this networking series!](https://learn.nextwork.org/projects/static/aws-networks-private/architecture-past.png)

What you've learnt from parts 1 and 2 of this networking series!

  

In  **Creating a Private Subnet**, we're going to level up by creating a  **private subnet**  in your VPC - you'll learn all about this in a minute!

  
  

**Get ready to:**

1.  🚷 Create a private subnet.
    
2.  🚧 Create a private route table.
    
3.  🚔 Create a private network ACL.
    

![Today's game plan.](https://learn.nextwork.org/projects/static/aws-networks-private/architecture.png)



  
  





### Your Step-By-Step Project

We'll guide you through this project step-by-step.

Let's go!

> 📣  **Delete all your resources**  by the end of the day, even if you don't finish the entire project.  
>   





☁️ Step 1

### Set up your VPC basics

  

We're repeating our steps from the first two networking projects to set up our VPC, subnet, internet gateway, route table, security group  _and_  network ACLs.

What a list, you're going to crush it!

![Let's set this up to get started.](https://learn.nextwork.org/projects/static/aws-networks-private/architecture-past.png)

Let's set this up to get started.

  

**Create a VPC:**

Off we go! Your VPC is the foundation of this project and represents your corner of the AWS Cloud.

![Let's create a VPC.](https://learn.nextwork.org/projects/static/12/high-step1.1.png)

Let's create a VPC.

  

-   [Log in to your AWS Account.](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26state%3DhashArgsFromTB_ap-southeast-2_fffdf5be4bb1a27e&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=m-aiqeB2UZeXTGXNyugMP8L64zd_AGUxJl4HLnA-X1o&code_challenge_method=SHA-256)
    
-   In your  **AWS Management Console's**  search bar, search for  `VPC`.
    
-   Select  **VPC**  from the drop down menu.
    
-   In the left navigation pane, choose  **Your VPCs**.
    
-   Make sure you're on the Region that's closest to you. Use the dropdown on the top right hand corner to switch Regions.
    
-   Choose  **Create VPC**.
    
-   Choose  **VPC Only**.
    
-   Name tag:  `NextWork VPC`
    
-   IPv4 CIDR:  `10.0.0.0/16`
    

> **💡 What is a CIDR block?**  
> CIDR is a way to assign a whole block of IP addresses, kind of like creating a zone/area in a city.  
>   
> To understand how big a CIDR block is, look at the number after the slash - the smaller the number, the larger the CIDR block!
> 
> ![Step 1: A summary of how CIDR blocks work.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.2.png)
> 
> Step 1: A summary of how CIDR blocks work.
> 
> `10.0.0.0/16`  means the first 16 bits of your IP address (`10.0`) are fixed, but the remaining 16 bits (i.e. the second half of the IP address) can be allocated however you like. This CIDR block ranges from  `10.0.0.0`  to  `10.0.255.255`! There are 2^16 (65,536) possible IP addresses within this subnet.  
>   
> A smaller CIDR block like  `10.0.0.0/24`  has the first 24 bits fixed, meaning only the last 8 bits can vary. This provides 2^8 (256) possible addresses.  
>   
> A larger CIDR block like  `10.0.0.0/8`  has only the first 8 bits fixed, allowing for a much larger number of varying bits - this gives you 2^24 (16,777,216) possible addresses.

-   Select  **Create VPC**.
    

  
  

**Create Subnets:**

Nice! We've created our VPC, so it's time for the next step...creating a public subnet. Subnets are subdivisions within your VPC where you can launch AWS resources, think of them as suburbs/neighbourhoods within your city.

![Step 1: Let's create a subnet.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.3.png)

Step 1: Let's create a subnet.

  

-   In the  **VPC Dashboard**, under  **Virtual Private Cloud**, choose  **Subnets**.
    
-   Choose  **Create subnet**.
    
-   Configure your subnet settings:
    
    -   VPC ID:  `NextWork VPC`
        
    -   Subnet name:  `Public 1`
        
    -   Availability Zone:  **Select the first Availability Zone in the list.**
        
    -   IPv4 VPC CIDR block:  `10.0.0.0/16`
        
    -   IPv4 subnet CIDR block:  `10.0.0.0/24`
        

> 💡  **Is my subnet a public subnet now?**  
> Even though your subnet is labeled **Public 1**, it isn't a public subnet yet. A public subnet must have a route to an  **internet gateway**, which you'll attach in a minute.

-   Choose **Create subnet.**
    

![Step 1: How IP addresses work across your VPC, subnet and resources.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.4.png)

Step 1: How IP addresses work across your VPC, subnet and resources.

  

-   Select the checkbox next to **Public 1**.
    
-   In the **Actions** menu, select **Edit subnet settings.**
    
-   Check the box next to **Enable auto-assign public IPv4 address.**
    

> **💡 What does it mean to enable auto-assign public IPv4 address?**  
> When you enable auto-assign public IPv4 address for a subnet, any  **EC2 instance**  launched in that subnet will automatically receive a public IP address. This makes the instance accessible from the internet without needing to manually assign a public IP - a huge time saver!

-   Choose **Save.**
    

  
  

**Create an internet gateway:**

Time to connect our VPC to the internet! Let's create an internet gateway.

![Step 1: Let's create an internet gateway.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.5.png)

Step 1: Let's create an internet gateway.

  

-   In the left navigation pane, choose **Internet gateways**.
    
-   Choose  **Create internet gateway**.
    
-   Configure your internet gateway settings:
    
    -   **Name tag:**  `NextWork IG`
        
-   Choose  **Create internet gateway**.
    
-   Select your newly created internet gateway and choose  **Actions**, then  **Attach to VPC**.
    
-   Select  **NextWork VPC**.
    
-   Select  **Attach internet gateway**.
    

> 💡  **What does attaching an internet gateway to a VPC mean?**  
> Attaching an internet gateway means resources in your VPC can now access the internet. The EC2 instances with public IP addresses also become accessible to users, so any application you host on those instances become public too.

  
  

**Create a route table**

Even though you've created an internet gateway and attached it to your VPC, you still have to tell the resource in your public subnet how to get to the internet.

You'll have to set up  **route tables**  to direct traffic from your resource to your internet gateway!

![Step 1: Let's create a route table.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.6.png)

Step 1: Let's create a route table.

  

-   In the left navigation pane, choose **Route tables**.
    
-   Refresh your page.
    
-   Ooo, two route tables!
    
-   Check out the  **Routes**  tab for both, and note that they have different routes.
    

> 💡  **Why do I have two route tables? What do they do?**  
> As you might guess, one of your route tables was created with your AWS account's default VPC! This is the route table with two routes inside. AWS also created the other route table automatically when you set up  **NextWork VPC.**
> 
> ![Step 1: Your NextWork VPC's default route table.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.7.png)
> 
> Step 1: Your NextWork VPC's default route table.
> 
>   
> 
> -   This route table has a single route that allows traffic within the  **10.0.0.0/16**  CIDR block to flow within the network.
>     
> -   There is no route with an internet gateway as the target! This means there is no route for traffic to leave your VPC.
>     

-   Select the checkbox next to your NextWork VPC's default route table - this is the route table with a single route to 10.0.0.0/16.
    
-   Select the pencil icon in the  **Name**  column of your route table.
    
-   Enter the name  `NextWork route table`.
    

![Step 1: Name your route table.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.8.png)

Step 1: Name your route table.

  

-   Select the  **Routes**  tab.
    
-   Choose **Edit routes.**
    
-   Choose **Add route**  near the bottom of the page.
    
-   Destination: `0.0.0.0/0`
    

> 💡  **Why is the destination 0.0.0.0/0?**  
> 0.0.0.0/0 means  **all**  IPv4 addresses! When you set 0.0.0.0/0 as the destination in a route table, you are creating a default route that sends any traffic that doesn't match more specific routes on your route table.

![Step 1: A real conversation between internet-bound traffic and your route table.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.9.png)

Step 1: A real conversation between internet-bound traffic and your route table.

  

-   Target:  **Internet Gateway**.
    
-   Select the only **Internet Gateway** id option.
    
-   Choose **Save changes.**
    
-   Choose the **Subnet associations** tab.
    
-   Under the  **Explicit subnet associations**  tab, choose **Edit subnet associations**
    
-   Select **Public 1**.
    
-   Choose **Save associations.**
    

![Step 1: Your subnet is now associated!](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.10.png)

Step 1: Your subnet is now associated!

  

Ayyy nice! Your subnet is now public because it is connected to the Internet via the internet gateway!

  
  

**Create a security group**

In this task, let's add a security group so that users can access resources in your VPC.

![Step 1: Let's create a security group.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.11.png)

Step 1: Let's create a security group.

  

_Note that we won't be creating the diagram's EC2 instance in this step, but we're adding it to this diagram to illustrate a security group's scope!_

> **💡 What is a security group?**  
> A security group controls which traffic can enter or leave a  **resource**  based on its IP address, protocols and port numbers.  
>   
> Every  **resource**  must be associated with a security group. This means security groups don't attach to a VPC or a subnet, they attach to a specific  **resource**  within that VPC/subnet.

-   In the left navigation pane, choose **Security groups**.
    
-   Choose **Create security group**.
    
-   Security group name: `NextWork Security Group`
    
-   Description:  `A Security Group for the NextWork VPC`
    
-   VPC: **NextWork VPC**
    
-   Under the  **Inbound rules**  panel, choose **Add rule.**
    

> **💡 What's the difference between inbound and outbound rules?**  
> Inbound rules control the data that can enter the resources in your security group, while outbound rules control that data that your resources can send out.
> 
> -   **Examples of inbound data:**  Visitors to your website hosted on an EC2 instance in a public subnet, your website receives form submissions.
>     
> -   **Examples of outbound data:**  Your server requests data from another service, sends out an email notification.
>     

-   Type:  `HTTP`
    
-   Source: `Anywhere-IPv4`
    
-   At the bottom of the screen, choose **Create security group.**
    

  
  

**Create a Network ACL**

Nice, that's your traffic flow (route table) and basic security (security groups) sorted for your VPC!

To level up your VPC's security, let's add a network ACL i.e. network access control list.

![Step 1: Let's create a network ACL.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.12.png)

Step 1: Let's create a network ACL.

  

-   In the left navigation pane, choose **Network ACLs**.
    

> **💡 What are Network ACLs?**  
> Think of Network ACLs as community guards stationed at every entry and exit point of your  **subnet**, checking each data packet against a table of ACL rules before allowing them through.
> 
>   
> **💡 Data packets? What's that?**  
> When we talk about "traffic" moving through your VPC in AWS, we're actually talking about data packets! For example, when a user types your website's URL into their browser and presses enter, the "inbound traffic" entering your EC2 instance is actually data packets that represent your user's request to see your website.  
>   
> Data packets travel across the internet or within networks, and each packet contains a piece of the data being sent, e.g the user's request, or a part of a web page or a file. Network ACLs are responsible for inspecting and managing these data packets as they enter and exit your VPC's subnets, making sure only authorized data moves in and out.
> 
>   
> **💡 What's the difference between security groups and network ACLs?**
> 
> -   **Network ACLs**  are used to set broad traffic rules that apply to an entire  **subnet**. For example, blocking incoming traffic from a particular range of IP addresses or denying all outbound traffic to certain ports.
>     
> -   **Security groups**  allow for more granular control, managing access to individual  **resource**. You can specify which ports and protocols are allowed for each connected resource.  
>       
>       
>     

-   Choose the network ACL that's associated with your  **Public 1**  subnet, and check out the tabs for  **Inbound rules**  and  **Outbound rules**.
    

![Step 1: Your Inbound and Outbound rules.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.13.png)

Step 1: Your Inbound and Outbound rules.

  

> 💡  **What do the rules under the Inbound and Outbound rules tabs mean?**  Just like security groups, network ACLs use inbound and outbound rules to decide which data packets are allowed to enter or leave subnets:
> 
> -   **Rule 100 Inbound** allows all inbound traffic into the public subnet.
>     
> -   **Rule 100 Outbound** allows all traffic out of the public subnet.
>     
> -   The second line in each ruleset shows an asterisk (*) that acts as a catch-all rule in case traffic does not match any of the earlier rules. In our case, since Rule 100 already allows all traffic, the asterisk rule won't actually come into play.
>     
> 
> This means default network ACLs allow  **all**  inbound and outbound traffic, unless customized.

To solidify our learnings, let's recreate this set up ourselves in the console! Your default ACL has everything we need, but it's great practise to set up everything from scratch.

-   Name:  `NextWork Network ACL`
    
-   VPC:  **NextWork VPC**
    
-   Select  **Create network ACL.**
    
-   Select the checkbox next to your  **NextWork Network ACL**
    
-   Select the  **Inbound rules**  tab.
    

> 💡  **There is only one rule that denies all traffic! I thought all inbound and outbound traffic are allowed by default?**  
> Good spotting! The default network ACLs that AWS creates for us allow all inbound and outbound traffic. But for custom network ACLs that we create, all inbound and outbound traffic are denied until you add rules to specify that kind of traffic you'll allow.

-   Select  **Edit inbound rules.**
    
-   Select  **Add new rule**.
    
-   Rule number:  `100`
    
-   Type: **All traffic.**
    
-   Source:  `0.0.0.0/0`
    

![Step 1: Setting up a new inbound rule.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step1.14.png)

Step 1: Setting up a new inbound rule.

  

-   Click **Save changes.**
    

  
  

**Challenge:**  Do you think you could set up the same for your Network ACL's outbound rules?

Here are the steps again if you get stuck!

-   Select the  **Outbound rules**  tab.
    
-   Select  **Edit outbound rules.**
    
-   Select  **Add new rule**.
    
-   Rule number:  `100`
    
-   Type: **All traffic.**
    
-   Source:  `0.0.0.0/0`
    

  
  

-   Switch tabs from  **Outbound rules**  to the  **Subnet associations tab**.
    
-   Select  **Edit subnet associations.**
    
-   Select your  **Public 1**  subnet.
    
-   Select  **Save changes.**
    

  
  

Fantastic! You've done an incredible job setting up a functioning VPC.

Now let's dive into what's next for your VPC. 🤿

🚷 Step #2

### Set up a private subnet

  

We've learnt about subnets and even created a  **public subnet**  that's connected to the internet.

But what about resources that we want to keep private?

For example, it's very common for engineers to set up an EC2 instance hosting their web app in a public subnet, but keep the database of customers and login details in a  **private subnet**.

Let's set up your very first private subnet and learn its differences from a public subnet along the way.

![Step 2: Let's set up a private subnet!](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.subnet.png)

Step 2: Let's set up a private subnet!

  

-   Still in your VPC console, select the  **Subnets**  tab again.
    

![Step 2: Select the Subnets tab.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.1.png)

Step 2: Select the Subnets tab.

  

-   Select  **Create subnet**.
    
-   For the  **VPC ID,**  select  **NextWork VPC**.
    
-   Set the  **Subnet name**  as  `NextWork Private Subnet`
    
-   For the subnet's  **Availability Zone**, use the second AZ on the dropdown (not the first!)
    
-   The IPv4 VPC CIDR block is already pre-set to 10.0.0.0/16
    
-   For the IPv4 subnet CIDR block, what do you think will happen if this new subnet has the exact same CIDR block as your Public subnet?
    
-   Let's investigate by entering  `10.0.0.0/24`  to start with.
    
-   Select  **Create subnet**.
    
-   Aha! An error message.
    

![Step 2: An error message pops up next to your IPV4 subnet CIDR block.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.1.5.png)

Step 2: An error message pops up next to your IPV4 subnet CIDR block.

  

> 💡  **What does this error message mean?**  
> The error message says:  **CIDR Address overlaps with existing Subnet CIDR: 10.0.0.0/24.**  This error pops up when the CIDR block you're trying to assign to a new subnet is already being used by another subnet in the same VPC.  
>   
> Imagine if you were to build a new suburb in your city with the exact same set of street names and post codes as another suburb. Navigation would become very confusing - some addresses in your city would have two possible locations!  
>   
> For the same reason, every subnet in a VPC must have a unique CIDR block so traffic is routed correctly and there are no conflicts.

-   How would you fix this error?
    
-   Let's assign your new subnet a CIDR block that doesn't overlap with Public 1.
    
-   Replace the IPv4 subnet CIDR block with  `10.0.1.0/24`
    

> 💡  **How does this new CIDR block not overlap with Public 1's CIDR block?**  
> By setting the CIDR block of your new private subnet to  `10.0.1.0/24`, you allocate a specific range of IP addresses from  `10.0.1.0`  to`10.0.1.255`.
> 
> The  **Public 1**  subnet is defined with the CIDR block  `10.0.0.0/24`, which is a different range of IP addresses from  `10.0.0.0`  to  `10.0.0.255`.
> 
> Notice the small difference between these CIDR blocks - your private subnet's CIDR block is 10.0.**1**.0/24, whereas the public subnet's CIDR block is 10.0.**0**.0/24. That's what keeps each range complete separate from each other!

![Step 2: Create your NextWork Private Subnet.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.2.png)

Step 2: Create your NextWork Private Subnet.

 
-   Select  **Create subnet**.
    
-   Success!
    
-   To tidy up your subnets' naming conventions, let's retitle your  **Public 1**  subnet to  `NextWork Public Subnet`
    

![Step 2: Rename your public subnet.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.4.png)

Step 2: Rename your public subnet.

  

🚧 Step #3

### Set up a private route table

  

Like your public subnet, a private subnet also needs to be associated with a route table.

![Step 3: Let's create a new route table.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.routetable.png)

Step 3: Let's create a new route table.

  

-   Head to the  **Route tables**  page in your console.
    

> 💡  **Why are we revisiting the Route tables page?**  
> Back when you set up  **NextWork route table**, you renamed the default route table that AWS automatically created with your VPC.
> 
> This means  **NextWork route table**  is the default route table for your  _entire_  VPC. Subnets that aren't associated with another route table automatically use  **NextWork route table.**
> 
> Should your private subnet use the same route table as your public subnet?
> 
> Probably not!  **NextWork route table**  has a route to an internet gateway, and having that route would make your subnet public! It's time to set up a new route table for your private subnet.

-   Select  **Create route table**.
    
-   Name your new route table  `NextWork Private Route Table`
    
-   Under  **VPC**, select  **NextWork VPC**.
    
-   Select  **Create route table.**
    

![Step 3: Set up a new route table.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.5.png)

Step 3: Set up a new route table.

  

-   Nice! With your private route table set up, let's make sure it can only direct traffic to another internal resource (instead of the public internet).
    
-   Select  **NextWork Private Route Table**.
    
-   Check the  **Routes**  tab - does it only have one default route with a  **local**  target?
    

![Step 3: Check the routes tab.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.6.png)

Step 3: Check the routes tab.

  

-   Switch tabs to  **Subnet associations.**
    
-   Select  **Edit subnet associations**  under the  **Explicit subnet associations**  tab.
    
-   Select the checkbox next to  **NextWork Private Subnet**.
    
-   Select  **Save associations**.
    

![Step 3: Edit subnet associations.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.7.png)

Step 3: Edit subnet associations.

  

-   To tidy up your Route tables' naming conventions, let's also retitle  **NextWork route table**  to  `NextWork Public Route Table`
    

![Step 3: Rename your public route table.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.8.png)

Step 3: Rename your public route table.

  






🚔 Step #4

### Set up a private network ACL

  

Your private subnet is set up!

A dedicated route table is all done too!

Now to round things off, let's set up a new network ACL.

Oops! The image failed to load.  
Please try refreshing and  [let us know](https://community.nextwork.org/c/i-have-a-question?automatic_login=true&utm_source=app&utm_campaign=server_error)  if the problem persists.

Refresh

Step 4: Let's create a new network ACL.

  

-   Select  **Network ACLs**  from the left hand navigation panel.
    
-   Select the checkbox next to the default ACL for your VPC.
    
    -   Note that this is NOT  **NextWork Network ACL**  - your default ACL isn't named!
        
-   Select the  **Inbound rules**  and  **Outbound rules**  tabs.
    

![Step 4: Review the default ACL for your VPC.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.9.png)

Step 4: Review the default ACL for your VPC.

  

> 💡  **Why are we reviewing our default network ACL?**  
> It's a very similar scenario to the route tables!
> 
> You might recall that there is a default network ACL set up for every VPC. This default network ACL is associated with your private subnet, since you haven't set up an explicit association between your private subnet and another network ACL.
> 
> A VPC's default network ACL allows  **all**  traffic, which exposes your private subnet to unrestricted access from the internet or other untrusted networks. Let's set up a new network ACL that restricts traffic and protects your private subnet!
> 
> 💡  **We've already removed the route to an internet gateway. Isn't that enough to prevent traffic from the internet?**  
> Ooo great catch! Removing a route to the internet gateway  _does_  prevent direct internet access to and from the subnet. However, relying only on route table configurations might not be great for security.
> 
> If any part of your VPC (e.g. your public subnet) gets compromised, the attacker could take advantage of your permissive ACL setup to access or attack the resources in your private subnet!

-   So while the default ACL is very convenient in allowing all traffic types, we'll create a new custom network ACL to keep our private subnet safe.
    
-   Select  **Create network ACL**  on the top right.
    
-   For the name, enter  `NextWork Private NACL`.
    
-   Select  **NextWork VPC**.
    
-   Select  **Create network ACL**.
    
-   Done!
    
-   Observe the  **Inbound rules**  and  **Outbound rules**  tabs for your private network ACL.
    

> 💡  **Why are they both denying all traffic?**  
> Remember that custom network ACLs start with denying all inbound and outbound traffic! We'll leave these settings for now - let's customise them later in this project series, when we know exactly which traffic source we're wanting to allow.

![Step 4: Check your network ACL's inbound rules.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.10.png)

Step 4: Check your network ACL's inbound rules.

![Step 4: Check your network ACL's outbound rules.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.11.png)

Step 4: Check your network ACL's outbound rules.

  

-   Switch tabs to  **Subnet associations.**
    
-   Select  **Edit subnet associations.**
    
-   Select your private subnet.
    
-   Select  **Save changes.**
    

![Step 4: Check your network ACL's subnet associations.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.12.png)

Step 4: Check your network ACL's subnet associations.

  

-   To tidy up your Network ACLs' naming conventions, let's also rename  **NextWork Network ACL**  to  `NextWork Public NACL`
    

![Step 4: Rename your public network ACLs.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step2.13.png)

Step 4: Rename your public network ACLs.

 
All done! Your private subnet is set up and ready to goooooo.

> 💡  **What about security groups?**  
> Remember how security groups are set at the  **resource**  level? This means you won't need to create security groups until there is a specific resource e.g. EC2 instance you're launching in your subnet! We'll be setting up security groups in an alternative way later in this series...

😮‍💨 All Done

### Nice work!

  

You've just completed today's project and  **set up your very own private subnet in an Amazon VPC.**







🗑️ Before You Go

### Delete Your Resources

  

> 🤫  **If you have time for another project today...**  
> Did you know that the next project in our networking series—[Launching VPC Resources](https://learn.nextwork.org/projects/aws-networks-ec2)—will build directly on top of what you've created here?
> 
> If you're going to start the next project  **today**, you won't need to delete your resources yet. Just head straight to  [Launching VPC Resources!](https://learn.nextwork.org/projects/aws-networks-ec2)
> 
> **Delete**  the resources in your AWS account if you're planning to continue this series another day.

✋  **STOP**

Before diving into the steps for deleting your resources, why not challenge yourself to delete everything in this project on your own?

Keeping track of your resources, and deleting them at the end, is absolutely a skill that will help you reduce waste in your account.

  
  

🛑  **STEPS BELOW:**

-   In your  **VPC console**, select the checkbox next to  **NextWork VPC**.
    
-   Select the  **Actions**  dropdown.
    
-   Select  **Delete VPC**.
    

![Step 6: Delete your VPC.](https://learn.nextwork.org/projects/static/aws-networks-private/high-step8.2.png)

Step 6: Delete your VPC.

  

Now visit each of the pages below!  **Refresh**  your the page before checking if the resource you created today is still in your account. They should be automatically deleted with your VPC, but it's always a good idea to check anyway:

1.  Subnets
    
2.  Route tables
    
3.  Internet gateways
    
4.  Network ACLs
    
5.  Security groups
    

 
      


### Nice Work!

  

THAT'S NETWORKING PROJECT THREE...

DONE!!!!! 🥳

![Your amazing work today!](https://learn.nextwork.org/projects/static/aws-networks-private/architecture-clean.png)

Your amazing work today!

  

**Today you've learnt how to:**

-   🚷  **Create a private subnet:**  You created a new subnet and set its CIDR block to avoid an overlap with your public subnet.  
      
      
    
-   🚧  **Create a private route table:**  You also made this subnet private by assigning it to a dedicated route table that doesn't route traffic to an internet gateway!  
      
      
    
-   🚔  **Create a private network ACL:**  Then, you set up custom network ACLs to control inbound and outbound traffic for this private subnet - denying all traffic by default.  

### 👏 All done!

