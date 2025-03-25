

# Access S3 from a VPC

Get resources in your VPC to interact with S3!



WHAT YOU'LL NEED

-   An AWS account -  [Create one here!](https://github.com/dineshrajdhanapathyDD/Cloud/blob/main/AWS/NextWork%20AWS%20Documentation/5%20AWS%20BASIC/legendary-aws-account-setup.pdf))

-   Part 1 of this series -  [Build a Virtual Private Cloud](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%201%20Build%20a%20Virtual%20Private%20Cloud)
-   Part 2 of this series -  [VPC Traffic Flow and Security](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%202%20VPC%20Traffic%20Flow%20and%20Security)

-   Part 3 of this series -  [Creating a Private Subnet](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%203%20Creating%20a%20Private%20Subnet%20in%20Your%20Amazon%20VPC)

-   Part 4 of this series -  [Launching VPC Resources](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%204%20Launching%20VPC%20Resources)

-   Part 5 of this series -  [Testing VPC Connectivity](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%205%20Testing%20VPC%20Connectivity)

-   Part 6 of this series -  [VPC Peering](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%206%20VPC%20Peering)
-   Part 7 of this series -  [Access S3 from a VPC](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/Part%207%20VPC%20Monitoring)



## ⚡️ 30 second Summary

Welcome to AWS networking project number 8!

So far, you've become an absolute pro at creating VPC architectures and launching EC2 instances inside them...

In this project,  **Access S3 from a VPC**, it's time to  **go beyond the boundaries of a VPC**  🪽

  
  

**💭 What's beyond the boundaries of a VPC?**

For example,  **Amazon S3**  is a classic AWS service that doesn't live inside a VPC! S3 is, by default, accessible from the internet, so you can manage its access and security without having to change network settings or internet gateways.

And S3 is just the beginning. Services like AWS IAM, Amazon Route 53, and even databases like DynamoDB also live outside of your VPC.

  
  

**⭐️ Why is this important?**

Engineers and companies combine  **lots**  of AWS services when they build applications, so resources inside your VPC need to know how to work with the other AWS services outside.

Let’s kick off by accessing Amazon S3 from your VPC in this introductory project!

  
  

**Get ready to:**

1.  ☁️ Set up a VPC with an EC2 instance.
    
2.  🔑 Use access keys to give your EC2 instance the power to use your AWS account.
    
3.  🪣 Interact with Amazon S3... through your EC2 instance!
    

![Here's today's game plan.](https://learn.nextwork.org/projects/static/aws-networks-s3/architecture-today.png)

  

  
If you haven't done  **Testing VPC Connectivity** in our networking series, we'd highly recommend doing that first. This project uses key skills from that project!



### ☁️ Step #1

### Set up your VPC and EC2 Instance

  

LET's GOOOOOO!!

Set up the foundations of today's project - a VPC and EC2 instance are coming right up.

  
  

**In this step, you're going to:**

1.  Create a VPC from scratch!
    
2.  Launch an EC2 instance into your VPC.
    

![Step 1: Off we gooooooooo!](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step1.0.png)

Step 1: Off we gooooooooo!

  


-   [Log in to your AWS Account.](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26state%3DhashArgsFromTB_ap-southeast-2_fffdf5be4bb1a27e&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=m-aiqeB2UZeXTGXNyugMP8L64zd_AGUxJl4HLnA-X1o&code_challenge_method=SHA-256)
    

  
  
  

**Create Your VPC**

-   Head to your **VPC** console - search for  `VPC`  at the search bar at top of your page.
    
-   From the left hand navigation bar, select **Your VPCs.**
    
-   Select **Create VPC.**
    
-   Select **VPC and more.**
    
-   Under **Name tag auto-generation**, enter `NextWork`
    
-   The VPC's **IPv4 CIDR block** is already pre-filled to `10.0.0.0/16`  - we'll use this default CIDR block!
    

![Step 1: Your VPC's settings.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step1.1.png)

Step 1: Your VPC's settings.

  

-   For **IPv6 CIDR block**, we'll leave in the default option of **No IPv6 CIDR block.**
    
-   For **Tenancy**, we'll keep the selection of **Default.**
    
-   For **Number of Availability Zones (AZs)**, we'll use just **1** Availability Zone.
    
-   Make sure the **Number of public subnets** chosen is **1**.
    
-   For **Number of private subnets,** we'll keep thing simple today and go with  **0**  private subnets.
    
-   For the **NAT gateways ($)** option, make sure you've selected **None.** As the dollar sign suggests, NAT gateways cost money!
    
-   For the **VPC endpoints** option, select **None.**
    

> 💡 **What are VPC endpoints?**  
> Normally, to access some AWS services like S3 from your VPC, your traffic would go out to the public internet.
> 
> But, VPC endpoints let you connect your VPC privately to AWS services without using the public internet. This means your data stays within the AWS network, which can improve security and reduce data transfer costs.
> 
> We're selecting None here, but we'll learn to set one up in the next project! 👀

-   You can leave the **DNS options** checked.
    

![Step 1: Your VPC's settings.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step1.2.png)

Step 1: Your VPC's settings.

  

-   Select **Create VPC.**  
      
    

  
  
  

**Launch an instance in your VPC**

Wooohooo, now it's time to launch an EC2 instance into your architecture!

-   Head to the **EC2 console** - search for `EC2` in the search bar at the top of screen.
    
-   Select **Instances** at the left hand navigation bar.
    
-   Select **Launch instances**.
    
-   Since your first EC2 instance will be launched in your first VPC, let's name it `Instance - NextWork VPC Project`
    

![Step 1: Name your new instance.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step1.3.png)

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
> EC2 Instance Connect is an EC2 tool designed to help you get direct access to your EC2 instance!
> 
> Once you get direct access to your EC2 instance, you're going into the instance's terminal. This lets you do some advanced work like installing software into your EC2 instance or accessing another AWS service!

-   Select  **Enable.**
    

![Step 1: Your instance's network settings.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step1.4.png)

Step 1: Your instance's network settings.

  

-   For the **Firewall (security groups)** setting, choose **Create security group.**
    

> ⏸️ **PAUSE**  
> Before you read ahead - can you figure out the correct security group settings for this EC2 instance?  
>   
> Hint: you  **WON'T**  need to run ping tests in this project!  
>   
> Hmmm!  
> 🤔  
> 🤔  
> 🤔

▶️ Alright - steps below!

-   Name your security group  `SG - NextWork VPC Project`
    
-   That's it! No security group rules to add.
    

> 💡  **Didn't we use to add other security group rules?**  
> By default, this new security group allows all inbound SSH traffic. That's all we need to use EC2 Instance Connect later.
> 
> We used to add an inbound rule to allow ICMP traffic - but we won't need it if we aren't running any ping tests!

![Step 1: Your new security group settings.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step1.5.png)

Step 1: Your new security group settings.

  

-   Select  **Launch instance.**
    



### 💻 Step #2

### Connect to Your EC2 Instance

  

In this step, we're gonna connect to your EC2 instance and try access an AWS service!

  
  

**In this step, you're going to:**

1.  Connect directly to your EC2 instance.
    

![Step 2: Connect to your EC2 instance](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step2.0.png)

Step 2: Connect to your EC2 instance

  



-   Head to your  **EC2** console and the  **Instances**  page.
    
-   Select the checkbox next to  **Instance - NextWork VPC Project.**
    
-   Select **Connect**.
    
-   In the EC2 Instance Connect set up page, select  **Connect**  again.
    
-   Yay! Successfully connected.
    

![Step 2: Feels good that we've connected right away!](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step2.1.png)

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

![Step 2: Run `aws s3 ls`](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step2.2.png)

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
    

![Step 2: Run `aws configure`](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step2.3.png)

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
    

![Step 3: Create access keys.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step3.0.png)

Step 3: Create access keys.

  



-   Search for  `Access keys`  in the search bar.
    
-   Aha! So it's the IAM console that helps us set this up. Select  **IAM.**
    

![Step 3: Head to the IAM console.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step3.1.png)

Step 3: Head to the IAM console.

  

-   Search for  `Access keys`  again in the IAM console's left hand navigation panel.
    

![Step 3: Search for `Access keys` one more time.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step3.2.png)

Step 3: Search for `Access keys` one more time.

  

-   Choose the search result for managing an access key for your IAM Admin account.
    

![Step 3: Choose the search result that mentions your IAM user name.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step3.3.png)

Step 3: Choose the search result that mentions your IAM user name.

  

-   Select  **Create access key.**
    
-   On the first set up page, select  **Command Line Interface (CLI).**
    
-   Select the checkbox that says  **I understand the above recommendation and want to proceed to create an access key.**
    

![Step 3: Set up your access key.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step3.4.png)

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
    
-   For the  **Description tag value,**  we'll write  `Access key created to access an S3 bucket from an EC2 Instance. NextWork VPC project.`
    

![Step 3: Give your access key a description.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step3.5.png)

Step 3: Give your access key a description.

  

-   Select  **Create access key.**
    
-   OOoo this is important!  **STAY ON THIS PAGE ✋**
    

![Step 3: Stay on this page!](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step3.6.png)

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



### 🪣 Step #4

### Create an S3 bucket with 2 files

  

Access keys DONE.

Before we jump back into our EC2 instance, let's create a bucket in Amazon S3 🪄

After creating this bucket, we'll learn how to access it from our EC2 instance and do things like checking what objects are in the bucket.

  
  

**In this step, you're going to:**

1.  Launch a bucket in Amazon S3.
    

![Step 4: Create an S3 bucket.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step4.0.png)

Step 4: Create an S3 bucket.

  



-   Search for  **S3**  at the search bar at the top of your console.
    

![Step 4: Search for S3 at the search bar up top.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step4.1.png)

Step 4: Search for S3 at the search bar up top.

  

-   Make sure you're in the same Region as your NextWork VPC!
    
-   Select  **Create bucket.**
    

![Step 4: Select Create bucket - here we goooo.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step4.2.png)

Step 4: Select Create bucket - here we goooo.

  

-   Let's set up your bucket! Keep the  **Bucket type**  as  **General purpose.**
    
-   Your  **bucket name**  should be  `nextwork-vpc-project-yourname`
    
    -   Don't forget to replace  **yourname**  with your first name! S3 bucket names need to be globally unique.
        
-   We'll leave all other default settings, go straight to  **Create bucket.**
    

  
  

Nice! Bucket created 😎 😎

![Step 4: Bucket created! That was fast.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step4.3.png)

Step 4: Bucket created! That was fast.

  

Next, let's upload two files into the bucket.

This can be  **any**  two files in your local computer!

-   Click into your bucket.
    
-   Select  **Upload**.
    

![Step 4: Select Upload.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step4.4.png)

Step 4: Select Upload.

  

-   Select  **Add files**  in the  **Files and folders panel.**
    

![Step 4: Select Add files.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step4.5.png)

Step 4: Select Add files.

  

-   Select two files in your local computer to upload.
    

  
  
  

Not sure what to upload? You can download and use these images instead! 👇

**Right click**  on each link, select  **Save link as...**  and select  **Save.**

-   [NextWork - Denzel is awesome.png](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20VPC%20Endpoints/NextWork%20-%20Denzel%20is%20awesome.png)
    
-   [NextWork - Lelo is awesome.png](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20VPC%20Endpoints/NextWork%20-%20Lelo%20is%20awesome.png)
    

  
  
  

Your files should show up in your  **Files and folders**  panel once they're uploaded!

![Step 4: What Files and folders will look like after uploading.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step4.6.png)

Step 4: What Files and folders will look like after uploading.

  

-   Select  **Upload**  at the bottom of the page.
    



### 🔌 Step #5

### Connect to your S3 bucket

  

S3 bucket created 🪣✨

Shall we try use our EC2 instance to interact with it? 👀

  
  

**In this step, you're going to:**

1.  Head back to your EC2 instance.
    
2.  Get your EC2 instance to interact with your S3 bucket.
    

![Step 5: Connect to your S3 bucket.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step5.0.png)

Step 5: Connect to your S3 bucket.

  



-   Now back to your  **EC2 Instance Connect**  tab!
    
-   Are you ready to enter your  **Access keys details now?**
    
-   Open the  **AccessKeys.csv**  file you've downloaded.
    
-   Copy the  **Access key ID.**
    
-   Paste this into your EC2 instance's terminal, and press  **Enter**  on your keyboard.
    

![Step 5: Enter your Access key ID.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step5.1.png)

Step 5: Enter your Access key ID.

  

-   Let's do the same for the  **AWS Secret Access Key!**
    
-   Copy the key from your .csv file, and paste it in the terminal. Press  **Enter**.
    
-   Next, for your  **Default region name,**  open your  **Region**  dropdown on the top right hand corner of your AWS console.
    
-   Copy your  **Region's code name.**  For example, us-west-2.
    

![Step 5: Copy the Region's code name.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step5.2.png)

Step 5: Copy the Region's code name.

  

-   Paste that in your EC2 instance's terminal. Press  **Enter**  on your keyboard.
    
-   We don't have a default output format, so we can leave that empty. Press  **Enter**.
    

> 💡  **What is a default output format?**  
> In just a second, you'll be running a few CLI commands in your EC2 instance's terminal to use Amazon S3. The  **default output format**  is how the results of your commands will display!
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

![Step 5: Leave the default output format empty.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step5.3.png)

Step 5: Leave the default output format empty.

  

-   Nice! Set up is done.
    



-   Let's try running the  `aws s3 ls`  command again to see a list of your account's S3 buckets.
    

  
  
  

YOOOOOO look at that! Do you see a list of your buckets? You might have a shorter list than the one in this screenshot, but the only line to look out for is  **vpc-project-yourname.**

![Step 5: Do you see your bucket name?](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step5.4.png)

Step 5: Do you see your bucket name?

  



-   Next, let's run the command  `aws s3 ls s3://nextwork-vpc-project-yourname`. Make sure to replace  `nextwork-vpc-project-yourname`  with your actual bucket name.
    
-   Based on the command, and what you've learnt about  **aws s3 ls**, can you guess what this command does?
    
-   Nice - we can even see the objects that are inside your bucket!
    

![Step 5: Oooo you can even peek at the objects inside your bucket.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step5.5.png)

Step 5: Oooo you can even peek at the objects inside your bucket.

  



Did you know you could upload files using AWS CLI too?!

-   Run  `sudo touch /tmp/test.txt`  to create a blank .txt file in your EC2 instance.
    

> 💡  **What does this command say?**  
> Let's break it down!
> 
> -   **sudo**  stands for "superuser do" and it's used when you're running a command that typicaly needs elevated user permissions, like installing software or creating new files.
>     
> -   **touch**  is a standard command used to create an empty file if it doesn't exist. If it does exist, this command will update the file's timestamp (i.e. the last time it was accessed) instead.
>     
> -   **/tmp/**  is a common directory path (you can think of a directory path as layers and layers of folders) typically used for temporary files.
>     
> -   **test.txt**  is the name of the empty file you're creating!
>     

-   Next, run  `aws s3 cp /tmp/test.txt s3://nextwork-vpc-project-yourname`  to upload that file into your bucket.
    

> 💡  **What does this command say?**  
> Let's break it down!
> 
> -   **aws s3 cp:**  is the command to  **copy**  files.
>     
> -   **/tmp/test.txt**  is the  **source file path.**  It's saying that the file to copy is test.txt, which exists inside a folder called tmp.
>     
> -   **s3://nextwork-vpc-project-yourname**  is the  **destination path**. It's saying that the file should be copied to the S3 bucket vpc-project-yourname!
>     

-   Finally, run  `aws s3 ls s3://nextwork-vpc-project-yourname`  again - what objects are listed in your bucket now?
    

![Step 5: Run `aws s3 ls s3://nextwork-vpc-project-yourname` again.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step5.6.png)

Step 5: Run `aws s3 ls s3://nextwork-vpc-project-yourname` again.

  

> 💡  **What is the 0 next to test.txt?**  
> The numbers next to each file name is the size fo that file! Since test.txt is an empty file with no data, it has 0 bytes.



-   Switch tabs back to your  **S3**  console.
    
-   Refresh the  **Objects**  tab for your S3 bucket.
    
-   Do you see your new file there? 👀
    

![Step 5: New file spotted!](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step5.7.png)

Step 5: New file spotted!

  

Super cool 😎 A file you've created in your EC2 instance now lives in your S3 bucket too!

😮‍💨 All Done

### Nice work!

 --------------------------------------------- 

You've just completed today's project and  **learnt how to access another AWS service from your VPC.**


  
🗑️ Before You Go

### Delete Your Resources

  

✋  **STOP**

Before diving into the steps for deleting your resources, why not challenge yourself to delete everything in this project on your own?

Keeping track of your resources, and deleting them at the end, is absolutely a skill that will help you reduce waste in your account.

  
  

🛑  **STEPS BELOW:**

  
  
  

**🪣 Delete Your S3 Buckets**

-   Head to your  **S3**  console.
    
-   Select your S3 bucket, and select  **Delete**.
    
-   Enter your bucket name, and select  **Delete bucket**.
    
-   Aha! You need to empty your bucket first. Select  **Empty bucket.**
    
-   Type  `permanently delete`  in the text field.
    
-   Select  **Empty.**
    
-   Select your S3 bucket, and select  **Delete**.
    
-   Enter your bucket name, and select  **Delete bucket**.
    

![Step 7: Select Delete bucket.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step7.1.png)

Step 7: Select Delete bucket.

  

  
  
  

**💻 Delete your EC2 Instance**

-   Head back to the  **Instances**  page of your EC2 console.
    
-   Select the checkboxes next to  **Instance - NextWork VPC Endpoint.**
    
-   Select  **Instance state,**  then select  **Terminate Instance.**
    
-   Select  **Terminate**.
    

![Step 7: Select Terminate.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step7.2.png)

Step 7: Select Terminate.

  

  
  
  

**☁️ Delete your VPCs**

-   Select  **Your VPCs**  from your left hand navigation panel.
    
-   Select  **NextWork-vpc,**  then  **Actions**, and  **Delete VPC.**
    

![Step 7: Select Delete VPC.](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step7.3.png)

Step 7: Select Delete VPC.

  

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
    

![Step 7: Delete your access key!](https://learn.nextwork.org/projects/static/aws-networks-s3/high-step7.4.png)

Step 7: Delete your access key!


Nice Work!

THAT'S NETWORKING PROJECT EIGHT...

DONE!!!!! 🥳
-----------

**Today you've learnt how to:**

-   🔑 **Set up access keys for an EC2 instance:** You created an access key for your EC2 instance. Now your EC2 instance can interact with your AWS services e.g. view objects in your S3 bucket!  
      
    
-   👩‍💻 **Interact with S3 through the AWS CLI:** You learnt what AWS ClI does, and you ran commands to see a list of buckets and even upload an object to a bucket!
    

  

**👀 A teaser for your next project...**

Wooooohoo! Your EC2 instance definitely has access to your bucket - your access key worked 👏

Buttt your EC2 instance is accessing your bucket through the public internet.

This isn't the most secure way to communicate - external threats and attacks can easily intercept traffic and get access to your AWS environment or sensitive data.

What's a VPC resource that could solve this?

🥁 Introducing... VPC endpoints!
![Coming up next - VPC endpoints.](https://learn.nextwork.org/projects/static/aws-networks-s3/architecture-next.png)

Coming up next - VPC endpoints.



### 👏 All done!

Content Credits : **Nextwork**