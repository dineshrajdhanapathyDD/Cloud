# VPC Endpoints

Connect your VPC to other AWS services directly, no internet needed!


WHAT YOU'LL NEED

-   An AWS account -  [Create one here!](https://github.com/dineshrajdhanapathyDD/Cloud/blob/main/AWS/NextWork%20AWS%20Documentation/5%20AWS%20BASIC/legendary-aws-account-setup.pdf))

-   Part 1 of this series -  [Build a Virtual Private Cloud](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%201%20Build%20a%20Virtual%20Private%20Cloud)
-   Part 2 of this series -  [VPC Traffic Flow and Security](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%202%20VPC%20Traffic%20Flow%20and%20Security)

-   Part 3 of this series -  [Creating a Private Subnet](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%203%20Creating%20a%20Private%20Subnet%20in%20Your%20Amazon%20VPC)

-   Part 4 of this series -  [Launching VPC Resources](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%204%20Launching%20VPC%20Resources)

-   Part 5 of this series -  [Testing VPC Connectivity](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%205%20Testing%20VPC%20Connectivity)

-   Part 6 of this series -  [VPC Peering](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%206%20VPC%20Peering)
-   Part 7 of this series -  [Access S3 from a VPC](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%207%20VPC%20Monitoring)
-   Part 8 of this series -  [Access S3 from a VPC](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%208%20Access%20S3%20from%20a%20VPC)



## ⚡️ 30 second Summary

Welcome to your 🏁  **FINAL**  🏁 AWS networking project!

In this last project, you learnt how to use your VPC to  **access other AWS services,**  specifically S3.

That was pretty cool - with direct access to your EC2 instance, you could use AWS CLI commands to see what objects are in your S3 bucket and even upload files!

![You learnt how to access an S3 bucket from an EC2 instance in your VPC.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/architecture-past.png)

You learnt how to access an S3 bucket from an EC2 instance in your VPC.

  

Buttt there's just one thing... with this setup, your EC2 instance is accessing your S3 bucket through the  **public internet.**

  
  

**🤔 How is that a problem?**  
When traffic is going through the internet, there is a higher risk of external threats and attacks looking at your data!

For example, attackers can expose your EC2 instance's keys to your AWS account if they manage to break into the traffic between your instance and S3 bucket. Yikes, that's not great for security!

  
  

**😰 But we need resources to talk to each other to build things on AWS!**

You're right, so how could we solve this problem and let our VPC communicate with other AWS services in a safer way?

  
  

🥁 Introducing...  **VPC endpoints!**

VPC endpoints gives your VPC  **private, direct access to other AWS services like S3**, so traffic doesn't need to go through the internet.

Just like how internet gateways are like your VPC's door to the internet, you can think of VPC endpoints as  **private doors to specific AWS services.**

  
  

**Get ready to:**

1.  🚪 Use VPC endpoints to directly access your S3 bucket from your VPC.
    
2.  🔐 Test your endpoint setup using an S3 security tool called bucket policies!
    

![You're at the final level of this series! Here's today's game plan.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/architecture-today.png)

You're at the final level of this series! Here's today's game plan

If you haven't done the previous project in our networking series, **Access S3 from a VPC**, we'd highly recommend doing that first. This project starts right where the previous one leaves off.


  
### ☁️ Step #1

### Set up your Architecture

  

LET's GOOOOOO!! Set up the foundations of today's project - a VPC, EC2 instance and S3 bucket are coming right up.

  
  

**In this step, you're going to:**

1.  Create a VPC from scratch!
    
2.  Launch an EC2 instance, which you'll connect to using EC2 Instance Connect later.
    
3.  Set up an S3 bucket.
    

![Step 1: Off we gooooooooo!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step1.0.png)

Step 1: Off we gooooooooo!

  



-   [Log in to your AWS Account.](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26state%3DhashArgsFromTB_ap-southeast-2_fffdf5be4bb1a27e&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=m-aiqeB2UZeXTGXNyugMP8L64zd_AGUxJl4HLnA-X1o&code_challenge_method=SHA-256)
    

  
  
  

**☁️ Create Your VPC**

Starting off STRONG with your VPC - let's set it up in just two minutes ⚡️

![Step 1: Create a VPC from scratch!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step1.0.vpc.png)

Step 1: Create a VPC from scratch!

  

-   Head to your **VPC** console - search for  `VPC`  at the search bar at top of your page.
    
-   From the left hand navigation bar, select **Your VPCs.**
    
-   Select **Create VPC.**
    
-   Select **VPC and more.**
    
-   Under **Name tag auto-generation**, enter `NextWork`
    
-   The VPC's **IPv4 CIDR block** is already pre-filled to `10.0.0.0/16`  - we'll use this default CIDR block!
    

![Step 1: Your VPC's settings.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step1.1.png)

Step 1: Your VPC's settings.

  

-   For **IPv6 CIDR block**, we'll leave in the default option of **No IPv6 CIDR block.**
    
-   For **Tenancy**, we'll keep the selection of **Default.**
    
-   For **Number of Availability Zones (AZs)**, we'll use just **1** Availability Zone.
    
-   Make sure the **Number of public subnets** chosen is **1**.
    
-   For **Number of private subnets,** we'll keep thing simple today and go with  **0**  private subnets.
    
-   For the **NAT gateways ($)** option, make sure you've selected **None.** As the dollar sign suggests, NAT gateways cost money!
    
-   For the **VPC endpoints** option, select **None.**
    

> 💡 **What are VPC endpoints?**  
> Ooo, the main character of today's project!
> 
> Normally, to access some AWS services like S3 from your VPC, your traffic would go out to the public internet.
> 
> But, VPC endpoints let you connect your VPC privately to AWS services without using the public internet. This means your data stays within the AWS network, which can improve security and reduce data transfer costs.
> 
> We're selecting None here, so we can learn to set one up manually later! 👀

-   You can leave the **DNS options** checked.
    

![Step 1: Your VPC's settings.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step1.2.png)

Step 1: Your VPC's settings.

  

-   Select **Create VPC.**  
      
    

  
  
  

**💻 Launch an instance in your VPC**

Wooohooo, now it's time to launch an EC2 instance into your architecture!

![Step 1: Launch an EC2 instance.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step1.0.ec2.png)

Step 1: Launch an EC2 instance.

  

-   Head to the **EC2 console** - search for `EC2` in the search bar at the top of screen.
    
-   Select **Instances** at the left hand navigation bar.
    
-   Select **Launch instances**.
    
-   Since your first EC2 instance will be launched in your first VPC, let's name it `Instance - NextWork VPC Endpoints`
    

![Step 1: Name your new instance.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step1.3.png)

Step 1: Name your new instance.

  

-   For the **Amazon Machine Image,** select **Amazon Linux 2023 AMI.**
    
-   For the **Instance type,** select **t2.micro.**
    
-   For the **Key pair (login)** panel, select **Proceed without a key pair (not recommended).**
    
-   At the **Network settings** panel, select **Edit** at the right hand corner.
    
-   Under  **VPC**, select **NextWork-vpc**.
    
-   Under  **Subnet,**  select your VPC's public subnet.
    
-   Keep the **Auto-assign public IP** setting to... do you remember whether our EC2 instance needs a public IP address?
    

> 💡 **Hmmm, I can't seem to remember. What is it?**  
> We're using EC2 Instance Connect after this to connect with our EC2 instance!
> 
> EC2 Instance Connect requires instances to be in a public subnet AND  **have a public IPv4 address!**
> 
>   
> 💡  **What is EC2 Instance Connect?**  
> EC2 Instance Connect is an EC2 service designed to help you get direct access to your EC2 instance!
> 
> Once you get direct access to your EC2 instance, you're going into the instance's terminal. This lets you do some advanced work like installing software into your EC2 instance or accessing another AWS service!

-   Select  **Enable.**
    

![Step 1: Your instance's network settings.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step1.4.png)

Step 1: Your instance's network settings.

  

-   For the **Firewall (security groups)** setting, choose **Create security group.**
    
-   Name your security group  `SG - NextWork VPC Endpoints`
    
-   That's it! No security group rules to add.
    

> 💡  **Didn't we use to add other security group rules?**  
> By default, this new security group allows all inbound SSH traffic. That's all we need to use EC2 Instance Connect later.
> 
> We used to add an inbound rule to allow ICMP traffic - but we won't need it if we aren't running any ping tests!

![Step 1: Your new security group settings.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step1.5.png)

Step 1: Your new security group settings.

  

-   Select  **Launch instance.**
    



**🪣 Launch a bucket in Amazon S3**

Before we connect with our EC2 instance, let's set up a bucket in Amazon S3 🪄

After creating this bucket, we'll access it from our EC2 instance and do things like checking what objects are in the bucket.

![Step 1: Launch an S3 bucket.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step1.0.s3.png)

Step 1: Launch an S3 bucket.

  

-   Search for  **S3**  at the search bar at the top of your console.
    

![Step 1: Search for S3 at the search bar up top.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step4.1.png)

Step 1: Search for S3 at the search bar up top.

  

-   Make sure you're in the same Region as your NextWork VPC!
    
-   Select  **Create bucket.**
    

![Step 1: Select Create bucket - here we goooo.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step4.2.png)

Step 1: Select Create bucket - here we goooo.

  

-   Let's set up your bucket! Keep the  **Bucket type**  as  **General purpose.**
    
-   Your  **bucket name**  should be  `nextwork-vpc-endpoints-yourname`
    
    -   Don't forget to replace  **yourname**  with your first name! S3 bucket names need to be globally unique.
        
-   We'll leave all other default settings, go straight to  **Create bucket.**
    

  
  

Nice! Bucket created 😎 😎

![Step 1: Bucket created! That was fast.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step4.3.png)

Step 1: Bucket created! That was fast.

  

We'll finish set up by uploading two files into your shiny new bucket.

This can be  **any**  two files in your local computer!

-   Click into your bucket.
    
-   Select  **Upload**.
    

![Step 1: Select Upload.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step4.4.png)

Step 1: Select Upload.

  

-   Select  **Add files**  in the  **Files and folders panel.**
    

![Step 1: Select Add files.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step4.5.png)

Step 1: Select Add files.

  

-   Select two files in your local computer to upload.
    

  
  
  

Not sure what to upload? You can download and use these images instead! 👇

**Right click**  on each link, select  **Save link as...**  and select  **Save.**

-   [NextWork - Denzel is awesome.png](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20VPC%20Endpoints/NextWork%20-%20Denzel%20is%20awesome.png)
    
-   [NextWork - Lelo is awesome.png](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20VPC%20Endpoints/NextWork%20-%20Lelo%20is%20awesome.png)
    

  
  
  

Your files should show up in your  **Files and folders**  panel once they're uploaded!

![Step 1: What Files and folders will look like after uploading.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step4.6.png)

Step 1: What Files and folders will look like after uploading.

  

-   Select  **Upload**  at the bottom of the page.
    





### 💻 Step #2

### Connect to Your EC2 Instance

  

This project is all about VPC endpoint connections, so before we create that endpoint... let's see what things are like  **without**  endpoint connections in place.

In this step, we're gonna connect to your EC2 instance and try access S3 through the  **public internet!**

  
  

**In this step, you're going to:**

1.  Connect directly to your EC2 instance.
    

![Step 2: Connect to your EC2 instance](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step2.0.png)

Step 2: Connect to your EC2 instance

  



-   Head to your  **EC2** console and the  **Instances**  page.
    
-   Select the checkbox next to  **Instance - NextWork VPC 1.**
    
-   Select **Connect**.
    
-   In the EC2 Instance Connect set up page, select  **Connect**  again.
    
-   Yay! Successfully connected.
    

![Step 2: Feels good that we've connected right away!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step2.1.png)

Step 2: Feels good that we've connected right away!

  

-   For your first command, try running  `aws s3 ls`, which is a command used to list the S3 buckets in your account (yup,  **ls**  stands for list!).
    

> 💡  **Wait, you can view S3 buckets from an instance's terminal?!**  
> Yes, you can! From an EC2 instance's terminal, you can run all kinds of commands to interact with AWS services. Listing all the S3 buckets you have access to is just the tip of the iceberg!
> 
>   
> **💡 How does that work?**  
> There is a special software called the  **AWS CLI (Command Line Interface)**  that you install and run on your computer to control AWS services directly from the command line i.e. your terminal! You can install this in your local computer too, and all EC2 instances come with it already installed.
> 
>   
> **Extra for Experts:**  As you advance in your cloud engineering career, you'll find that the AWS CLI often becomes your go-to tool. Engineers use the CLI to automate tasks and manage AWS resources efficiently using scripts, making it essential for managing your cloud environment in an efficient way.
> 
> While the AWS Management Console is fantastic for learning and having a visual guide, the CLI provides the speed and versatility that professionals need for complex tasks.

![Step 2: Run `aws s3 ls`](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step2.2.png)

Step 2: Run `aws s3 ls`

  


-   Hmmm, doesn't look like a success. We need to provide credentials.
    

> 💡 **What are credentials?**  
> **Credentials**  in AWS are like keys that let you access and manage AWS services securely. Without credentials, you won't have the permission to do things like viewing your S3 bucket list.
> 
>   
> **💡 Do I have credentials?**  
> When you log into your AWS Management Console, you're already authenticated using your AWS user's details.
> 
> Running commands from an EC2 instance is a different story! You can think of your EC2 instance as another user that needs its own username and password (i.e. credentials) to get access to your AWS account.
> 
> Your account by default  **doesn't**  have credentials set up for running commands from an EC2 instance. You'll need to manually set these up to securely access and manage AWS services from your instance.

-   Run  `aws configure`
    
-   The terminal is now asking us for an Access Key ID!
    

![Step 2: Run `aws configure`](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step2.3.png)

Step 2: Run `aws configure`

  

> 💡 **What is an access key ID? Do I have one?**  
> An access key ID is a part of a credential!
> 
> Your credentials are made up of a username and password; think of the access key ID as the username.
> 
> You don't automatically have one, but you can create access keys IDs through AWS IAM.
> 
>   
> 💡 **What's the difference between access keys and key pairs?**  
> You might remember key pairs from launching EC2 instances!
> 
> -   **Key pairs**  are used specifically for logging into your EC2 instances through SSH.
>     
> -   **Access keys**, which are what we're learning about now, are credentials for your applications and other servers to log into AWS and talk to your AWS services/resources.
>     



### 🔑 Step #3

### Create Access Keys

  

Challenge accepted! Your EC2 instance needs credentials to access your AWS services, so let's set up access keys right away 🏃‍♀️

  
  

**In this step, you're going to:**

1.  Give your EC2 instance access to your AWS environment.
    

![Step 3: Create access keys.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step3.0.png)

Step 3: Create access keys.

  



-   Search for  `Access keys`  in the search bar.
    
-   Aha! So it's the IAM console that helps us set this up. Select  **IAM.**
    

![Step 3: Head to the IAM console.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step3.1.png)

Step 3: Head to the IAM console.

  

-   Search for  `Access keys`  again in the IAM console's left hand navigation panel.
    

![Step 3: Search for `Access keys` one more time.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step3.2.png)

Step 3: Search for `Access keys` one more time.

  

-   Choose the search result for managing an access key for your IAM Admin account.
    

![Step 3: Choose the search result that mentions your IAM user name.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step3.3.png)

Step 3: Choose the search result that mentions your IAM user name.

  

-   On the first set up page, select  **Command Line Interface (CLI).**
    
-   Select the checkbox that says  **I understand the above recommendation and want to proceed to create an access key.**
    
-   Select  **Create access key.**
    

![Step 3: Set up your access key.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step3.4.png)

Step 3: Set up your access key.

  



> 💡 **What is the yellow warning banner saying?**  
> In this project we're creating access keys and manually applying them in our EC2 instance, but typically the recommended way is to create an  **IAM role**  with the necessary permissions and then  **attaching**  that role to your EC2 instance.
> 
> Your EC2 instance would inherit the permissions from the role, and this is best practice as you can easily attach and detach EC2 instances from roles to give and take away their credentials.
> 
> We aren't using this method so that we can learn about access keys, but roles are usually a better alternative for security.
> 
>   
> 💡 **Extra for Experts: What do the other options mean?**  
> Let's break 'em down!
> 
> -   Choose  **Local code**  if you're building an application in your local computer, and need the access key to connect your app with AWS services.
>     
> -   Choose  **Application running on an AWS compute service**  if you're building an application that's running on an AWS compute service like EC2 or Lambda, and need the access key to connect your app with AWS services.
>     
> -   Choose  **Third-party service**  if you're running an application from an external company (i.e. it wasn't built by yourself or AWS), but requires access to your AWS environment. For example, Crowdstrike is a third party security service that requires access to your AWS environment to protect them in real time!
>     
> -   Choose  **Application running outside AWS**  if you're running an application built by yourself but hosted on a physical server or another cloud platform, and you need to integrate it with AWS services.
>     

-   Select  **Next.**
    
-   For the  **Description tag value,**  we'll write  `Access key created to access an S3 bucket from an EC2 Instance. NextWork VPC Endpoints project.`
    

![Step 3: Give your access key a description.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step3.5.png)

Step 3: Give your access key a description.

  

-   Select  **Create access key.**
    
-   OOoo this is important!  **STAY ON THIS PAGE ✋**
    

![Step 3: Stay on this page!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step3.6.png)

Step 3: Stay on this page!

  

You've just created your access key, well done.

This is the only time that your secret access key can be viewed or downloaded. You cannot recover it later. However, you can create a new access key any time.

> 💡 **What is the secret access key?**  
> The secret access key is like the password that pairs with your access key ID (your username). You need both to access AWS services.
> 
> Secret is a key word here - anyone who has it can access your AWS account, so we need to keep this away from anyone else!

-   Select  **Download .csv file**  near the bottom of the page.
    

> 🚨 PLEASE don't forget to  **delete your access key and the .csv file**  at the END of your session!
> 
> If you don't finish this project today, it's better to delete your access key and create a new one tomorrow, than to keep the same access key for a longer period of time.


### 🔌 Step #4

### Connect to your S3 bucket

  

Access keys created 💻 🔑 ☁️

Shall we try use our EC2 instance to access your S3 bucket now? (Yes!!) 👀

  
  

**In this step, you're going to:**

1.  Head back to your EC2 instance.
    
2.  Get your EC2 instance to access your S3 bucket.
    

![Step 4: Connect to your S3 bucket.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step5.0.png)

Step 4: Connect to your S3 bucket.

  



-   Now back to your  **EC2 Instance Connect**  tab!
    
-   Are you ready to enter your  **Access keys details now?**
    
-   Open the  **AccessKeys.csv**  file you've downloaded.
    
-   Copy the  **Access key ID.**
    
-   Paste this into your EC2 instance's terminal, and press  **Enter**  on your keyboard.
    

![Step 4: Enter your Access key ID.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step5.1.png)

Step 4: Enter your Access key ID.

  

-   Let's do the same for the  **AWS Secret Access Key!**
    
-   Copy the key from your .csv file, and paste it in the terminal. Press  **Enter**.
    
-   Next, for your  **Default region name,**  open your  **Region**  dropdown on the top right hand corner of your AWS console.
    
-   Copy your  **Region's code name.**  For example, us-west-2.
    

![Step 4: Copy the Region's code name.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step5.2.png)

Step 4: Copy the Region's code name.

  

-   Paste that in your EC2 instance's terminal. Press  **Enter**  on your keyboard.
    
-   We don't have a default output format, so we can leave that empty. Press  **Enter**.
    

> 💡  **What is a default output format?**  
> In just a second, you'll be running a few CLI commands in your EC2 instance's terminal to use Amazon S3. The  **default output format**  is how the results of your will display!
> 
> Options for your output format options are...
> 
> -   `json`, which is the default if you're not using another option.
>     
> -   `text`  for plain text.
>     
> -   `table`  for an formatted table.
>     
> -   `yaml`, which is a format for writing data in a way that is easy for people to read and write.
>     
> 
>   
> **💡 What is JSON?**  
> Amaaaazing question! JSON is a format for storing and exchanging data that is easy to understand for both humans and computers.
> 
> You'll get to use JSON and see it in action in a second 😎

![Step 4: Leave the default output format empty.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step5.3.png)

Step 4: Leave the default output format empty.

  

-   Nice! Set up is done.
    



-   Let's try running the  `aws s3 ls`  command again to see a list of your account's S3 buckets.
    

  
  
  

YOOOOOO look at that! Do you see a list of your buckets? You might have a shorter list than the one in this screenshot, but the only line to look out for is  **vpc-endpoints-yourname.**

![Step 4: Do you see your bucket name?](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step5.4.png)

Step 4: Do you see your bucket name?

  



-   Next, let's run the command  `aws s3 ls s3://nextwork-vpc-endpoints-yourname`. Make sure to replace  `nextwork-vpc-endpoints-yourname`  with your actual bucket name!
    
-   Based on the command, and what you've learnt about  **aws s3 ls**, can you guess what this command does?
    
-   Nice - we can even see the objects that are inside your bucket.
    

![Step 4: Oooo you can even peek at the objects inside your bucket.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step5.5.png)

Step 4: Oooo you can even peek at the objects inside your bucket.

  



Did you know you could upload files using AWS CLI too?!

-   Run  `sudo touch /tmp/nextwork.txt`  to create a blank .txt file in your EC2 instance.
    

> 💡  **What does this command say?**  
> Let's break it down!
> 
> -   **sudo**  stands for "superuser do" and it's used when you're running a command that typicaly needs elevated user permissions, like installing software or creating new files.
>     
> -   **touch**  is a standard command used to create an empty file if it doesn't exist. If it does exist, this command will update the file's timestamp (i.e. the last time it was accessed) instead.
>     
> -   **/tmp/**  is a common directory path (you can think of a directory path as layers and layers of folders) typically used for temporary files.
>     
> -   **nextwork.txt**  is the name of the empty file you're creating!
>     

-   Next, run  `aws s3 cp /tmp/nextwork.txt s3://nextwork-vpc-endpoints-yourname`  to upload that file into your bucket.
    

> 💡  **What does this command say?**  
> Let's break it down!
> 
> -   **aws s3 c:**  is the command to  **copy**  files.
>     
> -   **/tmp/nextwork.txt**  is the  **source file path.**  It's saying that the file to copy is nextwork.txt, which exists inside a folder called tmp.
>     
> -   **s3://nextwork-vpc-endpoints-yourname**  is the  **destination path**. It's saying that the file should be copied to the S3 bucket vpc-project-yourname!
>     

-   Finally, run  `aws s3 ls s3://nextwork-vpc-endpoints-yourname`  again - what objects are listed in your bucket now?
    

![Step 4: Run `aws s3 ls s3://nextwork-vpc-endpoints-yourname` again.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step5.6.png)

Step 4: Run `aws s3 ls s3://nextwork-vpc-endpoints-yourname` again.

  

> 💡  **What is the 0 next to nextwork.txt?**  
> The numbers next to each file name is the size fo that file! Since nextwork.txt is an empty file with no data, it has 0 bytes.





-   Switch tabs back to your  **S3**  console.
    
-   Refresh the  **Objects**  tab for your S3 bucket.
    
-   Do you see your new file there? 👀
    

![Step 4: New file spotted!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step5.7.png)

Step 4: New file spotted!

  

Super cool 😎 A file you've created in your EC2 instance now lives in your S3 bucket too!

### 🚪 Step #5

### Create an endpoint

  

Wooooohoo! Your EC2 instance definitely has access to your bucket - your access key worked 👏

Buttt your instance is connected to your bucket through the public internet.

This isn't the most secure way to communicate - external threats and attacks can easily intercept your commands and get access to your AWS environment or sensitive data.

🥁 Yup... it's time we bring in VPC endpoints!

  
  

**In this step, you're going to:**

1.  Set up a way for your VPC and S3 to communicate direclty.
    

![Step 5: Create an endpoint.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step6.0.png)

Step 5: Create an endpoint.

  



-   **In a new tab,**  head back to your  **VPC**  console.
    
-   Select  **Endpoints**  from the left hand navigation panel.
    

![Step 5: Select Endpoints.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step6.1.png)

Step 5: Select Endpoints.

  

-   Select  **Create endpoint.**
    

![Step 5: Select Create endpoint.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step6.2.png)

Step 5: Select Create endpoint.

  

> 💡  **What's an endpoint?**  
> Woohoo! We've been teasing about endpoints for a couple of projects, and it's great that we're finally creating one now!
> 
> An endpoint in AWS is a service that allows  **private**  connections between your VPC and other AWS services without needing the traffic to go over the internet.
> 
> 💡  **I thought all of my resources get launched inside my VPC, so how are some connections through the internet?**  
> Not all AWS resources get launched inside your VPC! While your EC2 instances live within your VPC, S3 buckets and some other AWS services exist outside your VPC because they're designed to be highly available and accessible from anywhere.
> 
> For example, the commands you're putting through AWS CLI now will be communicated to your S3 bucket through the public internet.
> 
> That's why VPC endpoints exist to create a  **private**  connection between your VPC and AWS services. Having a VPC endpoint means your instances can now access services like S3 directly without routing through the public internet, which makes sure your data stays within the AWS network for security.

-   For the  **Name tag**, let's use  `NextWork VPC Endpoint`
    
-   Keep the  **Service category**  as  **AWS services.**
    

![Step 5: Select AWS services.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step6.3.png)

Step 5: Select AWS services.

  

-   In the  **Services**  panel, search for  `S3`.
    
-   Select the filter result that just ends with  **s3.**
    

![Step 5: Be careful here! Don't pick any of the other filter results.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step6.4.png)

Step 5: Be careful here! Don't pick any of the other filter results.

  

-   Select the row with the  **Type**  set to  **Gateway**.
    

![Step 5: Select the row that has a Type set to Gateway.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step6.5.png)

Step 5: Select the row that has a Type set to Gateway.

  

> 💡  **What's does Gateway mean?**  
> A  **Gateway**  is a type of endpoint used specifically for Amazon S3 and DynamoDB (DynamoDB is an AWS database service).
> 
> Gateways work by simply adding a route to your VPC route table that directs traffic bound for S3 or DynamoDB to head straight for the Gateway instead of the internet.
> 
>   
> **Extra for Experts:**  As AWS evolved and more companies started using it for diverse and complex tasks, there was a need for more detailed control over how data moves within AWS networks. Gateway endpoints they could manage traffic but didn’t offer detailed settings - this led to AWS creating Interface endpoints, which offer more security settings.

-   Next, at the  **VPC**  panel, select  **NextWork-vpc.**
    
-   We'll leave the remaining default values and select  **Create endpoint.**
    

  
  

Nice! Endpoint created 🤩

![Step 5: Niceee, your endpoint is here!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step6.6.png)

Step 5: Niceee, your endpoint is here!

  

-   Select the checkbox next to your endpoint's name.
    

![Step 5: Your endpoint's details.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step6.7.png)

Step 5: Your endpoint's details.

  



### 🔒 Step #6

### Create a super secure bucket policy

  

Gooood work, you've just set up a VPC endpoint.

You might be wondering:  
-  _How do I know that my endpoint is truly providing direct access to S3?_  
-  _How can I confirm that my VPC isn't still communicating with S3 through the public internet?_

To answer these questions, we'll validate our endpoint connection by doing something a lil wild 🐲

We're going to block off your S3 bucket from ALL traffic... except traffic coming from the endpoint.

It's the ultimate test - if your endpoint was truly set up properly, then your EC2 instance should still be able to access S3. Otherwise, your instance's access is blocked!

  
  

**In this step, you're going to:**

1.  Limit your S3 bucket access's to only traffic from your endpoint.
    

![Step 6: Create a suuuuuuper secure bucket policy.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step7.0.png)

Step 6: Create a suuuuuuper secure bucket policy.

  



In your S3 bucket, we're going to kick things up a notch and make access super secure.

Let's say we want to make this bucket completely private to ALL access...  **except**  access through the VPC endpoint you've set up.

-   In the  **S3**  console, select  **Buckets**  from the left hand navigation panel.
    
-   Click into your bucket  **vpc-endpoints-yourname.**
    
-   Select the  **Permissions**  tab.
    

![Step 6: Select the Permissions tab.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step7.1.png)

Step 6: Select the Permissions tab.

  

-   Scroll to the  **Bucket policy**  panel, and select  **Edit**.
    

> 💡  **What's a bucket policy?**  
> A bucket policy is a type of IAM policy designed for setting access permissions to an S3 bucket. Using bucket policies, you get to decide who can access the bucket and what actions they can perform with it.

-   Add the below bucket policy to the policy editor.
    

json

Copy code

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ],
      "Condition": {
        "StringNotEquals": {
          "aws:sourceVpce": "vpce-xxxxxxx"
        }
      }
    }
  ]
}

```

> 💡  **What does this policy do?**  
> This policy  **denies**  all actions (`s3:*`) on your S3 bucket and its objects to everyone (`Principal: "*"`)... unless the access is from the VPC endpoint with the ID defined in  `aws:sourceVpce`.
> 
> In other words, only traffic coming from your VPC endpoint can get any access to your S3 bucket!

![Step 6: Your JSON policy code.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step7.2.png)

Step 6: Your JSON policy code.

  

> ⏸️ **PAUSE**  
> Before you save this policy - do you spot anything you should change?  
>   
> Read the policy code and spot whether there is anything that needs updating - there are  **two things**  you should notice.  
>   
> Hmmm!  
> 🤔  
> 🤔  
> 🤔

**▶️ Ready to find out the answer?**

![Step 6: Replace these placeholders!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step7.2.5.png)

Step 6: Replace these placeholders!

  

Don't forget to replace:

1.  BOTH instances of  **arn:aws:s3:::your-bucket-name**  with your actual bucket ARN.
    
    -   Handy tip: you can find your Bucket ARN right above the Policy window
        

![Step 6: Your bucket's ARN.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step7.3.png)

Step 6: Your bucket's ARN.

  

1.  **vpce-xxxxxxx**  with your VPC endpoint's ID.
    
    -   To find this ID, you'll have to switch back to your  **Endpoints**  tab and copy your endpoint's ID. Make sure it starts with  `vpce-`
        

![Step 6: Your VPC endpoint ID.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step7.4.png)

Step 6: Your VPC endpoint ID.

  

After replacing the default values with your resources' ARN or ID, double check that you haven't deleted the quote marks around any of your statements. Also check that you still have  `/*`  at the second Resource line!

![Step 6: Double check - are all the quote marks there?](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step7.5.png)

Step 6: Double check - are all the quote marks there?

  



-   Select  **Save changes.**
    

> 🚨  **Ran into this error?**  
> 
> ![Step 6: Ran into this error?](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step7.6.png)
> 
> Step 6: Ran into this error?
> 
> This means you haven't replaced all the placeholder values with your resources' ARN or ID yet!
> 
> If you're still stuck, take a screenshot of your bucket policy and  [**share it with the NextWork community**](https://community.nextwork.org/c/i-have-a-question/)  - we can solve this together.

Woah! Once you've saved your changes, panels have turned red all across the screen.

![Step 6: Access denied everywhereeee 🤯](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step7.7.png)

Step 6: Access denied everywhereeee 🤯

  

> 💡  **Why am I denied access?!**  
> Don't forget what your policy does 👀
> 
> Your policy denies all actions unless they come from your VPC endpoint. This means any attempt to access your bucket from other sources, including the AWS Management Console, is blocked!



☎️ Step #7

### Access your S3 bucket again!

  

Its the moment of truth!

Now that your S3 bucket's access is only limited to your endpoint, can your EC2 instance still access your bucket?

✅ If it can, you've set up your endpoint connection perfectly.

❌ If it can't, something's gone wrong with our VPC endpoint set up...

  
  

**In this step, you're going to:**

1.  Test your VPC endpoint set up.
    
2.  Troubleshoot a connectivity issue.
    

![Step 7: Access your bucket again... will it work?](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step8.0.png)

Step 7: Access your bucket again... will it work?

  



-   Head back to  **EC2 Instance Connect.**
    
-   Try running  `aws s3 ls s3://nextwork-vpc-endpoints-yourname`  again.
    
-   Ah! Access denied. It looks like the bucket policy had stopped us.
    

![Step 7: Access denied!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step8.1.png)

Step 7: Access denied!

  

> 💡  **Wait a second... why is our EC2 instance also denied access?**  
> We're supposed to get exclusive access to this S3 bucket... after all, the policy denies everyone  **except**  traffic through the endpoint!
> 
> We did set up an endpoint already between your VPC and your S3, didn't we?





-   Troubleshoot this error by heading to your VPC console.
    

> ⏸️ **Pause and have a think - where do you think you can investigate this?**  
> Up till now, you've learnt about internet gateways, subnets, route tables, IPv4 addressing and security groups...  
>   
> Which of these would you need to configure for Instance - NextWork VPC 2 to receive ICMP traffic?  
>   
> Hmmm!  
> 🤔  
> 🤔  
> 🤔

-   Select  **Subnets**  from the left hand navigation panel.
    
-   Select your public subnet, which starts with  **NextWork-subnet-public1.**
    
-   Select the  **Route table**  tab.
    
-   Aha! Mystery solved.
    

![Step 7: Your public subnet's route table.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step8.2.png)

Step 7: Your public subnet's route table.

  

> 💡  **How is it mystery solved?!**  
> We'll ask another question back to ya - using this route table, how would traffic from your EC2 instance get access to your S3 bucket?
> 
> The route table is the GPS / traffic controller directing traffic from your EC2 instances.
> 
> If your route table  **doesn't**  have a route that directs traffic bound for S3 to your VPC endpoint, traffic from your EC2 instance is actually trying to get to your S3 bucket through the public internet instead.
> 
> ![Step 7: Your endpoint grants access to the S3 bucket... but traffic is not going through it.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step8.2.5.png)
> 
> Step 7: Your endpoint grants access to the S3 bucket... but traffic is not going through it.
> 
>   

-   Let's make sure your public subnet has a route to your endpoint.
    
-   Select  **Endpoints**  from the left hand navigation panel.
    
-   Select the checkbox next to your endpoint, and select  **Route tables.**
    
-   Select  **Manage route tables.**
    

![Step 7: Select Manage route tables.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step8.3.png)

Step 7: Select Manage route tables.

  

-   Select the checkbox next to your public route table.
    
-   Select  **Modify route tables.**
    

![Step 7: Select Modify route tables.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step8.4.png)

Step 7: Select Modify route tables.

  

-   Head back to the  **Subnets**  page.
    
-   Select the refresh button next to the  **Actions**  dropdown.
    
-   Check the  **Route table**  tab for your public subnet again.
    

![Step 7: Select the Route table tab.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step8.5.png)

Step 7: Select the Route table tab.

  

Nice! there's a route to the VPC endpoint now.



### 😅 Step #8

### Access your S3 bucket (one last time)!

  

Surelyyyy our VPC endpoint set up is perfect now!

To validate your work, let's get your EC2 instance to interact with your S3 bucket one last time.

  
  

**In this step, you're going to:**

1.  Test your VPC endpoint set up (again).
    
2.  Restrict your VPC's acccess to your AWS environment.
    

![Step 8: Access your bucket one last time!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step9.0.png)

Step 8: Access your bucket one last time!

  



-   Back in your EC2 Instance Connect tab, run  `aws s3 ls s3://nextwork-vpc-endpoints-yourname`  again.
    
-   WOOOHOOOO! We're back.
    

![Step 8: Run `aws s3 ls s3://nextwork-vpc-endpoints-yourname` again.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step9.1.png)

Step 8: Run `aws s3 ls s3://nextwork-vpc-endpoints-yourname` again.

  

-   Congrats on making a successful VPC endpoint connection!
    


Did you know VPC endpoints can be configured using policies too?!

-   We'll do a simple configuration - switch to your  **Endpoints**  tab.
    
-   Select the checkbox next to your policy.
    
-   Select the  **Policy**  tab.
    
-   Ooo! By default, your VPC endpoint allows access to all AWS services.
    
-   Select  **Edit policy.**
    
-   Change the line  **"Effect": "Allow"**  to  `"Effect": "Deny"`!
    

![Step 8: Change the effect from Allow to Deny ❌](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step9.3.png)

Step 8: Change the effect from Allow to Deny ❌

  

-   Click  **Save.**
    
-   Switch back to your EC2 Instance Connect tab.
    
-   Run  `aws s3 ls s3://nextwork-vpc-endpoints-yourname`  - what do you see now?
    
-   Wow! The endpoint policy now stops us from accessing our S3 bucket.
    

![Step 8: Run `aws s3 ls s3://nextwork-vpc-endpoints-yourname` again.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step8.1.png)

Step 8: Run `aws s3 ls s3://nextwork-vpc-endpoints-yourname` again.

  

> **💡 Why would I use policies to configure a VPC endpoint?**  
> This is a great tool to quickly block off access if you suspect attackers are using your endpoint to access your resources! Instantly switch the effect to Deny, and your Gateway is closed.
> 
> You could also use VPC endpoint policies to be even more granular with the way you give away access to your AWS services. For example, you can write a policy that gives your endpoint read access only to S3 buckets, so the permission to upload objects is denied.

-   Switch tabs back to your  **Endpoints**  page.
    



-   Select  **Edit Policy.**
    
-   Change the policy back to  `"Effect": "Allow"`  **-**  this will be important when it comes to deleting your resources later!
    
-   Select  **Save changes.**
    

![Step 8: Change the effect from Deny back to Allow ✅](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step9.5.png)

Step 8: Change the effect from Deny back to Allow ✅

  

😮‍💨 All Done

### Nice work!

  
------------
You've just completed today's project and  **learnt how to set up direct, private access to S3 from your VPC.**


  
🗑️ Before You Go

### Delete Your Resources

  

✋  **STOP**

Before diving into the steps for deleting your resources, why not challenge yourself to delete everything in this project on your own?

Keeping track of your resources, and deleting them at the end, is absolutely a skill that will help you reduce waste in your account.

  
  

🛑  **STEPS BELOW:**

**🪣 Delete Your S3 Buckets**

-   Head to your  **S3**  console.
    
-   Select the  **Buckets**  page.
    
-   Select your  **nextwork-vpc-endpoints-yourname**, and select  **Delete**.
    
-   Enter your bucket name, and select  **Delete bucket**.
    
-   Oh no!
    

![Step 10: Deleting your S3 bucket from the Console.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step11.1.png)

Step 10: Deleting your S3 bucket from the Console.

  

-   Deleting your bucket from the console is not possible - don't forget, your S3 bucket policy literally denies everyone else (**except**  traffic from the VPC endpoint) access to the bucket.
    
-   Our only option is to delete our bucket through the EC2 instance!
    
-   Switch tabs to your instance's terminal.
    
-   Run the command  `aws s3 rb s3://nextwork-vpc-endpoints-yourname`
    

> **💡 What does this command do?**  
> `rb`  is a command that deletes your bucket!
> 
> This means  `rb s3://nextwork-vpc-endpoints-yourname`  is used to delete your S3 bucket nextwork-vpc-endpoints-yourname.

![Step 10: Run `aws s3 rb s3://nextwork-vpc-endpoints-yourname`](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step11.2.png)

Step 10: Run `aws s3 rb s3://nextwork-vpc-endpoints-yourname`

  

-   Nope! The delete failed - we need to make sure our bucket is empty first 🙈
    
-   To delete everything in your bucket, run the command  `aws s3 rm s3://nextwork-vpc-endpoints-yourname --recursive`
    

> **💡 What does this command do?**
> 
> -   `rm`  stands for "remove" and is used to remove things inside your bucket.
>     
> -   `--recursive`  means the remove command should include  **all**  objects and subdirectories inside your bucket. This is a super helpful command to run before delete a non-empty bucket.
>     

![Step 10: Run `aws s3 rm s3://nextwork-vpc-endpoints-yourname --recursive`](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step11.3.png)

Step 10: Run `aws s3 rm s3://nextwork-vpc-endpoints-yourname --recursive`

  

-   Run the command  `aws s3 rb s3://nextwork-vpc-endpoints-yourname`  again.
    

![Step 10: Run `aws s3 rb s3://nextwork-vpc-endpoints-yourname` again.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step11.3.2.png)

Step 10: Run `aws s3 rb s3://nextwork-vpc-endpoints-yourname` again.

  

-   Wooohoo! That's your S3 bucket successfully removed.
    
-   Let's check it's gone by running  `aws s3 ls`  one last time - does your bucket still show in the list of results?
    

![Step 10: Your bucket is alllllll gone!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step11.3.3.png)

Step 10: Your bucket is alllllll gone!

  

**💻 Delete your EC2 Instance**

-   Head back to the  **Instances**  page of your EC2 console.
    
-   Select the checkboxes next to  **Instance - NextWork VPC Endpoint.**
    
-   Select  **Instance state,**  then select  **Terminate Instance.**
    
-   Select  **Terminate**.
    

![Step 10: Select Terminate.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step11.4.png)

Step 10: Select Terminate.

  

**🚪 Delete your VPC Endpoint**

-   Head back to the  **Endpoints**  page of your VPC console.
    
-   Select the checkbox next to your endpoint.
    
-   Select the  **Actions**  dropdown.
    
-   Select  **Delete VPC endpoints.**
    

![Step 10: Select Delete VPC endpoints.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step11.5.png)

Step 10: Select Delete VPC endpoints.

  

**☁️ Delete your VPCs**

-   Select  **Your VPCs**  from your left hand navigation panel.
    
-   Select  **NextWork-vpc,**  then  **Actions**, and  **Delete VPC.**
    

![Step 10: Select Delete VPC.](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step11.6.png)

Step 10: Select Delete VPC.

  

-   Type `delete` in the text box and click **Delete.**
    
-   Note: if you get stopped from deleting your VPC because  **network interfaces**  are still attached to your VPC - delete all the attached network interfaces first!


    

  
  
  

Other network components should be automatically deleted with your VPC, but it's always a good idea to check anyway.

Don't forget to  **refresh**  each page before checking if these resources are still in your account:

1.  Subnets
    
2.  Route tables
    
3.  Internet gateways
    
4.  Network ACLs
    
5.  Security groups
    

  
  
  

One last thing...

Can you remmeber one last resource that we created in this project?

Do you remember one more thing to delete?!

  
  

**🔑 Delete Your IAM Access Keys**

-   Head to your  **IAM**  console.
    
-   Select  **Users**.
    
-   Select your  **Security credentials**  tab.
    
-   Scroll down to your  **Access keys**  panel and select the  **Actions**  drop down.
    
-   Select  **Delete.**
    
-   At the popup panel, select  **Deactivate**, and enter your access key ID into the text field.
    
-   Select  **Delete.**
    
-   Last but definitely not least - don't forget to delete the local access key  **.csv file**  saved on your local computer!
    

![Step 10: Delete your access key!](https://learn.nextwork.org/projects/static/aws-networks-endpoints/high-step11.7.png)

Step 10: Delete your access key!



Nice Work!

THAT'S NETWORKING PROJECT NINE...

... AND THE **ENTIRE** NETWORKING SERIES...

DONE!!!!! 🥳

------------

**Today you've learnt how to:**

🚪 **Set up a VPC endpoint:** You created a VPC endpoint that enables secure, direct access from your VPC to S3. The type of endpoint you set up was an S3 Gateway.  
  

🪣 **Manage permissions with bucket policies:** You set up a strict bucket policy that blocks off all access to your bucket, except for access from your VPC endpoint.  
  

👩‍🔧 **Resolve VPC endpoint issues:** You resolved connectivity issues by adding a route that directs S3-bound traffic from your public subnet to your S3 Gateway endpoint!


### 👏 All done!

Content Credits : **Nextwork**