

# VPC Monitoring with Flow Logs



WHAT YOU'LL NEED

-   An AWS account -  [Create one here!](https://github.com/dineshrajdhanapathyDD/Cloud/blob/main/AWS/NextWork%20AWS%20Documentation/5%20AWS%20BASIC/legendary-aws-account-setup.pdf))

-   Part 1 of this series -  [Build a Virtual Private Cloud](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%201%20Build%20a%20Virtual%20Private%20Cloud)
-   Part 2 of this series -  [VPC Traffic Flow and Security](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%202%20VPC%20Traffic%20Flow%20and%20Security)

-   Part 3 of this series -  [Creating a Private Subnet](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%203%20Creating%20a%20Private%20Subnet%20in%20Your%20Amazon%20VPC)

-   Part 4 of this series -  [Launching VPC Resources](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%204%20Launching%20VPC%20Resources)

-   Part 5 of this series -  [Testing VPC Connectivity](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%205%20Testing%20VPC%20Connectivity)

-   Part 6 of this series -  [VPC Peering](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%206%20VPC%20Peering)

KEY CONCEPTS

-   [Amazon VPC](https://www.youtube.com/watch?v=Pazb3rS_Ers)
-   [Amazon EC2](https://youtu.be/fHY1naCZ9Y0?feature=shared)
-   [Amazon CloudWatch](https://youtu.be/z1qc4Sh8S5I?feature=shared)

## ⚡️ 30 second Summary

Welcome to another AWS networking project (#7) ✨

Are you ready to spice things up again with your VPC?! 🌶️📊

  
  

**In your first six networking projects, you've created:**

1.  ☁️ An Amazon VPC (super cool!)
    
2.  💻 EC2 instances in your public and private subnets (huuuuuuuge!)
    
3.  🧪 Connectivity tests to validate your VPC set up (let's GO!)
    
4.  🌉 Peering connections to bridge two VPCs together (that's 200 IQ!)
    

  
  

If you haven't done the previous project in our networking series,  **VPC Peering**, we'd highly recommend doing that first. This project starts right where the previous one leaves off.

![What you've learnt from your first six networking projects of this series!](https://learn.nextwork.org/projects/static/aws-networks-monitoring/architecture-past.png)

What you've learnt from your first six networking projects of this series!

  

In today's project,  **VPC Monitoring with Flow Logs**, we're jumping right back into where we left off and adding  **monitoring**  to our VPC.

  
  

**💭 What's network monitoring?**

Network monitoring is how engineers keep track of their network's traffic and analyze it too.

For example, network monitoring includes:

-   📊 Checking the source of traffic coming into your VPC,
    
-   📊 Analysing how much data is being transferred in your network, and
    
-   📊 Identifying traffic that's been blocked by your security settings.
    

  
  

Once you get to a more advanced stage, network monitoring also includes optimizing your network setup to speed up data transfers, automating responses to security threats, and so much more!

  
  

**⭐️ Why is this important?**

At the end of the day, a network exists to:

1.  Let resources in our network talk to each other + resources outside our VPC
    
2.  Make sure they are talking to each other in the most secure way possible!
    

  
  

So for engineers and network administrators, network monitoring is how they know whether a network is doing these two things well.

Otherwise, it'd be hard to tell whether their network is running smoothly and actually protecting resources against threats!

Let’s kick off network monitoring today by adding tracking tools to our VPC set up 👀

Introducing two new characters today's project ....

🦸‍♀️  **VPC Flow Logs**  and 🦹‍♀️  **Amazon CloudWatch!**

  
  

**Get ready to:**

1.  ☁️ Set up two VPCs and test their peering connection.
    
2.  🛶 Set up VPC Flow Logs that collect network traffic data.
    
3.  🧠 Analyse network traffic using CloudWatch's Log Insights.
    

![Today's game plan!](https://learn.nextwork.org/projects/static/aws-networks-monitoring/architecture-today.png)

  





    

  
  



  
  




    

  
  


  
  



  


  
  






  



  



### ☁️ Step #1

### Set up your VPCs in Minutes

  

Now that we've learnt about the VPC wizard from our previous projects, let's use it to set up TWO VPCs in minutes.

p.s. You can absolutely set up monitoring for architectures with a single VPC, but we're settings up two VPCs today so we can revise some learnings from the VPC peering project too!

  
  

**In this step, you're going to:**

1.  Create two VPCs from scratch!
    

![Step 1: Let's set up two VPCs in minutes.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step1.0.png)

Step 1: Let's set up two VPCs in minutes.

  



-   [Log in to your AWS Account.](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26state%3DhashArgsFromTB_ap-southeast-2_fffdf5be4bb1a27e&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=m-aiqeB2UZeXTGXNyugMP8L64zd_AGUxJl4HLnA-X1o&code_challenge_method=SHA-256)
    
-   Head to your **VPC** console - search for  `VPC`  at the search bar at top of your page.
    
-   From the left hand navigation bar, select **Your VPCs.**
    
-   Select **Create VPC.**
    
-   Select **VPC and more.**
    

![Step 1: Select VPC and more.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step1.1.png)

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
    

![Step 1: We're moving ahead with just one public subnet!](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step1.3.png)

Step 1: We're moving ahead with just one public subnet!

  

-   Next, for the **NAT gateways ($)** option, make sure you've selected **None.** As the dollar sign suggests, NAT gateways cost money!
    

![Step 1: Select None for the NAT gateways option.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step1.4.png)

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
    

![Step 1: Leave DNS options checked.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step1.5.png)

Step 1: Leave DNS options checked.

  

-   Select **Create VPC.**  
      
    

![Step 1: Your VPC gets set up super fast!](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step1.6.png)

Step 1: Your VPC gets set up super fast!

  

-   Select **View VPC**.
    
-   Select the **Resource map** tab - nice, all of these resources have been set up for you in a flash!
    

  
  
  

**Set up VPC 2**

Challenge yourself - can you set up your second VPC without any guidance?

Your second VPC has the exact same settings, except:

-   Under **Name tag auto-generation**, enter `NextWork-2`
    
-   The VPC's **IPv4 CIDR block** should be unique! Make sure the CIDR block is  `10.2.0.0/16`  - NOT `10.1.0.0/16`
    

> 💡 **Why do they need to be unique?**  
> Each VPC must have a unique IPv4 CIDR block so the IP addresses of their resources don't overlap. Having overlapping IP addresses could cause routing conflicts and connectivity issues!

![Step 1: Use a new name tag and CIDR block.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step1.7.png)

Step 1: Use a new name tag and CIDR block.

  





### 💻 Step #2

### Launch EC2 Instances

  

Wooohooo, now it's time to launch EC2 instances into your architecture!

We need to create these EC2 instances so that they can send data to each other later in the project, which gives us network activity to monitor.

  
  

**In this step, you're going to:**

1.  Launch an EC2 instance in each VPC, so we can use them to test your VPC peering connection later.
    

![Step 2: EC2 instances have joined the party 🥳](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step2.0.png)

Step 2: EC2 instances have joined the party 🥳

  



**Launch an instance in VPC 1**

-   Head to the **EC2 console** - search for `EC2` in the search bar at the top of screen.
    
-   Select **Instances** at the left hand navigation bar.
    
-   Select **Launch instances**.
    
-   Since your first EC2 instance will be launched in your first VPC, let's name it `Instance - NextWork VPC 1`
    
-   For the **Amazon Machine Image,** select **Amazon Linux 2023 AMI.**
    
-   For the **Instance type,** select **t2.micro.**
    
-   For the **Key pair (login)** panel, select **Proceed without a key pair (not recommended).**
    

![Step 2: We shall proceed without a key pair.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step2.1.png)

Step 2: We shall proceed without a key pair.

  

> 💡 **Why aren't we setting up a key pair? Wasn't this step important in the last few projects?**  
> In previous projects, setting up a key pair was a key step for learning how SSH and directly accessing an EC2 instance works.
> 
> However, we've also learnt that with  **EC2 Instance Connect,**  AWS actually manages a key pair for us! We don't need to manage key pairs ourselves. Since we've already learnt how to set up key pairs twice in the last two projects, we don't need to do it again this time.
> 
>   
> 💡  **What is EC2 Instance Connect?**  
> EC2 Instance Connect is an EC2 tool designed to help you get direct access to your EC2 instance!
> 
> Once you get direct access to your EC2 instance, you're going into the instance's terminal. This lets you do some advanced work like installing software into your EC2 instance or accessing another AWS service!

-   At the **Network settings** panel, select **Edit** at the right hand corner.
    

> 💡 **Why are we editing the Network settings?**  
> By default, all resources are launched into the default VPC that AWS has set up for your account. We need to tell AWS that we actually want to launch this instance in **NextWork-vpc-1.**

-   Under  **VPC**, select **NextWork-vpc-1**.
    
-   Under  **Subnet,**  select your VPC's public subnet.
    
-   Keep the **Auto-assign public IP** setting to... do you remember whether our EC2 instance needs a public IP address?
    

> 💡 **Hmmm, I can't seem to remember. What is it?**  
> Don't forget - we're using EC2 Instance Connect after this to connect with our EC2 instance.
> 
> EC2 Instance Connect requires instances to be in a public subnet AND  **have a public IPv4 address.**

-   Select  **Enable.**
    

![Step 2: Your networking settings.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step2.2.png)

Step 2: Your networking settings.

  

-   For the **Firewall (security groups)** setting, choose **Create security group.**
    

> 💡 **Why are we creating a new security group?**  
> In the last project, we chose to use the default security group from Amazon VPC, but later saw some connectivity issues when we tried to connect to it!
> 
> Let's avoid those connectivity issues by setting up a new security group with all the right settings from the get go 💪

Do you remember which are the security group settings you'll need for your instance?

⏸️ Challenge yourself to set this up yourself first before referring to the steps below!

▶️ Alright - steps below!

-   Name your security group  `NextWork-1-SG`
    
-   Choose  **Add security group rule.**
    
-   For the new rule's  **Type**, select  **All ICMP - IPv4.**
    
-   For the new rule's  **Source**, select  `0.0.0.0/0`
    

![Step 2: Your new security group settings.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step2.3.png)

Step 2: Your new security group settings.

  

> 💡  **Why are we allowing ICMP traffic from all IP addresses?**  
> We'll be doing a new ping test in just a second... it's going to require your security group to allow in ICMP traffic from  **all**  IP addresses, not just from the other VPC!

-   Select **Launch instance.**
    

  
  
  

**Launch an instance in VPC 2**

You know the drill - do you think you can set up an EC2 instance in VPC 2?

If you get stuck, use the same instructions above but make sure:

-   The  **Name**  is `Instance - NextWork VPC 2`
    
-   The  **VPC**  is **NextWork-vpc-2**.
    
-   Make sure you select  **Enable**  for  **Auto-assign public IP**  here too
    
-   Name your security group  `NextWork-2-SG`
    
-   Allow ICMP traffic from ALL IP addresses.
    

![Step 2: Your two EC2 instances.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step2.4.png)

Step 2: Your two EC2 instances.

  



### 🛶 Step #3

### Set Up Flow Logs

  

EC2 instances LAUNCHED 🚀

Next up, are you ready to start monitoring VPC traffic?!

We're using a tool called VPC flow logs to do this... let's set them up in this step.

  
  

**In this step, you're going to:**

1.  Set up a way to track all inbound and outbound network traffic.
    
2.  Set up a space that stores all of these records.
    

![Step 3: Let's set up flow logs!](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.0.png)

Step 3: Let's set up flow logs!

  


-   Navigate to the **CloudWatch console**  - search for  `CloudWatch`  in your Management Console's search bar.
    

![Step 3: Search for CloudWatch.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.1.png)

Step 3: Search for CloudWatch.

  

> 💡  **Amazon CloudWatch**  is a powerful  **monitoring**  service that watches over everything happening in your AWS environment in real time.
> 
> AWS services would report to CloudWatch with their metrics, which are stats or measurements of the service's performance. You can then use CloudWatch to take these metrics and transform them into clear, easy-to-read graphs and dashboards to help you understand your AWS environment's performance and health health.
> 
> For example, if you were hosting an application on AWS, your dashboard could track how quickly your app is loading for your users.
> 
> Another great use case of CloudWatch is that you can set it to automatically do actions based on key metrics! For example, you could set CloudWatch to automatically shut down a VPC if it detects that it's letting in illegitimate traffic.

-   Check the  **Region**  you're on - is this the same Region as the one you've used to launch your VPCs?
    
    -   Double check your Region by looking at the top right hand corner of your console. Your Region is right next to your account name!
        

![Step 3: Choose your Region.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.2.png)

Step 3: Choose your Region.

  

> 💡  **Why is it important to select the same Region?**  
> CloudWatch data is region-specific! That means the data collected on your VPC in one region is not automatically available in other regions.
> 
> If you're using a region outside of the one you used to launch your VPCs, you won't get access to CloudWatch's metrics on your VPC!

-   At the left hand navigation panel, click **Log groups** under **Logs.**
    

![Step 3: Select Logs.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.3.png)

Step 3: Select Logs.

  

-   Click **Create log group** at the top right.
    

![Step 3: Select Create log group.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.4.png)

Step 3: Select Create log group.

  

> **💡 What is a log group?**  
> Think of a log group as a big folder in AWS where you keep related logs together. Usually, logs from the same source or application will go into the same log group, BUT logs are also region-specific. This means log data gets created and saved in the region it was created, although you can use CloudWatch dashboards to bring together logs from different regions.
> 
>   
> **💡 What are logs?**  
> Logs are like a diary for your computer systems. They record everything that happens, from users logging in to errors popping up. It's the go-to place to understand what's going on with your systems, troubleshoot problems, and keep an eye on who’s doing what.

-   Enter `NextWorkVPCFlowLogsGroup` as the  **Log group name.**
    

![Step 3: Enter a log group name.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.5.png)

Step 3: Enter a log group name.

  

-   That's it! Click **Create.**
    

![Step 3: Your created log group.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.5.5.png)

Step 3: Your created log group.

  

> **💡 Wow there were some interesting settings we skipped! What were they about?**  
>   
> 
> 1.  **Retention setting**  is  **Never expire**  by default, which means your logs won’t be deleted over time. They’ll stick around as long as you need them, unless you decide to clear them out yourself.  
>     
>     ![Step 3: Retention setting.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.6.png)
>     
>     Step 3: Retention setting.
>     
>       
>     
> 2.  **Log class**  is  **Standard**  by default, which means the logs that get created will get accessed or analyzed regularly.  
>     If we chose  **Infrequent Access**  instead, your logs will be stored for long-term archiving - you are charged less for storage, but higher for each time you need to access the, for analysis. This setting isn't quite important since our usage will fall under the Free Tier!  
>     
>     ![Step 3: Log class.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.7.png)
>     
>     Step 3: Log class.
>     
>       
>     



-   Head back to your  **VPC**  console.
    
-   Select the  **Your VPCs**  page.
    
-   Select **NextWork-1-vpc.**
    
-   Scroll down to the **Flow Logs** tab, and click on **Create flow log.**
    

> ![Step 3: Click on Create flow log.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.8.png)
> 
> Step 3: Click on Create flow log.
> 
>   
> 
> **💡 What is a flow log?**  
> Now that we know that logs are digital diaries that services keep, think of flow logs as a specific type of diary for VPCs. Flow logs capture traffic going to and from the network - noting down who's visiting your VPC and the specific network interface it going to!
> 
>   
> **💡 What are network interfaces?**  
> Network interfaces are small but powerful components in a network!
> 
> We've previously learnt that subnets are subdivisions, or neighbourhoods, inside your VPC.
> 
> Think of network interfaces as another layer down - they are even smaller subdivisions of your subnet! Since your subnets are like neighbourhoods, think of a network interface as a specific building or block inside that neighbourhood.
> 
> Network interfaces exist to connect your resources to your VPC! For example, whenever you launch an EC2 instance, AWS automatically creates a primary network interface with a private IP address from your subnet's IPv4 CIDR block. That's how your EC2 instance gets a private IP address.
> 
> They're not too important in simple networks like ours, but network interfaces become very powerful when you have complex network situations, like wanting an EC2 instance to belong to two subnets at once!  _😳_
> 
>   
> **💡 Why do flow logs track traffic to network interfaces?**  
> Flow logs are associated with specific network interfaces because each interface represents a distinct point where traffic enters or exits an EC2 instance or other AWS resources. No two resources can share the same network interface!

-   Welcome to the **Flow log settings**  page! Nice, you've just unlocked a new section of VPC set up.
    
-   Enter `NextWorkVPCFlowLog` in the **Name** field.
    
-   Set **Filter** to **All.**
    

![Step 3: Make sure your Filter is set to All.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.9.png)

Step 3: Make sure your Filter is set to All.

  

> **💡 What does Filter do?**  
> The  **Filter**  setting in the context of VPC flow logs determines the type of traffic that is logged.
> 
> Setting the filter to  **All**  means that it captures all the traffic flowing in and out of the VPC.
> 
> The other option,  **Accept**, means only traffic that was successfully allowed through your security groups and network ACLs get logged - great for understanding what kind of traffic is being let through.
> 
> There's also a  **Reject**  filter that only captures the traffic blocked by your network settings - great for detecting illegitimate traffic trying to access your resources, or any network setting issues!

-   Set the  **Maximum aggregation interval** to **1 minute**
    

![Step 3: Is Maximum aggregation interval set to 1 minute?](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.10.png)

Step 3: Is Maximum aggregation interval set to 1 minute?

  

> **💡 What does the maximum aggregation interval mean?**  
> **The maximum aggregation interval**  means how often traffic flow data will get lumped into a single flow log record. If you set the interval to '1 minute', flow log records are generated every minute.
> 
> This gives you a more granular view of network traffic compared to '10 minutes', which would give you less frequent and potentially less detailed records.

-   Leave **Destination** as **Send to CloudWatch Logs.**
    

![Step 3: Let's make sure the logs get sent to CloudWatch.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.11.png)

Step 3: Let's make sure the logs get sent to CloudWatch.

  

> **💡 Wow there are other Destination options?**  
> Yup, besides sending your flow logs straight to to CloudWatch, you can also send them to  **Amazon S3.**  This option is useful if you need to archive logs for cost-effective, long-term storage or use them with other analytics and processing tools in the future.
> 
> **Amazon Data Firehose**  is another destination! Data Firehose is a handy option that lets you process and analyze data in real-time (whereas S3 is better for storing large volumes of data that don't need real-time analysis).

-   Set **Destination log group** as **NextWorkVPCFlowLogsGroup.**
    
-   Under the  **IAM role**, you might notice that there isn't an IAM role that's designed for Flow Logs!
    

![Step 3: Whoopsies... no Flow Log IAM role to be found.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step3.12.png)

Step 3: Whoopsies... no Flow Log IAM role to be found.

  

Let's set up an IAM role for your Flow Logs!

### 💂 Step #4

### Set Up A Flow Log IAM Policy and Role

  

Aha, so VPC Flow Logs doesn't have the permission to write logs and send them to CloudWatch... yet.

Let's give Flow Logs the permission to do both, using the power of IAM roles and policies!

  
  

**In this step, you're going to:**

1.  Give VPC Flow Logs the permission to write logs and send them to CloudWatch.
    
2.  Finish setting up your subnet's flow log.
    



-   Select that handy  **Set up permissions**  link under  **IAM role.**
    

![Step 4: Click on Set up permissions.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.1.png)

Step 4: Click on Set up permissions.

  

> 💡  **Why am I setting up permissions here?**  
> VPC Flow Logs doesn't have the permission to write logs and send them to CloudWatch... yet. Let's give Flow Logs the permission to do both, using the power of IAM roles and policies!

-   In the navigation pane, choose **Policies**.
    

![Step 4: Click on Policies.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.2.png)

Step 4: Click on Policies.

  

-   Choose **Create policy**.
    

![Step 4: Select Create policy.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.3.png)

Step 4: Select Create policy.

  

-   Choose **JSON**.
    
-   Delete everything in the  **Policy editor.**
    
-   Add this JSON policy to the empty Policy editor:
    

json

Copy code

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents",
        "logs:DescribeLogGroups",
        "logs:DescribeLogStreams"
      ],
      "Resource": "*"
    }
  ]
}

```

![Step 4: Your JSON policy.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.4.png)

Step 4: Your JSON policy.

  

> **💡 Why are we creating this policy? What does this policy say?**  
> VPC Flow Logs by default don't have the permission to record logs and store them in your CloudWatch log group. This policy makes sure that your VPC can now send log data to your log group!
> 
> We can also break this statement down line by line:  
> 
> ![Notes on your JSON policy ✍️](https://learn.nextwork.org/projects/static/aws-networks-monitoring/json-annotated.png)
> 
> Notes on your JSON policy ✍️
> 
> **Version: "2012-10-17"**  
> The version of IAM policy language that you're using. This is the latest version of IAM policy language, older policies use 2008-10-17!  
> **Statement:**  
> This section contains the set of permissions that make up this policy.  
> **Effect: "Allow"**  
> This line states that the actions you're about to list below are allowed. This line is quite powerful - if you change "Allow" to "Deny", this policy would immediately block Flow Logs from creating and sending logs!  
>   
> **Action:**  
> This section lists specific actions that are allowed under this policy:
> 
> -   **logs:CreateLogGroup**: Allows the IAM role to create new log groups in CloudWatch.  
>       
>     
> -   **logs:CreateLogStream**: Allows the IAM role to create log streams within those groups.  
>       
>     
> -   **logs:PutLogEvents**: Allows the IAM role to send log data to the streams.  
>       
>     
> -   **logs:DescribeLogGroups**  and  **logs:DescribeLogStreams**: These actions allow the role to see information about the log groups and streams.  
>       
>     **Resource: "*"**  
>     This specifies that the permissions apply to all log groups and streams.
>     


-   Choose **Next**.
    
-   For your policy's name, let's call it  `NextWorkVPCFlowLogsPolicy`
    
-   Choose **Create policy**.
    

  
  
Nice, IAM policy done!

Can we head back to your Flow Logs set up now?

Not quite...

Don't forget that your Flow Logs set up is asking for an IAM  **role**.

> **💡 What's the difference between an IAM policy and role? Why did we need to create the policy just now?**  
> IAM policies and roles go hand in hand, so it's important to know their differences and how they work together!
> 
> 1.  IAM policies are like rules that determine what someone/something can or cannot do in your AWS account.  
>       
>     
> 2.  When you bundle IAM policies together, you create an IAM role. You then assign this role to AWS services or users, giving them the permissions included in the attached policies.  
>       
>     
> 
>   
> **💡 I'm still a bit lost on the differences between policies and roles...**  
> As an analogy, imagine you manage a big hotel! Think of IAM policies as rules that allow/deny specific parts of the hotel e.g. the staff elevator, rooms at the top floor, the hotel gym, the front desk computers.
> 
> Then, hotel guests are assigned IAM roles made up of combinations of IAM policies, giving them access to their own room and the hotel gym while denying access to other people's rooms.
> 
> Hotel staff are also assigned IAM roles made up of the right mix of policies that give them access to the rooms and tools they need to do their jobs!
> 
>   
> **💡 So you can't assign an IAM policy directly to a service, you have to assign ROLES to a service?**  
> Yup! It's typically a three step process (which is what you're doing now):
> 
> 1.  Create IAM policies (you just did this)  
>       
>     
> 2.  Create IAM role (you're about to do this)  
>       
>     
> 3.  Assign the IAM role to services (you'll do this soon too).
>     

-   In the left hand navigation pane, choose **Roles**.
    

![Step 4: Choose Roles.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.5.png)

Step 4: Choose Roles.

  

-   Choose **Create role**.
    

![Step 4: Choose Create role.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.6.png)

Step 4: Choose Create role.

  

-   For **Trusted entity type**, choose **Custom trust policy**.
    

![Step 4: Choose Custom trust policy.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.7.png)

Step 4: Choose Custom trust policy.

  

> **💡 What is a custom trust policy**  
> A custom trust policy is specific type of policy! They're different from IAM policies. While IAM policies help you define the actions a user/service can or cannot do, custom trust policies are used to very narrowly define who can use a role.
> 
> Here's another way to think about it: using a custom trust policy is like using a special VIP list - only the services you pinpoint in your policy would be allowed to use your role.
> 
>   
> **💡 Why did we pick Custom trust policy here?**  
> Don't forget why we're creating an IAM role - to give VPC Flow Logs the permission to write and send logs to CloudWatch. We only want Flow Logs to have this access, not just any service.
> 
> By choosing a custom trust policy, we're making sure that only VPC Flow Logs can use this role.
> 
>   
> **💡 Extra for Experts:**  But we could assign permissions using the "AWS service" option too, why didn't we pick that?
> 
> That's a 10/10 question! Try giving it a go - can you select  **AWS service**  as the  **Trusted entity type**, and specify we only want to give permissions to VPC Flow Logs?
> 
> ![Where is the option for VPC Flow Logs?](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.75.png)
> 
> Where is the option for VPC Flow Logs?
> 
> Yup, you'll find that you can't actually find an option for VPC Flow Logs!
> 
> VPC Flow Logs is technically just a feature within the wider Amazon VPC service (instead of being its own standalone AWS service), so we'd have to use a custom trust policy to assign permissions specifically to VPC Flow Logs.

-   A custom trust policy panel pops up!
    
-   Replace `"Principal": {},` with the following:
    

json

Copy code

```json
"Principal": {
   "Service": "vpc-flow-logs.amazonaws.com"
},

```

-   To avoid any errors, make sure the statement is well formatted and the spacing of your lines look exactly like this!
    

![Step 4: Make sure your Statement line has the right formatting.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.8.png)

Step 4: Make sure your Statement line has the right formatting.

  

> **💡 What does this statement mean?**  
> The statement  `"Service": " vpc-flow-logs.amazonaws.com "`  in a trust policy specifically points to VPC Flow Logs as the only service that can use this role!
> 
> Even if you try to give this role to other AWS services, they can't use it because the permissions are locked down to just VPC Flow Logs. This is so good for security, in case this role gets accidentally assigned to another service/user.
> 
> Hot tip:  `"Principal"`  defines the entity that is given the permissions in this policy. In this case, the entity is a service (VPC Flow Logs), but other entity types are IAM Users and IAM roles!



-   Choose **Next**.
    
-   On the **Add permissions** page, search for the policy you've created -  `NextWorkVPCFlowLogsPolicy`
    
-   Select your policy.
    

![Step 4: Select the policy you created.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.9.png)

Step 4: Select the policy you created.

  

-   Choose **Next**.
    
-   Enter a name for your role -  `NextWorkVPCFlowLogsRole`.
    
-   Choose **Create role**.
    

  
  
  

Phew! IAM role set up DONEEEE 🔥

-   Head back to your VP console's  **Create flow log**  page.
    

![Step 4: Head back to this page.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.10.png)

Step 4: Head back to this page.

  

-   Select the  **refresh**  button next to the IAM role field.
    
-   Select your IAM role -  **NextWorkVPCFlowLogsRole**.
    

![Step 4: Pick your IAM role.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.11.png)

Step 4: Pick your IAM role.

  

-   Click on **Create flow log.**
    

![Step 4: Your created flow log.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step4.12.png)

Step 4: Your created flow log.

  



Nice - the flow log is all set up! This means network traffic going into and out of your VPC is  **now getting tracked**  🔥

### 🧪 Step #5

### Test VPC Peering

  

Phew, flow log set up is all done!

Let's generate some network traffic and see whether our flow logs can pick up on them.

We're going to generate network traffic by trying to get our instance in VPC 1 to send a message to our instance in VPC 2.

Since we're trying to get our instances to talk to each other, this means we're also testing our VPC peering setup at the same time! Two birds, one step 😎

  
  

**In this step, you're going to:**

1.  Get Instance 1 to send test messages to Instance 2.
    



-   Head to your  **EC2** console and the  **Instances**  page.
    
-   Select the checkbox next to  **Instance - NextWork VPC 1.**
    
-   Select **Connect**.
    
-   In the EC2 Instance Connect set up page, select  **Connect**  again.
    
-   Phew! Success.
    

![Step 5: Feels good to see we've connected right away!](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step5.1.png)

Step 5: Feels good to see we've connected right away!

  

-   Leave open the **EC2 Instance Connect** tab, but head back to your **EC2** console in a new tab.
    
-   Select **Instance - NextWork VPC 2.**
    
-   Copy Instance - NextWork VPC 2's **Private IPv4 address.**
    

> 💡  **Why do we pick the Private IPv4 address? Why not the public address?**  
> This step is all about testing the peering connection between our EC2 instances.
> 
> If the peering connection is succesful, our instances can communicate using each other's  **private**  IPv4 addresses.
> 
> If they can't communicate using their private IPv4 addresses, then... we have an error!
> 
> That's why it's a good idea to test with the private IPv4 addresses - using public IPv4 addresses wouldn't give you much information about whether the peering connection was successful!

![Step 5: Copy the IP address.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.1.png)

Step 5: Copy the IP address.

  

-   Switch back to the **EC2 Instance Connect** tab.
    
-   Run `ping [the Private IPv4 address you just copied]` in the terminal.
    
    -   Your final result should look similar to something like `ping 10.0.1.227`
        
    -   Don't know where to enter this prompt? Look for the `$` sign at the bottom line of the black window, and type in your command after the $ sign.
        

> 💡 **What does ping mean?**  
> **Ping** is a network tool used to check whether your computer can communicate with another computer or device on a network.
> 
> When you "ping" a specific IP address, your server (in this case, Instance - NextWork VPC 1) sends a small packet of data to the target server (Instance - NextWork VPC 2), asking for a response. Ping will tell you whether you get a response back and how long it took to get a response.

-   You should see a response similar to this:
    

![Step 5: Your first ping response... 🙉](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.2.png)

Step 5: Your first ping response... 🙉

  

> 💡 **What does this response mean? Is it a good response?**  
> If you don't get any replies (that's our situation right now), or if the replies stop suddenly, it's usually a sign that there's a problem with the connection.  
> 
> ![](https://learn.nextwork.org/projects/static/aws-networks-monitoring/ping.png)
> 
>   
> 
> 💡 **Why is there a problem with the connection between my servers?**  
> In our last two projects, the issue was that VPC 2's network might be blocking the type of traffic used with ping i.e. ICMP (Internet Control Message Protocol) traffic.
> 
> Butttt we've made sure our security group allows inbound ICMP traffic, so what's happened here?



🔥🆙 Ready for more advanced peering work?

-   Let's do some investigating... press  **Ctrl + C**  on your keyboard to end this ping test.
    

![Step 5: Let's stop that ping test.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.3.png)

Step 5: Let's stop that ping test.

  

-   See if you can test the connection from VPC 1 to VPC 2's  **public**  IP address.
    
-   Head back to your EC2 console, and copy the  **Public IPv4 address**  of  **Instance - NextWork VPC 2.**
    

![Step 5: Copy the public IP address this time.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.4.png)

Step 5: Copy the public IP address this time.

  

-   Head back to your EC2 Instance Connect tab and run a ping test with this public IPv4 address.
    
-   Your final result should look similar to something like `ping [public IPv4 address]`
    
-   Do you get ping replies back?
    

![Step 5: Is that ping replies?! 😳](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.5.png)

Step 5: Is that ping replies?! 😳

  

> **💡 I do get ping replies! What does this mean?**  
> Receiving ping replies from the public IPv4 address means Instance 2  _is_  correctly configured to respond to ping requests, and Instance 1  _can_  actually communicate with Instance 2 if it traffic goes across the public internet!



-   As an extension (this is optional, try this if you're up for it!):
    
    -   Open your computer's local Terminal. Search for  **Windows Terminal**  if you're using a Windows computer, or  **Terminal**  if you're using a Macbook.
        
    -   Try running the same ping command for VPC 2's public IP address from your local Terminal. Do you get ping replies back?
        

![Step 5: Is that ping replies (again)?! 🤯](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.6.png)

Step 5: Is that ping replies (again)?! 🤯

  

> **💡 I do get ping replies! What does this mean?**  
> Nice work getting replies!
> 
> This is further validation that Instance 2 is actually reachable from ICMP traffic. It also shows you just how vulnerable your EC2 instance is to external access when you allow  **all**  IP addresses to reach it!
> 
>   
> **Extra for Experts:**  Did you notice that the average time for each ping message is much longer from your local computer?  
> **time=147 ms**  i.e. 147 milliseconds or more, when the ping command is coming from your local computer.
> 
> ![Step 5: Your local computer's ping time.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.7.png)
> 
> Step 5: Your local computer's ping time.
> 
> **time=0.557 ms**  i.e. 0.5 milliseconds or more, when the ping command is coming your Instance 1.
> 
> ![Step 5: Your EC2 Instance's ping time.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.8.png)
> 
> Step 5: Your EC2 Instance's ping time.
> 
> Instance 1 is in the same Availability Zone as Instance 2, so it'll likely be physically much closer to Instance 2 than you are! That's why traffic from Instance 1 experiences much less latency.

-   Press  **Ctrl + C**  on the session running on your local terminal - we'll need this again later!
    
-   Back in your EC2 Instance Connect page, press  **Ctrl + C**  on your keyboard again to end this ping test.
    
-   Ping your EC2 Instance 2's  **private**  address again.
    

![Step 5: Ping the private address one more timeeeeeee.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.9.png)

Step 5: Ping the private address one more timeeeeeee.

  

-   Yup... still no replies with the private IP address.
    

> ⏸️ **Pause and have a think - where do you think you can investigate this?**  
> We receive ping replies when we use Instance 2's  **public**  IP address, whicih confirms that VPC 2's security groups and NACL's  _are_  letting in ICMP traffic.
> 
> But using Instance 2's  **private**  IP address doesn't give us any ping replies.
> 
> Up til now, you've learnt about internet gateways, subnets, route tables, IPv4 addressing, security groups, route tables, and peering connections...
> 
> Which of these would you need to configure to solve this connectivity issue?  
> Hmmm!  
> 🤔  
> 🤔  
> 🤔
> 
> Challenge yourself - can you solve this now without any guidance? Feel free to skip the remaining instructions in this step this try this on your own.
> 
> Orrrr if you'd prefer, let's do this step by step together with the instructions below 👇

▶️ Alright, resuming now - here are the specific steps!

-   Leave open the **EC2 Instance Connect** tab, but head back to your **VPC** console in a new tab.
    
-   In the VPC console, select the **Subnets** page.
    
-   Select VPC 1's subnet i.e.  **NextWork-1-subnet-public1-...**
    
-   Let's investigate the **Route tables** and **Network ACL** tabs for your subnet.
    
-   The network ACL allows all types of inbound traffic from anywhere! So this looks perfectly fine.
    
-   But let's take a closer look at the route tables...
    
-   Aha! Mystery solved.
    

![Step 5: Your subnet's route table.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.10.png)

Step 5: Your subnet's route table.

  

> **💡 Hmmmmm, what's the issue with this route table?**  
> We'll ask you a question back this time (surprise!) - where is the direct route to VPC 2 from VPC 1? Can you find it in this route table?
> 
> Nope! The missing ingredient in our architecture is the  **VPC peering connection**  that directly connects VPCs 1 and 2.
> 
>   
> **💡 But there's a route to 0.0.0.0/0 in the route table! Doesn't that get traffic anywhere, including Instance 2?**  
> Good question! The answer lies in the purpose of a peering connection - why do we set one up?  
>   
> The purpose of a peering connection is to create a  **direct**  link between two resources so they can communicate with their private IP addresses.  
>   
> You'd be correct to say that Instance 1 and Instance 2 are currently connected through the route with a destination of 0.0.0.0/0, but that traffic is is through the internet gateway i.e. traffic will travel through and be exposed to the public internet.  
>   
> To make sure communication between Instances 1 and 2 is direct, we need to set up a new route that directs traffic to our peering connection (instead of the public internet).



Let's fix this by setting up our VPC peering connection.

### 🌉 Step #6

### Create a Peering Connection and Configure Route Tables

  

Aha, so we have a missing link that's causing this connectivity error... did you catch it ahead of time that our network doesn't have a peering connection?

Let's add that peering connection in this step to bridge our VPCs together! 🌉

  
  

**In this step, you're going to:**

1.  Set up a connection link between your VPCs.
    

![Step 6: Let's set up a peering connection.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step6.0.png)

Step 6: Let's set up a peering connection.

  



-   Head to the VPC console, click on **Peering connections**  on the left hand navigation panel.
    

> 💡 **What is a peering connection?**  
> A VPC peering connection is a direct connection between two VPCs!  
> A peering connection lets VPCs and their resources route traffic between them using their  **private**  IP addresses. This means data can now be transferred between VPCs without going through the public internet.
> 
> Without a peering connection, data transfers between VPCs would use resources' public address - meaning VPCs have to communicate over the public internet!
> 
> ![](https://learn.nextwork.org/projects/static/aws-networks-monitoring/without-peering.png)
> 
>   

![Step 6: Select Peering connections.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step7.1.png)

Step 6: Select Peering connections.

  

-   Click on **Create peering connection** in the right hand corner.
    

![Step 6: Select Create peering connection.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step7.2.png)

Step 6: Select Create peering connection.

  

-   Name your  **Peering connection name**  as `VPC 1 <> VPC 2`
    
-   Select **NextWork-1-VPC**  for your  **VPC ID (Requester).**
    

> 💡 **What does Requester mean?**  
> In VPC peering, the  **Requester**  is the VPC that initiates a peering connection. As the requester, they will be sending the other VPC an  **invitation**  to connect!

![Step 6: Set the Requester.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step7.3.png)

Step 6: Set the Requester.

  

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

![Step 6: Set the Accepter.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step7.4.png)

Step 6: Set the Accepter.

  

-   Click on **Create peering connection.**
    
-   Your newly created peering connection isn't finished yet! The green success bar says the peering connection  **has been requested.**
    

![Step 6: A peering connection is requested.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step7.5.png)

Step 6: A peering connection is requested.

  

-   On the next screen, select **Actions** and then select **Accept request...**  Get ready to take a screenshot!
    

> 💡 **Why did I have to accept a request?**  
> You set up the VPC peering connection as VPC 1 (the Requestor), but don't forget that the Accepter needs to approve of it too!
> 
> By clicking  **Accept request,**  you were accepting the connection as VPC 2.

![Step 6: Select Accept request here.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step7.6.png)

Step 6: Select Accept request here.

  

-   Click on  **Accept request**  again on the pop up panel.
    
-   Click on **Modify my route tables now** on the top right corner.
    

A peering connection is all set now (nice work!) ✅

**Update VPC 1's route table**

-   Select the checkbox next to VPC 1's route table i.e. called  **NextWork-1-rtb-public.**
    
-   Scroll down and click on the **Routes** tab.
    
-   Click **Edit routes.**
    
-   Let's add a new route!
    

> 💡 **Why do I need to add a new route?**  
> Even if your peering connection has been accepted, traffic in VPC 1 won't know how to get to resources in VPC 2 without a route in your route table! You need to set up a route that directs traffic bound for VPC 2 to the peering connection you've set up.

-   Add a new route to  **VPC 2**  by entering the CIDR block `10.2.0.0/16` as our  **Destination**.
    
-   Under Target, select  **Peering Connection.**
    
-   Select  **VPC 1 <> VPC 2**.
    

![Step 6: Select your peering connection.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step8.1.png)

Step 6: Select your peering connection.

  

-   Click **Save changes.**
    
-   Confirm that the new route appears in VPC 1's **Routes** tab!
    

![Step 6: Do you see a new route in VPC 1's route table?](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step8.2.png)

Step 6: Do you see a new route in VPC 1's route table?

  

**Update VPC 2's route table**

Challenge yourself - do you think you can set up the equivalent route in VPC 2's route table?

If you get stuck, use the same instructions above but make sure:

1.  The route table you're updating is  **NextWork-2-rtb-public.**
    
2.  The  **Destination**  is the CIDR block `10.1.0.0/16`
    
3.  You save your changes!
    

![Step 6: Your updated route table looking fresh ✨](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step8.3.png)

Step 6: Your updated route table looking fresh ✨

  



-   Revisit the **EC2 Instance Connect** tab that's connected to NextWork Public Server.
    
-   Woah! Lots of new lines coming through in the terminal.
    

![Step 6: YAYYYY those are ping replies!! 🎉](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step8.4.png)

Step 6: YAYYYY those are ping replies!! 🎉

  

> **💡 Ooops... I've accidentally quit this command. I don't see any new lines.**  
>   
> 
> No worries! Handy hint: use the  **up arrow**  on your keyboard (i.e. the key that looks like ▲) and you'll see your latest command automatically pre-filled in the terminal!

**Congratulations!!!** You've successfully resolved the connectivity issue by setting up a peering architecture between VPC 1 and VPC 2!



-   As an extension (this is optional!), validate this by trying to run the same  **ping command**  from your  **local terminal.**
    
-   Do you get ping replies here too?
    

![Step 6 Extension: Does your local terminal get replies too?](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step8.5.png)

Step 6 Extension: Does your local terminal get replies too?

  

> **💡 I get request timeout... what does that mean?**  
> A request timeout typically means that the ping request was sent, but there was no reply within the expected time frame.
> 
> Perfect! This is validation that our peering connection is truly only letting Instance 1 get direct access to Instance 2 through private addresses.

-   You can quit your local terminal's session now! Validating DONE 🙂
    
-   Another optional extension! Back in your EC2 Instance Connect tab, run the same ping command but add  `-c 5`  to the end of the command.
    
-   Your final result should look like  `ping 10.2.15.210 -c 5`
    

![Step 6 Extension: Adding -c 5 limits the number of packages.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step8.6.png)

Step 6 Extension: Adding -c 5 limits the number of packages.

  

-   Ooo nice! The ping test automatically finishes after 5 packets have been sent.
    

> **💡 So what does -c 5 mean in a ping command?**  
> The  `-c 5`  option in a ping command tells the system to send exactly 5 ping packets to the target IP address. A great option to limit the number of ping attempts if you want to analyze connectivity with a consistent number of tests!

🧠 Step 7#

### Analyze Flow Logs

  

To wrap things up, let's check out what VPC Flow Logs has recorded about your network's activity!

It's monitoring time 😎📊

  
  

**In this step, you're going to:**

1.  Review the flow logs recorded aboout VPC 1's public subnet.
    
2.  Analyse the flow logs to get some tasty insights 👀
    



-   Head to your  **CloudWatch**  console.
    
-   Select  **Log groups**  from the left hand navigation panel.
    
-   Click into  **NextWorkVPCFlowLogsGroup.**
    
-   Click into your log stream to see flow logs from EC2 Instance 1!
    

![Step 7: Your log group has a single stream.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step9.1.png)

Step 7: Your log group has a single stream.

  

> **💡 Why is my log stream**  **_named_**  **eni-xxx?**  
> Log streams in CloudWatch are often named after the network interface ID (`eni-xxx`) when they're associated with VPC flow logs. This helps you organise which streams are tracking traffic to which resources in your VPC.  
>   
> **Tip:**  `eni`  = Elastic Network Interface (ENI)! If you ever wonder how an EC2 instance can have a public/private IP address, security group rules and the option connect to other services in your AWS environment, the ENI is the answer.  
>   
> Think of ENI as a cloud networking component that attaches to an EC2 instance and gives the EC2 instance networking capabilities. Every EC2 instance  **must**  have an ENI to exist and be in a VPC.

-   Oooo check out these  **log events!**
    

![Step 7: Log events about VPC 1's network traffic.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step9.2.png)

Step 7: Log events about VPC 1's network traffic.

  

-   Scroll to the very top and try expanding a log at the top - woahhh, welcome to this flow log.
    

![Step 7: Expand one of your flow logs.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step9.3.png)

Step 7: Expand one of your flow logs.

  

> **💡 What is this flow log saying?**  
> Let's break it down!
> 
> ![Notes on your flow log ✍️](https://learn.nextwork.org/projects/static/aws-networks-monitoring/flowlog-annotated.png)
> 
> Notes on your flow log ✍️
> 
> This flow log shows that  **344**  bytes of data were sent successfully from the IP address  **18.237.140.165**  to  **10.1.5.112**  using TCP protocol on port  **22**, with  **4**  packets transferred and the traffic was allowed (**"ACCEPT"**).
> 
> **Extra for Experts:**  EC2 Instance Connect's IP address range in the Oregon region is 18.237.140.160/29, which means the source of traffic mentioned in this log is actually EC2 Instance Connect's direct access to Instance 1!

-   Now scroll to the very bottom and select one of the newer logs, are there any differences?
    
-   For example, you might find one that says  **REJECT OK**  instead of  **ACCEPT OK**  at the end. These would represent the ping messages that failed to reach Instance 2!
    

![Step 7: Another flow log that says REJECT.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step9.4.png)

Step 7: Another flow log that says REJECT.

  



-   In the left hand navigation panel, click on **Logs Insights.**
    

![Step 7: Select Logs Insights.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step9.6.png)

Step 7: Select Logs Insights.

  

> 💡  **What are Logs Insights?**  
> **Logs Insights**  is a CloudWatch feature that analyzes your logs. In Log Insights, you use queries to filter, process and combine data to help you troubleshoot problems or better understand your network traffic!

-   Select **NextWorkVPCFlowLogsGroup** from the **Select log group(s)** dropdown.
    
-   Select the **Queries** folder on the right hand side.
    

> 💡  **What are queries?**  
> Queries are like commands you run to analyze your logs! You can use queries to filter logs, group data, and perform calculations like sums and averages.
> 
> You use queries to extract specific information from large volumes of log data, making it easier to see trends, identify outliers, and troubleshoot issues. For example, if you're managing a network and traffic suddenly slows down, you could use queries to extract logs on the longest wait times in your network.
> 
> _p.s._  if you've ever used a spreadsheet or tried our QuickSight project, queries are like the command/code version of buttons you use to filter your data!

![Step 7: Select the Queries icon.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step9.7.png)

Step 7: Select the Queries icon.

  

-   Under  **Flow Logs**, select **Top 10 byte transfers by source and destination IP addresses**.
    

> 💡  **What does this query mean?**  
> The query  **"Top 10 byte transfers by source and destination IP addresses"**  is all about discovering the top 10 biggest data transfers between IP addresses in your network! You'll find out which resources are moving the most data, which uncovers the busiest traffic routes in your network.

![Step 7: Select the Top 10 byte transfers query.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step9.10.png)

Step 7: Select the Top 10 byte transfers query.

  

-   Click **Apply,** and then **Run query.**
    

![Step 7: Run your query!](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step9.11.png)

Step 7: Run your query!

  

-   Review the query results... wow!
    

![Step 7: Your query results.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step9.12.png)

Step 7: Your query results.

  

> 💡  **What are these results telling me?**  
> Wow! Out of all the logs that Flow Logs has captured, here are the ten pairs of source and destination IP addresses that transferred the most data between them.
> 
> So as you might imagine, this is a great query for investigating any heavy traffic flows or unusual data transfers!
> 
> p.s. the bar chart at the top is just a little visualization to show you how many logs were captured at specific times of the day. The table below are the actual results of your query.

-   **Extra for Experts:**  Can you map the logs with IP addresses you've come across during this project?
    

![Step 7: Try matching these results with your instances' IPv4 addresses!](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step9.13.png)

Step 7: Try matching these results with your instances' IPv4 addresses!

  



😮‍💨 All Done

### Nice work!

  

You've just completed today's project and  **learnt how to monitor traffic within your VPC.**

------------------------
  
🗑️ Before You Go

### Delete Your Resources

  

✋  **STOP**

Before diving into the steps for deleting your resources, why not challenge yourself to delete everything in this project on your own?

Keeping track of your resources, and deleting them at the end, is absolutely a skill that will help you reduce waste in your account.

  
  

🛑  **STEPS BELOW:**

  
  

**Delete your CloudWatch Log Group**

-   In your CloudWatch console, select  **Log groups**  from the left hand navigation panel.
    
-   Select your  **NextWorkVPCFlowLogsGroup.**
    
-   Click the **Actions** button, and select **Delete log group(s)**.
    
-   Confirm by pressing the **Delete** button.
    

![Step 11: Delete your CloudWatch log group.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step11.1.png)

Step 11: Delete your CloudWatch log group.

  

  
  

**Delete your EC2 Instances**

-   Head back to the  **Instances**  page of your EC2 console.
    
-   Select the checkboxes next to  **Instance - NextWork VPC 1**  and  **Instance - NextWork VPC 2.**
    
-   Select  **Instance state,**  then select  **Terminate Instance.**
    
-   Select  **Terminate**.
    

![Step 11: Delete your EC2 instances.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step11.2.png)

Step 11: Delete your EC2 instances.

  

  
  

**Delete VPC Peering Connections**

-   Head back to your  **VPC**  console.
    
-   Select  **Peering connections**  from your left hand navigation panel.
    
-   Select the `VPC 1 <> VPC 2` peering connection.
    
-   Select  **Actions**, then **Delete peering connection.**
    
-   Select the checkbox to **Delete related route table entries**.
    
-   Type `delete` in the text box and click **Delete.**
    

![Step 11: Delete your VPC peering connection.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step11.4.png)

Step 11: Delete your VPC peering connection.

  

  
  

**Delete your VPCs**

-   Select  **Your VPCs**  from your left hand navigation panel.
    
-   Select  **NextWork-1-vpc,**  then  **Actions**, and  **Delete VPC.**
    
-   Type `delete` in the text box and click **Delete.**
    
-   Note: if you get stopped from deleting your VPC because  **network interfaces**  are still attached to your VPC - delete all the attached network interfaces first!
    

> 💡  **What is a network interface?**  
> Network interfaces get created automatically when you launch an EC2 instance. Think of them as a component that attaches to an EC2 instance on one end and your VPC on another - so that your EC2 instance is connected to your network and can send and receive data! Network interfaces are usually deleted automatically with your EC2 instance, but on some occassions it'd be faster to delete them manually.

-   Select  **NextWork-2-vpc,**  then  **Actions**, and  **Delete VPC.**
    
-   Type `delete` in the text box and click **Delete.**
    

  
  
  

Other network components should be automatically deleted with your VPC, but it's always a good idea to check anyway.

Don't forget to  **refresh**  each page before checking if these resources are still in your account:

1.  Subnets
    
2.  Route tables
    
3.  Internet gateways
    
4.  Network ACLs
    
5.  Security groups
    

  
  

One last thing...

Can you remember one last resource that we created in this project?

  
  
  

**Delete your CloudWatch IAM Role and Policy**

-   Head to your  **IAM**  console.
    
-   Select  **Policies**  from the left hand navigation panel.
    
-   Search for  `FlowLogs`, and select  **NextWorkVPCFlowLogsPolicy.**
    
-   Select  **Delete**, then enter  `NextWorkVPCFlowLogsPolicy`  to confirm your deletion.
    
-   Select  **Roles**  from the left hand navigation panel.
    
-   Search for  `FlowLogs`, and select  **NextWorkVPCFlowLogsRole.**
    
-   Select  **Delete**, then enter  `NextWorkVPCFlowLogsRole`  to confirm your deletion.
    

![Step 11: Delete your CloudWatch IAM Role and Policy.](https://learn.nextwork.org/projects/static/aws-networks-monitoring/high-step11.6.png)

Step 11: Delete your CloudWatch IAM Role and Policy.


Nice Work!

THAT'S NETWORKING PROJECT SEVEN...

DONE!!!!! 🥳

**Today you've learnt how to:**

-   ☁️ **Create two VPCs with public subnets and a peering connection:** You set up two VPCs, each with a public subnet, and resolved connectivity issues using a peering connection between them. You've also run ping tests on public IPv4 addresses!  
      
    
-   🛶 **Set up VPC Flow Logs:** You configured VPC Flow Logs to monitor network traffic, sending all logs directly to a CloudWatch log group for easy access and analysis.  
      
    
-   🧠 **Analyze network traffic with Log Insights:** You dove into CloudWatch Logs Insights to query and analyze your network traffic. This deep dive helped you understand traffic flows and pinpoint any issues or unusual patterns.


### 👏 All done!


Content Credits : **Nextwork**