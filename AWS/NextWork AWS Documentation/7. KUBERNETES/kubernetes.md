

# Launch a Kubernetes Cluster

![Tool icon](https://learn.nextwork.org/static/tool.svg)

WHAT YOU'LL NEED

-   An AWS account -  [Create one here!](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html?refid=em_127222&p=free&c=hp&z=1)

KEY CONCEPTS

-   [Amazon EKS]([Amazon Elastic Kubernetes Service Documentation](https://docs.aws.amazon.com/eks/))
-   [Amazon EC2]([Amazon Elastic Compute Cloud Documentation](https://docs.aws.amazon.com/ec2/))
-   [AWS CloudFormation]([AWS CloudFormation Documentation](https://docs.aws.amazon.com/cloudformation/))
-   [AWS IAM]([AWS Identity and Access Management Documentation](https://docs.aws.amazon.com/iam/))
-   [Kubernetes](https://kubernetes.io/)

Welcome to this project on Kubernetes and Amazon EKS (Elastic Kubernetes Service)!
In this project, we'll deploy our first Kubernetes cluster,**zero experience** to deploying a containerized app 🚀


**Get ready to...**

-   🌠 Launch and connect to an EC2 instance.
    
-   ✨ Create your very own Kubernetes cluster.
    
-   ☁️ Monitor cluster creation with CloudFormation.
    
-   🔑 Access your cluster using an IAM access entry.
    
-   💎 (Secret Mission) Test the resilience of your Kubernetes cluster.

![What you're about to build.](https://learn.nextwork.org/projects/static/aws-compute-eks1/architecture-complete.png)

### Step-By-Step Project
---
## 🚀 Step #1

### Launch and Connect to an EC2 instance

  

Let's kick things off by setting up our very own **EC2 instance**, which we'll use to send commands to Kubernetes in this project series.

![What you're about to build in this step!](https://learn.nextwork.org/projects/static/aws-compute-eks1/architecture-1.png)

What you're about to build in this step!

  

**In this step, you're going to:**

-   Launch an EC2 instance.
    
-   Connect to your instance so you can start sending commands.
    



**Launch an EC2 Instance**

-   Log into your [AWS Management Console as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    

    
-   Head to `EC2` in your AWS Management Console.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_1.png)

  
  ![Screenshot 2025-05-16 222258](https://github.com/user-attachments/assets/e28e2c8f-291c-4bf5-8226-cae34598566b)

-   Select **Instances** at the left hand navigation bar.
    
-   Check that you're using the **AWS Region** that's closest to you. Select the Region name at the top right corner of your console if you'd like to switch.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_2.png)

  ![Screenshot 2025-05-16 222347](https://github.com/user-attachments/assets/3abd1f6d-c682-409d-95df-d589324b62d6)


-   Select **Launch instances** at the top right corner of your console.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_3.png)


  

-   Name your EC2 instance `eks-instance`
    
-   For the **Amazon Machine Image,** select **Amazon Linux 2023 AMI.**
    

> 💡 **What is AMI? What is Free tier eligible?**  
> An **AMI** (**Amazon Machine Image**) is a template or blueprint used to create EC2 instance. The image defines your EC2 instance's operating system and with the applications needed to launch the instance.
> 
> **Free tier eligible** AMIs are those that qualify for the AWS Free Tier, so you won't get charged for using it. Just remember that not all AMIs are free!

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_4.png)

![Screenshot 2025-05-16 222541](https://github.com/user-attachments/assets/85206c46-f428-4ee6-bb8d-ed99aeb011b1)  

-   For the **Instance type,** select **t2.micro.**
    

> 💡 **What is instance type?**  
> If AMIs give you pre-built software and operating systems, instance types cover the '**hardware**' components. CPU power, memory size, storage space and more!
> 
> So, while the AMI decides what operating system your server runs, the instance type determines how fast and powerful it performs.
> 
> For example, a larger instance type might have more CPU power for heavy tasks, while a smaller type (for example, **t2.micro**) might be more affordable for light use.

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_5.png)

  ![Screenshot 2025-05-16 222825](https://github.com/user-attachments/assets/19ffa5be-b28a-4817-8b3d-e0a2f3f857bc)


-   For the **Key pair (login)** panel, select **Proceed without a key pair (not recommended).**
    

> **💡 What is a key pair?**  
> A **key pair** is like a lock and a key for your EC2 instance. Usually you'd need a key pair to SSH connect to your instance, but we're using a simpler way to do this later in this step (EC2 Instance Connect).
> 
> If you're new to key pairs and SSH connections and want to learn more, check out Steps #1 and #2 of [Testing VPC Connectivity](https://learn.nextwork.org/projects/aws-networks-connectivity?track=high).

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_6.png)

  

-   We won't change anything in the **Networking** section and keep the default security group.
    
-   Notice that the security group allows SSH traffic from anywhere (0.0.0.0/0) which isn't the best security practice, but we'll leave this to make connecting via SSH easier later on.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_7.png)

![Screenshot 2025-05-16 222800](https://github.com/user-attachments/assets/2e9a9bb7-10f9-4002-913a-bb62489ea49a)  

-   Select **Launch instances**.
    

  
  

**Connect to Your Instance**

Now that our EC2 instance is up and running, let's connect to it using EC2 Instance Connect.

> 💡 **What is EC2 Instance Connect?**  
> EC2 Instance Connect is a shortcut way to get direct SSH access to your EC2 instance. Instead of having to manage a key pair manually, Instance Connect connects you to your instance within your AWS Management Console - no download required!
> 
>   
> 💡 **Extra for PROs: Why are we using EC2 Instance Connect?**  
> When you connect via SSH to an EC2 instance (which you can learn how to do in [Set Up a Web App in the Cloud](https://learn.nextwork.org/projects/aws-devops-vscode)), you usually need to:
> 
> -   Generate a key pair.
>     
> -   Associate the public key with your EC2 instance.
>     
> -   Securely store your private key on your local machine.
>     
> -   Set up an SSH client (a software that can handle the SSH protocol, like Terminal on Max/Linux or VS Code).
>     
> -   Provide your private key and run ssh commands to set up an SSH connection to your EC2 instance.
>     
> 
>   
> EC2 Instance Connect lets us skip all those steps and connect to your EC2 instances directly using the AWS Management Console. We'd use the usual, manual way when we have some development work to do, but Instance Connect is great if we're just running a few commands in the terminal.
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-eks1/instance_connect.png)
> 
>   

-   Select the instance you just launched.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_8.png)

  ![Screenshot 2025-05-16 222954](https://github.com/user-attachments/assets/6ec36005-a270-4ea8-bb4b-4d8e6303feb7)

-   Select the checkbox next to **eks-instance.**
    
-   Select the **Connect** button.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_9.png)

  ![Screenshot 2025-05-16 223014](https://github.com/user-attachments/assets/f50bf201-e75a-46ac-8a29-ba4ee8091145)


-   Welcome to the instance connection page! This is where AWS gives you different options to connect with your EC2 instance.

![Screenshot 2025-05-16 223103](https://github.com/user-attachments/assets/db235c06-4bf1-4a30-b398-1128bde1cee9)    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_10.png)

  
 ![Screenshot 2025-05-16 223145](https://github.com/user-attachments/assets/de16665c-b709-4b82-8c31-75133109c2a0) 

> 💡 **What is the yellow warning banner about Port 22?**  
> Good spotting! That warning banner is a **security reminder** from AWS.
> 
> **Port 22** is the default port for SSH (Secure Shell) connections, which is what we use to connect securely to our EC2 instance.
> 
> Back when we set up our EC2 instance, we used the default security group which allows SSH access from **any** IP address. This opens your instance to the entire internet, which makes it more vulnerable to attacks.
> 
> 💡 **Extra for PROs: Is using the default security group security best practice?**  
> We wouldn't do this for production environments or long-term use, but for now the default security group makes it easier to use EC2 Instance Connect.
> 
> If we don't use the default security group, we'd have to manually edit our instance's inbound rules to let in Instance Connect's range of IP addresses, which is different depending on your AWS Region.
> 
> Feeling up for a challenge? Try editing your security group settings to make it more secure (while letting you use EC2 Instance Connect). 



-   Select **Connect** at the bottom of the page.
    
-   This will open a terminal session directly in your browser in a new tab.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_11.png)

![Screenshot 2025-05-16 223521](https://github.com/user-attachments/assets/2da5b9dc-ca71-4470-9900-6f264c3bacda)


---  

## 👺 Step #2




### Launch an EKS cluster (and get an error)

  

Now for the main event – creating our Kubernetes cluster with **Amazon EKS**!

We'll use a handy command-line tool called **eksctl** to create a cluster within your EC2 instance's termninal.

> 💡 **What is Kubernetes?**  
> **Kubernetes** is a tool that helps you manage your running containers.
> 
> Once you've created containers (e.g. using [Docker](https://docs.docker.com/)), Kubernetes helps keep them running smoothly by automatically handling tasks like load balancing, scaling, and restarting containers if they fail. It doesn’t build the containers—that’s Docker’s job—but it’s great for keeping them running without you having to do it manually.
> 
>   
> 💡 **What is Amazon EKS?**  
> While Kubernetes makes it easier to work with containers, Amazon EKS makes it easier to work with Kubernetes itself!
> 
> Setting up Kubernetes from scratch can be quite a time consuming and complex thing to do, because you'd need to configure Kubernetes' networking, scaling, and security settings on your own. Amazon EKS handles all of these set up tasks for you and helps you integrate Kubernetes with other AWS services.
> 
> **eksctl** is a tool specifically for working with EKS in the command line (more on this soon).

![What you're about to build in this step!](https://learn.nextwork.org/projects/static/aws-compute-eks1/architecture-2.png)

What you're about to build in this step!

  

**In this step, you're going to:**

-   Attempt to create an EKS cluster (and run into an error)!
    
-   Install a tool for creating Kubernetes clusters called eksctl.
    



Let's try creating a cluster right away.

-   In your EC2 Instance Connect window, run this command:
    


```bash
eksctl create cluster \
--name nextwork-eks-cluster \
--nodegroup-name nextwork-nodegroup \
--node-type t2.micro \
--nodes 3 \
--nodes-min 1 \
--nodes-max 3 \
--version 1.31

```


> 💡 **What does this command do?**  
> This command is meant to set up a Kubernetes cluster! We'll dive into the specifics of this command and Kubernetes in just a second. For now...

... you'll likely see an error message saying something like `eksctl not found`.

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_12.png)

  
![Screenshot 2025-05-16 223909](https://github.com/user-attachments/assets/9dff8533-97ac-41c3-afb3-0522998a8212)

Don't worry, this is expected! It means we haven't installed **eksctl** yet.

> 💡 **What is eksctl?**  
> **eksctl** is an official AWS tool for managing Amazon EKS clusters in your terminal. It's much, much easier to use compared to setting up a Kubernetes cluster using the AWS CLI!
> 
> If we were using the AWS CLI, we'd have to create a lot of other components manually before getting to deploy a cluster. You'll learn what these components are in Step #4.

**Install eksctl**

-   Run these commands in your terminal:
    



```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv -v /tmp/eksctl /usr/local/bin

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_13.png)

  

> 💡 **What do these commands do?**  
> The commands here download and install **eksctl** on your EC2 instance.
> 
> The first commands downloads the latest eksctl release from GitHub, then the second command moves it to a directory that lets you run eksctl from anywhere in your terminal.

-   Check that eksctl is installed correctly by running `eksctl version`. You should see the version number printed in the terminal.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_14.png)

  
![Screenshot 2025-05-16 224055](https://github.com/user-attachments/assets/3985056c-9d48-4e2e-a49a-d29544ac5563)

> 🙋‍♀️ **I don't see a version number!**  
> No stress! Try refreshing the Instance Connect tab and run the installation commands again.
> 
> Does a version number pop up the second time?
> 


----

## 🫐 Step #3

### Launch an EKS cluster (for real this time)

  

Now that eksctl is all installed, let's give launching an Kubernetes cluster on EKS another go. We'll also learn about giving your EC2 instance the permission to run AWS commands!

> 🚨 Creating a Kubernetes cluster and using EKS **is not** AWS Free Tier eligible, so expect to spend [$0.10 USD for every hour you leave your EKS cluster running](https://aws.amazon.com/eks/pricing/) once it's created.
> 
> Make sure to follow all the deletion instructions at the end of this project to minimise costs for this project.

![What you're about to build in this step!](https://learn.nextwork.org/projects/static/aws-compute-eks1/architecture-3.png)

What you're about to build in this step!

  

**In this step, you're going to:**

-   Attempt to create an EKS cluster (and run into an error again)!
    
-   Set up your EC2 instance's IAM role.
    
-   Create an EKS cluster using eksctl.
    


Now that eksctl is installed, let's try creating our cluster again.

-   Run this command:
    


```bash
eksctl create cluster \
--name nextwork-eks-cluster \
--nodegroup-name nextwork-nodegroup \
--node-type t2.micro \
--nodes 3 \
--nodes-min 1 \
--nodes-max 3 \
--version 1.31 \
--region [YOUR-REGION]

```

-   Make sure to replace `[YOUR-REGION]` in the last line of the command with your AWS region code, e.g. **us-west-2**. Make sure the region you pick is same region where you launched your EC2 instance.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_47.png)

  ![Screenshot 2025-05-16 224857](https://github.com/user-attachments/assets/ddb6f0d3-3d57-4cb1-a844-e787fa1626bc)

> 💡 **Dang it! What's the error this time?**  
> Your EC2 instance doesn’t have the permission to create an EKS cluster. By default, you can think of your EC2 instance as another computer that isn't 'logged in' or has access to your AWS Account yet.
> 
> We’ll need to set up an IAM role that lets your EC2 instance communicate with services like EKS to create the cluster.

**Create an IAM role for your EC2 instance**

Let's resolve this permissions error by setting up a new **Role** in AWS IAM.

-   In a new tab, head to your `AWS IAM` console.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_16.png)

 ![Screenshot 2025-05-16 224958](https://github.com/user-attachments/assets/26e916d5-cfd9-4931-a79b-b891769a809c)
 


-   Select **Roles** from the left hand sidebar.

![Screenshot 2025-05-16 225016](https://github.com/user-attachments/assets/d2a234f3-621c-4706-9752-6c34d5a4d529)


    
-   Select **Create role.**
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_17.png)

 ![Screenshot 2025-05-16 225041](https://github.com/user-attachments/assets/953bb0a8-1f87-4be1-baaa-4aa647ccfb4b) 

-   Under **Trusted entity type,** select **AWS service** to tell AWS that we're setting up this role for a AWS serice (Amazon EC2).
    
-   Under **Use case,** select **EC2.**
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_48.png)

  ![Screenshot 2025-05-16 225156](https://github.com/user-attachments/assets/9f5b6ec2-83f4-4b9a-b472-19871d17cb4d)

-   Select **Next.**
    
-   Under **Permissions policies,** we'll grant our EC2 instance **AdministratorAccess.**
    

> 💡 **What does this permission policy mean?**  
> This gives your EC2 instance the power to access any AWS resource and service in your AWS account.
> 
> A super powerful move, which your EC2 instance will need when it deploys and manages your Kubernetes cluster (your instance will be using a lot of different services).
> 
>   
> 💡 **Extra for PROs: Is granting AdministratorAccess best practice?**  
> Great question! Granting AdministratorAccess is powerful but not ideal for long-term use. We’re using it now because we don’t know _all_ the services that will be involved in the project yet.
> 
> Granting the most powerful permissions now means we avoid running into permission issues that could slow us down. Once we know which services your EC2 instance really needs for this project to work, we can dial back to more specific, secure settings.
> 
> Solution Architects typically plan security settings **before** they build anything, aiming to follow the **principle of least privilege**—only giving the exact permissions needed for the job.

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_49.png)

  ![Screenshot 2025-05-16 225253](https://github.com/user-attachments/assets/527cc8a5-502a-409b-bc82-af12e1dfaaf4)



-   Make sure the **AdministratorAccess** option is checked, and select **Next**.
    
-   Let's give this role a straightforward name - `nextwork-eks-instance-role`
    
-   Enter a short description:
    


```text
Grants an EC2 instance AdministratorAccess to my AWS account. Created during NextWork's Kubernetes project.

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_50.png)

  ![Screenshot 2025-05-16 225401](https://github.com/user-attachments/assets/6c98f18e-f177-4358-992d-8227deef4e28)

-   Select **Create role.**
    

 ![Screenshot 2025-05-16 225513](https://github.com/user-attachments/assets/71411cd0-6fec-4887-8c2b-9273bbbe190a)
 
  

**Attach IAM role to EC2 instance**

Great! Your new role is born. Now we'll add this role to our EC2 instance.

-   Head back to the **Amazon EC2** console.
    
-   Select **Instances** from the left hand sidebar.
    
-   Select the checkbox next to your **nextwork-eks-instance** EC2 instance.

![Screenshot 2025-05-16 225549](https://github.com/user-attachments/assets/075dfb32-758d-45df-94dd-92de35077b09)

    
-   Select the **Actions** dropdown, and then **Security** -> **Modify IAM role.**
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_20.png)

  
![Screenshot 2025-05-16 225653](https://github.com/user-attachments/assets/6fb575d3-7497-41ad-95a0-8ceae92e1d94)
-   Under **IAM role,** select your new `nextwork-eks-instance-role` role.
    
-   Select **Update IAM role**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_21.png)

  ![Screenshot 2025-05-16 225718](https://github.com/user-attachments/assets/c65ff79f-47f8-4ac2-a355-8da79c58cffe)

![Screenshot 2025-05-16 225734](https://github.com/user-attachments/assets/81bd32fd-802e-477e-958a-6c53f3b7f654)

  

**Create your EKS cluster agains (third time lucky)!**

-   Still in your browser, head back to your **EC2 Instance Connect** tab.
    
-   Let's run the command to kick off our Kubernetes cluster one more time...
    



```bash
eksctl create cluster \
--name nextwork-eks-cluster \
--nodegroup-name nextwork-nodegroup \
--node-type t2.micro \
--nodes 3 \
--nodes-min 1 \
--nodes-max 3 \
--version 1.31 \
--region [YOUR-REGION]

```

-   Make sure to replace `[YOUR-REGION]` in the last line of the command with your AWS region code, e.g. **us-west-2**. Make sure the region you pick is same region where you launched your EC2 instance.
    

> 💡 **What does this command do?**  
> We'll learn all these terms over the rest of this project, but as a sneak peek, this command will:
> 
> -   Set up an EKS **cluster** named `nextwork-eks-cluster`
>     
> -   Launch a **node group** called `nextwork-nodegroup`.
>     
> -   Use `t2.micro` EC2 instances as **nodes**.
>     
> -   Start your node group with `3` **nodes** and automatically scale between 1 (minimum) and 3 nodes (maximum) based on demand.
>     
> -   Use Kubernetes **version** `1.31` for the cluster setup.
>     

![Off we go!](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_22.png)

Off we go!
![Screenshot 2025-05-16 225919](https://github.com/user-attachments/assets/2536a1b9-1879-42f8-b6f0-19d15317620c)
  
![Screenshot 2025-05-16 230910](https://github.com/user-attachments/assets/6459ab3b-30b2-42ad-8584-eae9c2a2f5df)

![Screenshot 2025-05-16 231235](https://github.com/user-attachments/assets/7e2df0d3-9a93-4b46-8a3d-2c0fc3443549)


⏰ **Check the time on your computer now.** Don't forget that EKS charges $0.10 for every hour your cluster is running.

Creating a cluster can take 15-20 minutes, so grab a drink and read on to know more about Kubernetes while we wait.

> **💡 What is Kubernetes?**  
> **Kubernetes** is a **container orchestration** platform, which is a fancy way to say that it coordinates containers so they're running smoothly across all your servers. It makes sure all your containers are running where they should, scales containers automatically to meet demand levels, and even restarts containers if something crashes.
> 
> It’s THE standard tool for keeping large, container-based applications steady and easy to scale with traffic. That's why big tech companies, startups, and developers worldwide use Kubernetes.
> 
>   
> **💡 Why do people use Kubernetes?**  
> Without a tool like Kubernetes, you would create and manage every container manually. You’d have to start each container yourself and keep an eye on them to restart any that crash.
> 
> Traffic to your app going up or down would mean turning containers on or off one by one, and you’d also have to make sure each container has access to storage if it needs it. Updating your app would mean carefully swapping out containers without causing downtime.
> 
> As you might imagine, managing hundreds or thousands of containers this way would be a huge amount of work and hard to get right all the time. Kubernetes takes care of all these tasks automatically, so you can focus on building your app's features instead.



Still waiting on your terminal to finish running the command? Head to the next step anyway, you don't need your cluster to be ready to do it!

---
## 🕵️ Step #4

### Track How AWS Creates Your EKS Cluster

  

Let's take a tour around the AWS Management Console to see **how** AWS actually creates a Kubernetes cluster. What happens under the hood when you ran `eksctl create cluster`?

![What you're about to build in this step!](https://learn.nextwork.org/projects/static/aws-compute-eks1/architecture-4.png)

What you're about to build in this step!

  

**In this step, you're going to:**

-   Use CloudFormation to track how your cluster is getting created.
    



  
  

-   In a new tab, head to the `CloudFormation` console.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_23.png)

 ![Screenshot 2025-05-16 231636](https://github.com/user-attachments/assets/35f8b0ee-77f4-42dd-94f3-a10e3be3b24f)
 

> **💡 What is CloudFormation?**  
> **CloudFormation** is AWS’s service for setting up infrastructure as code. You write a **template** describing the resources you need (like an instruction manual), and CloudFormation handles creating and configuring those resources.
> 
>   
> **💡 Why are we in CloudFormation?**  
> **eksctl** actually uses CloudFormation under the hood to create your EKS cluster.
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-eks1/eksctl.png)
> 
> When you ran the `eksctl create cluster` command, eksctl sets up a CloudFormation stack to automate the creation of all the necessary resources for the EKS cluster.

-   In the **Stacks** page, notice that there is a new stack in progress! The stack should be called **eksctl-nextwork-eks-cluster-cluster.**

![Screenshot 2025-05-16 231654](https://github.com/user-attachments/assets/84ab0b13-ad20-4c4a-840f-45b3f84d9b23)

![Screenshot 2025-05-16 231810](https://github.com/user-attachments/assets/8ee39bd8-b85d-47bb-ad50-b2589ce90081)
    
-   Select the stack, and track the **Events** tab.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_44.png)

![Screenshot 2025-05-16 231745](https://github.com/user-attachments/assets/7068f754-4a02-4b7e-a178-52330f1ce338)
  

> 💡 **What are these Events about?**  
> The **Events** tab gives you a timeline of each action CloudFormation is taking to set up your resources. It’s a live update of what’s happening, which can be helpful for tracking progress or identifying any issues that come up during creation.
> 
> You can even select the **Refresh** button at the top of the panel to watch new updates come through on your stack's resources.

-   Now select the **Resources** tab.
    
-   Woah! Lots of resources are getting created here.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_24.png)

![Screenshot 2025-05-16 231820](https://github.com/user-attachments/assets/a5b9e4d5-3a33-4d2b-85d8-71feb63299bf)  

![Screenshot 2025-05-16 231829](https://github.com/user-attachments/assets/e6510583-22d0-4aec-af49-c9e12c8cc33a)

![Screenshot 2025-05-16 232032](https://github.com/user-attachments/assets/8836a67d-e1ea-4edd-9a5d-db71e074e0e4)

![Screenshot 2025-05-16 232428](https://github.com/user-attachments/assets/15561307-c256-430d-b33f-1c863d77bc76)


> 💡 **What are these resources?**  
> You might notice in your **Resources** tab all sorts of **networking resources** - VPC, subnets, route tables, security groups, NAT gateways and internet gateways!
> 
> These resources set up a private, secure network for your containers to connect with each other and the internet while keeping your app private. It's not required for this project that you understand all these components, but you can learn more about VPC resources at [Launching VPC Resources.](https://learn.nextwork.org/projects/aws-networks-ec2?track=high)
> 
> Note that this is one of the big reasons why you'd pick eksctl over the AWS CLI - if we were using AWS CLI, we'd have to create each of these resources manually!
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-eks1/aws-cli.png)
> 
>   
> 
> 💡 **Extra for PROs: Why can't I just use my account's default VPC?**  
> While you _could_ use your AWS account's default VPC, you might need to manually set up new VPC resources and edit a few settings to make it work for a Kubernetes cluster. eksctl creates a whole new VPC for us to let us start fresh.



  
  

-   You might also notice a NEW stack pop up in the Stacks page. This should pop up 10-12 minutes from the time you ran the `create cluster` command.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_25.png)

  
![Screenshot 2025-05-16 232507](https://github.com/user-attachments/assets/acc8c4ba-39e8-4aeb-9a3a-efcb6dc165d4)

> 💡 **Why is there a second stack?**  
> The second stack is specifically for your **node group**, which is a group of EC2 instances that will run your containers.
> 
> CloudFormation separates the core EKS **cluster** stack from the **node group** stack to make it easier to manage and troubleshoot each part independently, especially if one half fails.
> 
>   
> 💡 **What's the difference between a cluster and a node group?**  
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-eks1/kubernetes-cluster.png)
> 
> Think of a **cluster** as the entire environment that Kubernetes manages for your containerized app. This cluster is made up of **nodes** (the servers that actually run your containers) and a **control plane** (the brain that decides things like when to create or shut down containers).
> 
> Within your cluster, the nodes are organized into **node groups.** Node groups let you manage multiple nodes more easily by grouping them together, so you can control settings like instance type and resource limits for the whole group instead of adjusting each node individually. This makes it much simpler to scale and configure nodes for specific tasks.

-   Select the nodegroup stack, and open up the **Events** tab to get a preview of what being deployed.
    
-   Wait until the first stack i.e. **eksctl-nextwork-eks-cluster-cluster** is in **CREATE_COMPLETE** status.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_46.png)

  

![Screenshot 2025-05-16 232507](https://github.com/user-attachments/assets/acc8c4ba-39e8-4aeb-9a3a-efcb6dc165d4)

  
  

If your second stack isn't complete yet, that's okay - we can still head to the next step in the meantime!

----
## 👀 Step #5

### Access EKS from the Management Console

  

Now that our EKS cluster is ready, let's see it using the AWS Management Console.

![What you're about to build in this step!](https://learn.nextwork.org/projects/static/aws-compute-eks1/architecture-5.png)

What you're about to build in this step!

  

**In this step, you're going to:**

-   Open the EKS console.
    
-   Grant yourself the permissions to interact with your cluster.
    
![Screenshot 2025-05-16 232754](https://github.com/user-attachments/assets/fb9174b9-37f9-40ec-970d-e163a1ad9129)


**Accessing the EKS Console**

-   In a new tab, open up the `EKS` console.
    
-   Select the new **nextwork-eks-cluster** cluster you just created.
    
-   Welcome to your EKS cluster's dedicated page!
    
-   Select the **Compute** tab.
    
-   Scroll down to the **Node groups** panel - aha, it's getting created!
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_26.png)

![Screenshot 2025-05-16 232845](https://github.com/user-attachments/assets/61085f4e-eb27-4b33-a9d5-646a02639573)  

-   If it's been some time since you ran your create cluster command, you might even notice that it's already in **Created** status.
    
-   Scroll back up to the top of your cluster's page. Notice that there are two banners in blue.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_27.png)

![Screenshot 2025-05-16 232952](https://github.com/user-attachments/assets/5765d56c-d5ee-44bf-9b62-5247aefb85d1)  

> 💡 **What are these two banners saying?**  
> The two blue banners in the EKS console are letting you know that while you have created a node group, you might not have the permission to see the nodes inside.
> 
>   
> 💡 **But my IAM User has AdministratorAccess - how could it not have permission?**  
> AWS permissions alone don’t automatically carry over to Kubernetes — Kubernetes has its own way of managing access within a cluster.
> 
> Even if you have AdministratorAccess in AWS, which grants full access to AWS resources, Kubernetes will only let you into different parts of the cluster if you have permissions under its own system too.
> 
> Let's learn about this system and grant ourselves access now!

  ![Screenshot 2025-05-16 233100](https://github.com/user-attachments/assets/d3dc212c-57b3-4a0a-82ec-792099d92514)
  

**Set up your own access to your cluster**

-   Select **Create access entry** at the blue banner at the top of the page.
    

> 🙋‍♀️ **I don't see that top banner**  
> No problemo! There's a second way to get to the same place:
> 
> -   Head to the **Access** tab
>     
> -   Under **IAM access entries**, select **Create access entry**.
>     
> 
>   
> **💡 What are IAM access entries?**  
> **IAM access entries** connect AWS IAM users with Kubernetes’ Role-Based Access Control (RBAC), which is Kubernetes' system to manage access inside a cluster.
> 
> In short, your IAM Admin user (the one you're using to open this Management Console) needs a specific access entry to get access to the nodes in your EKS cluster.

Nice work, we can now set up an IAM access entry.

-   Under **IAM Principal**, select your IAM user's ARN. Double check your IAM Admin's name at the top right corner and make sure it matches your ARN.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_28.png)

  ![Screenshot 2025-05-16 233202](https://github.com/user-attachments/assets/5e0827d7-fdf3-47e2-96da-c42c11557447)

-   Select **Next**.
    
-   Under **Policy name,** select `AmazonEKSClusterAdminPolicy.`
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_30.png)

  ![Screenshot 2025-05-16 233316](https://github.com/user-attachments/assets/f91d3fea-86d6-47ad-b0f2-160335d3516b)


> 💡 **What does this policy do?**  
> The **AmazonEKSClusterAdminPolicy** gives you full administrative rights over your EKS clusters. Your IAM user will be able to see and control all parts of your EKS cluster - inclusding all the nodes inside!

-   Select **Add policy.**
    
-   Select **Next**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_31.png)

  ![Screenshot 2025-05-16 233329](https://github.com/user-attachments/assets/cdd8674c-bc91-4db7-82fa-33e2ac5bee67)

![Screenshot 2025-05-16 233501](https://github.com/user-attachments/assets/c0bc8739-0d2e-4f6c-aeee-7d2eb39798e2)


-   Select **Create**.
    
-   Head back to your cluster's page.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_29.png)

  ![Screenshot 2025-05-16 233519](https://github.com/user-attachments/assets/52923258-5ad4-4ac3-8a46-1791d7402b75)

-   Select the refresh button on the console. You should now see your nodes listed under your node group.
    

> 💡 **Why are there three nodes but one node group?**  
> The **node group** is a group of nodes that share the same configuration, like instance type and scaling settings. In this case, our node group has three nodes, which means there are three EC2 instances that will run containers like a single unit.
> 
>   
> 🙋‍♀️ **I don't see any nodes**  
> Totally possible!
> 
> 1.  Head back to your **CloudFormation** console.
>     
> 2.  Is your **nodegroup** stack in **CREATE_COMPLETE** too? If not, wait a few more moments.
>     
> 3.  Is your **nodegroup** cluster showing **ROLLBACK_COMPLETE**? Select the **Events** tab for that Stack and select **Detect root cause** to check why it's failed. See if you can resolve the root cause on your own, 
>     
> 4.  Everything looks okay in CloudFormation? Refresh your EKS console again just in case, 
>     

Nice work creating your very first Kubernetes cluster with Amazon EKS!

![Screenshot 2025-05-16 233657](https://github.com/user-attachments/assets/5f46a939-af6b-47d5-a8ae-3b6c56c0fe09)

![Screenshot 2025-05-16 233753](https://github.com/user-attachments/assets/5747fe54-c800-4361-9997-aadcfd14c77b)

Well done on setting up the basics of Amazon EKS. You'll go through this process of creating an EKS cluster **again** in the next project of this Kubernetes series.

---
## 💎 Secret Mission

### Delete Nodes (and watch them regenerate)

  

Welcome to your 🤫 exclusive 🤫 secret mission.

Your mission, should you choose to take it, is to test the **resilience** of your Kubernetes cluster. We'll delete some nodes and see how Kubernetes automatically recovers them like magic.

  
  

**💎 In this secret mission, you're going to:**

-   Terminate EC2 instances in your Kubernetes cluster.
    
-   Watch Kubernetes automatically replace the terminated instances.
    
-   Showcase your secret mission in your **project documentation.**
    

> 💎 **Congratulations** - Secret Mission unlocked!



  
  

**Terminating Nodes**

-   Head to the EC2 service in the AWS Management Console.
    
-   Find the EC2 instances that are part of your EKS cluster's node group. They will have names similar to `nextwork-eks-cluster-nextwork-nodegroup-Node`
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_33.png)

  ![Screenshot 2025-05-16 234547](https://github.com/user-attachments/assets/e8b0b9a5-20c5-4260-95d5-5d19fcdb74b1)


> **💡 How are Kubernetes and EC2 instances related?**  
> When you create **nodes** in a Kubernetes cluster on AWS, each node is actually an EC2 instance!
> 
> Kubernetes uses a generic term (node) because different cloud platforms use different cloud resources to be the node; in AWS, we use EC2 instances as our nodes.

-   Select all three nodes, select the **Instance state** dropdown, and select **Terminate (delete) instance**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_34.png)

  ![Screenshot 2025-05-16 234626](https://github.com/user-attachments/assets/7f9fb8d6-0c02-460a-a460-59fea7338dff)

-   Select **Terminate (delete).**
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_35.png)

 ![Screenshot 2025-05-16 234747](https://github.com/user-attachments/assets/41d39317-806a-4460-96bd-2b2602d90e27)

 

-   All three nodes should show that they are in **Shutting-down** state.
    
    ![Screenshot 2025-05-16 234803](https://github.com/user-attachments/assets/0a62ac0a-b558-4ca1-8354-40d1deb9ef3e)
    
-   After a another minute, your nodes will show that they are **Terminated.**

![Screenshot 2025-05-16 234835](https://github.com/user-attachments/assets/a9f43fb2-4c47-47dc-8bed-1c353d1976b4)
    
-   Check your **EKS** console and refresh the tab - are you seeing any nodes?
    
![Screenshot 2025-05-16 234913](https://github.com/user-attachments/assets/ed2e399b-f930-44b8-b8cd-a5aa7b687a33)

![Screenshot 2025-05-16 234949](https://github.com/user-attachments/assets/d22ec2dc-8e89-4fba-9de9-305c7a1f5764)

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_36.png)


  
![Screenshot 2025-05-16 235411](https://github.com/user-attachments/assets/2becbf91-57dd-4240-ac83-a9e5b30b308e)


-   We'll have to wait a few minutes before the next step. While we wait...
    



> **💡 What will happen once you delete nodes in a node group?**  
> When you delete nodes in a node group, Kubernetes automatically detects the change and **launches new nodes** to keep the cluster running at its **desired state** (more on this in a second).
> 
> This is one of the key benefits of using Kubernetes – it makes sure your application is always running, even if some nodes fail.

-   Select your node group **nextwork-nodegroup.**
    
-   In the **Details** panel, notice how the **Desired size** is 3, the **Minimum size** is 1, and the **Maximum size** is 3 nodes.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_43.png)

  

> **💡 What do desired state, minimum size, and maximum size mean?**  
> The **desired size** is the number of nodes you want running in your node group.
> 
> The **minimum size** is the minimum number of nodes your group needs to have to keep your app available at all times (even in low-demand periods).
> 
> The **maximum size** is the maximum number of nodes that you'll allow inside this group. This also lets EKS scale up your node group from the desired size in high-demand periods.
> 
> Kubernetes, being a container orchestration platform, uses these settings to automatically adjust the number of nodes based on the demands of your application. You can always edit these settings if you want your node group to be bigger or smaller!



-   Once a few minutes have passed since you've terminated your nodes, refresh the **EKS** console again.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_38.png)

  ![Screenshot 2025-05-16 235313](https://github.com/user-attachments/assets/6064a00a-4dad-4b4b-b05b-1354f11562d7)

-   You'll notice that there are new nodes again! 🤯
    
-   Head back to the **EC2** console.
    
-   Refresh the EC2 **Instances** page.
    
-   You'll notice that new instances were launched to replace the terminated ones.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_39.png)

  ![Screenshot 2025-05-16 235655](https://github.com/user-attachments/assets/54420ef0-e49c-4d24-96d6-6f9551abebc6)


----

### Nice Work!

  

You've just launched your first Kubernetes cluster on AWS!

Give yourself a pat on the back – that's no small feat.

![Yup - you did all that!](https://learn.nextwork.org/projects/static/aws-compute-eks1/architecture-complete.png)

Yup - you did all that!

You've learned how to:

-   🌠 Launch and connect to an **EC2** instance.
    
-   🛠️ Install and use **eksctl** to create an EKS cluster.
    
-   ☁️ Track cluster creation using **CloudFormation**.
    
-   🔑 Manage **IAM** access policies.
    
-   💎 (Secret Mission) Test the resilience of your cluster by terminating nodes.
    
  
Well done on making start as a Kubernetes pro. See you in the next part of this series, where your cluster will start running container images and have a load balancer handling traffic!

------
## Set Up Kubernetes Deployment

#### Prepare an app's backend for deployment with Kubernetes!

COST

$0.30 USD (for EKS)

![Tool icon](https://learn.nextwork.org/static/tool.svg)

WHAT YOU'LL NEED

-   An AWS account -  [Create one here!]([AWS Console - Signup](https://signin.aws.amazon.com/signup?request_type=register))

KEY CONCEPTS

-   [Amazon Elastic Kubernetes Service Documentation](https://docs.aws.amazon.com/eks/)
-   [Amazon ECR]()
-   [Git & GitHub]()
-   [Amazon EC2]()

Now, picture this: a team member just developed an entire application and shared the GitHub repository of the app's **backend.**

Are you ready to pull the app's backend from GitHub and prepare it for deployment with Kubernetes? Let's go!

  ![](https://learn.nextwork.org/projects/static/aws-compute-eks2/architecture-complete.png)

**By the end of this project, you will...**

-   📥 Clone a backend application from **GitHub**.
    
-   💿 Build a **Docker** image of the backend.
    
-   🗃️ Push your image to an **Amazon ECR** repository.
    
-   🤯 Troubleshoot **installation and configuration errors** - as a PRO student, get ready to face errors head-on and push your skills to the next level.
    
-   💎 (Secret Mission) Dive into the **backend code** on GitHub.


---


### Set up EC2 and EKS

  

Let's kick things off by setting up our environment! We'll launch an EC2 instance, which is where we'll send commands to **EKS** and other tools. Then, we'll create our EKS cluster.

> **💡 What is EKS?**  
> **Amazon EKS (Elastic Kubernetes Service)** is a service that helps you run Kubernetes on AWS.
> 
> Setting up Kubernetes from scratch can be quite a time consuming and complex thing to do, because you'd need to configure Kubernetes' networking, scaling, and security settings on your own. Amazon EKS handles these tasks for you and helps you integrate Kubernetes with other AWS services.

If you get stuck in this step, check out the [first project of this Kubernetes series]() for a detailed explanation of each part.

  
  

**In this step, you're going to:**

-   Launch and connect to an EC2 instance.
    
-   Set up **eksctl** and your instance's AWS credentials.
    
-   Create an EKS cluster.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/architecture-1.0.png)

  



  
  

Log into the AWS Management Console [as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)

  
  

**Launch and Connect to an EC2 Instance**

-   Head to the `EC2` console.
    
-   Check that you're using the **AWS Region** that's closest to you.
    
-   Click **Launch instances**.
    
-   Name your EC2 instance `nextwork-eks-instance`
    
-   For the **Amazon Machine Image,** select **Amazon Linux 2023 AMI.**
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_15.png)

  

-   For the **Instance type,** select **t2.micro.**
    
-   In the **Network settings** section, we'll keep the default security group for now.
    

> 💡 **Extra for PROs: Is using the default security group security best practice?**  
> We wouldn't do this for production environments or long-term use. For now, the default security group makes it easier to use **EC2 Instance Connect** when we connect to our EC2 instance.
> 
> If we don't use the default security group, we'd have to manually edit our instance's inbound rules to let in Instance Connect's range of IP addresses, which is different depending on your AWS Region.
> 
> Feeling up for a challenge? Try editing your security group settings to make it more secure (while letting you use EC2 Instance Connect later on). If you get stuck, [ask the NextWork community!](https://community.nextwork.org/c/i-have-a-question/?topics=7611)

-   Select **Launch instance.**
    
-   A pop up appears! Can you tell whether you need a key pair?
    
-   Select **Proceed without a key pair (not recommended).**
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_1.png)

  

-   Select **Launch instance.**
    
-   In your EC2 console's **Instances** page, select your new instance.
    
-   Select **Connect**. Welcome to **EC2 Instance Connect!** This is a convenient way to access your instance directly from your browser.
    
-   Select **Connect** again in your EC2 Instance Connect page.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_14.png)

  

  
  

**Install eksctl**

> **💡 What is eksctl?**  
> **eksctl** is a command-line tool for working with **Amazon EKS**.
> 
> We're using eksctl because it's one of the simplest ways to create Amazon EKS clusters. You end up running much fewer commands compared to using AWS CLI, because eksctl detects the resources you'll need and automates the environment setup e.g. creating networking resources.

-   Run the following command in your EC2 instance's terminal to download, extract, and install eksctl.
    


```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv -v /tmp/eksctl /usr/local/bin

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_4.png)

  

-   Verify that you've installed eksctl:
    



```bash
eksctl version

```

-   You should spot a version number in the terminal output.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/eksctl.png)

  

> **🙋‍♀️ I don't see a version number**  
> Try running command to install eksctl again. Make sure there aren't any errors in the terminal response.


  
  

**Create an IAM role for your EC2 Instance**

> **💡 Tip:** If you've created `nextwork-eks-instance-role` (an IAM role) in the previous project, jump straight to **⭐️ Attach IAM role to EC2 instance** in this step.

-   Head to the `IAM` console.
    
-   Select **Roles**.
    
-   Select **Create role.**
    
-   Under **Trusted entity type,** select **AWS service** to tell AWS that we're setting up this role for a AWS serice (Amazon EC2).
    

> **💡 Why do we need to set up an IAM role?**  
> Your EC2 instance starts off as a blank slate, so it doesn't actually have the permission to do anything in your AWS account yet! Your instance would fail to use eksctl to create any EKS clusters.
> 
> You need to give your instance the **permission** to work with AWS services, and you can grant this using roles.

-   Under **Use case,** select **EC2.**
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_8.png)

  

-   Select **Next.**
    
-   Under **Permissions policies,** we'll grant our EC2 instance **AdministratorAccess.**
    

> 💡 **Extra for PROs: Is granting AdministratorAccess best practice?**  
> Great question! Granting AdministratorAccess is powerful but not ideal for long-term use. We’re using it now because we don’t know _all_ the services your EC2 instance will access for this project yet.
> 
> In a real-world scenario, you’d follow the **principle of least privilege**—giving user/services/apps just enough permissions for the job to minimize security risks.

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_7.png)

  

-   Make sure the **AdministratorAccess** option is checked, and select **Next**.
    
-   Let's give this role a straightforward name - `nextwork-eks-instance-role`
    
-   Enter a short description:
    


```text
Grants an EC2 instance AdministratorAccess to my AWS account. Created during NextWork's Kubernetes project.

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_6.png)

  

-   Select **Create role.**
    

  
  

Great! Your new role is born. Now we'll add this role to our EC2 instance.

  
  

**⭐️ Attach IAM role to EC2 instance**

-   Head back to the **Amazon EC2** console.
    
-   Select **Instances** from the left hand sidebar.
    
-   Select the checkbox next to your **nextwork-eks-instance** EC2 instance.
    
-   Select the **Actions** dropdown, and then **Security** -> **Modify IAM role.**
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks1/processed_image_20.png)

  

-   Under **IAM role,** select your new `nextwork-eks-instance-role` role.
    
-   Select **Update IAM role**.
    

  
  

**Create EKS Cluster**

-   Back to **EC2 Instance Connect,** run the following command to create your EKS cluster.
    
-   Make sure to replace `YOUR-REGION` with your AWS region's code e.g. us-west-2:
    



```bash
eksctl create cluster \
  --name nextwork-eks-cluster \
  --nodegroup-name nextwork-nodegroup \
  --node-type t2.micro \
  --nodes 3 \
  --nodes-min 1 \
  --nodes-max 3 \
  --version 1.31 \
  --region YOUR-REGION

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_3.png)

  

-   Check: Have you replaced `YOUR-REGION` with your AWS region's code?
    
-   Creating your EKS cluster can take some time (around 15-20 minutes), so let's do something else in the meantime...
    





### Pull the Code for your Backend

  

Now that our EKS cluster is spinning up, let's find the app **backend** that we want to deploy. Your team member has pushed the backend code into GitHub repository, so let's start there!

> 💡 **What is 'backend'?**  
> The **backend** is the "brain" of an application. It's where your app processes user requests and stores and retrieves data. Unlike frontend code, which is what users see and interact with, backend code works on the server side (i.e. in the background) to make sure your app behaves as expected (e.g. loads a new page) when a user does things like clicking on buttons.

**In this step, you're going to:**

-   Install Git.
    
-   Make a copy of application code from GitHub.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/architecture-2.0.png)

  



-   While your EC2 instance is busy with creating your cluster, head back to the **EC2** console.
    
-   Select your EC2 instance **nextwork-eks-instance-role**, and select **Connect** again.
    
-   Start a new **EC2 Instance Connect** session with your instance.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_5.png)

  ![Screenshot 2025-05-17 001551](https://github.com/user-attachments/assets/a0889be7-cf61-43dd-981e-1f823d4c9c11)

> 💡 **Woah, I can connect to the same instance twice... at the same time?**  
> It's true—you can open multiple SSH sessions to the same EC2 instance at the same time.
> 
> This can be super helpful when you want to multitask or monitor logs while running commands in another session. And don’t worry, it doesn’t pause any progress in your other windows.

  
  

Let's clone our team member's backend repository.

> **💡 What does cloning mean?**  
> When we say "clone a repository," we mean creating a full copy of a repository's code stored remotely (in this case, in GitHub) to your machine (in this case, our EC2 instance).
> 
> This way, you get access to all the files and code without having to manually copy and paste.
> 
> If you're new to Git and GitHub, check out our [Connect a GitHub Repo with AWS](https://learn.nextwork.org/projects/aws-devops-github) project.

-   In a new tab, visit your [team member's GitHub repository](https://github.com/NatNextWork1/nextwork-flask-backend).
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/github-repo.png)

  

-   Select **Code** to reveal the instructions for cloning their repository.
    
-   Copy the **HTTPS** URL.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/github-code.png)

  

-   Head back to your **EC2 Instance Connect** tab.
    
-   In the terminal, run the command to clone your team member's repository. Replace `[GITHUB-URL]` with the HTTPS URL you've copied:
    



```bash
git clone [GITHUB-URL]

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_11.png)

  

-   Whoops! You'll probably get an error here...
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_6.png)

  ![Screenshot 2025-05-17 001551](https://github.com/user-attachments/assets/a0889be7-cf61-43dd-981e-1f823d4c9c11)

> **💡 What is this error about?**  
> The terminal response `"Git command not found"` means you don't have **Git** installed in your EC2 instance. You'll need to install it first to clone a GitHub repository.
> 
> **Tip:** It's helpful to note that "command not found" typically means you haven't installed the tool you're trying to use!

-   Install Git:
    



```bash
sudo dnf update
sudo dnf install git -y

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_7.png)

  ![Screenshot 2025-05-17 003128](https://github.com/user-attachments/assets/0ca0aea3-ca2b-4899-83e9-012cdef27c75)

![Screenshot 2025-05-17 003404](https://github.com/user-attachments/assets/8767fe67-095f-4be7-b8bf-8c1043e58cc8)

-   Verify you've downloaded Git by checking for its version:
    



```bash
git --version

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_8.png)

  ![Screenshot 2025-05-17 002128](https://github.com/user-attachments/assets/cc491e76-9b24-4ea6-a4f3-affac65b3e90)


-   Configure Git by running the command below. Make sure to replace the placeholder values with your name and email:
    



```bash
git config --global user.name "username"
git config --global user.email "yourname@gmail.com"

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_10.png)

  

-   _Now_ we should be able to clone the repository:
    
![Screenshot 2025-05-17 002128](https://github.com/user-attachments/assets/cc491e76-9b24-4ea6-a4f3-affac65b3e90)



```bash
git clone https://github.com/NatNextWork1/nextwork-flask-backend.git

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_11.png)

 ![Screenshot 2025-05-17 002308](https://github.com/user-attachments/assets/3422acc8-65fd-4290-9bda-108982db4063) 

> **💡 What am I cloning?**  
> You are cloning the **nextwork-flask-backend** repository from GitHub. This repository contains all the backend code needed for your application, including files like app.py, Dockerfile, and requirements.txt.
> 
> By **cloning** this repository, you're copying all the code and resources onto your EC2 instance so you can build, run, and deploy the backend part of your project.
> 
> Once you've cloned it, the project will look like a new folder in your EC2 instance with the entire project's files inside.



-   Run `ls`, which is the Linux command to list all files and subdirectories in your current directory.
    
-   Confirm that you have a new folder called `flask-backend` in your EC2 instance now.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_58.png)

![Screenshot 2025-05-17 002527](https://github.com/user-attachments/assets/3f69d7ab-f450-4f62-95aa-0bc154617554)  

> **💡 Why does the repository name say 'flask'?**  
> The repository is named with `flask` because the backend code is built using **Flask**, a web framework for Python that developers use to create backend services or APIs quickly. It's called a "framework" because Flask comes with templates for building web applications, making it easier to create features like handling HTTP requests managing databases.
> 
> **Tip:** You'll explore the backend code in depth in this project's Secret Mission 💎

Nice work, seeing the folder means you've successfully cloned your team member's backend code!



---



### Build a Container Image for Your Backend

  

Great, we've got our team member's code sitting in our EC2 instance.

On to deployment?! 👀

Oooo not so fast. When you deploy a containerized app to Kubernetes, Kubernetes **needs** to pull the app from a **container image** that it can access.

> **💡 What is a container image?**  
> A **container image** is like a blueprint that contains all the instructions, code, libraries, and dependencies needed to run the application. Note that on the other hand, a **container** is the running instance created from that image, bringing the application to life and running it in an environment.

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/kubernetes-comic1.png)

  

**In this step, you're going to:**

-   Build a container image of the backend.
    
-   Resolve four **installation and configuration errors** 🤯 You're a PRO so you've absolutely got this - you could even challenge yourself to solve some of them without the guide!
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/architecture-3.0.png)

  


-   To build a container image, run the following command in your EC2 instance's terminal:
    



```bash
docker build -t nextwork-flask-backend .

```

> 💡 **What does building an image mean?**  
> When your team member prepared the app's backend, they wrote a file called a **Dockerfile** and stored it inside the GitHub repository that they shared with you. A Dockerfile contains instructions on how to build a container image that packages up an app (in this case, the backend) and all its dependencies.
> 
> **Building an image** means you're creating a container image using the Dockerfile that your team member prepared. When you ran the `docker build` command, you were asking Docker to read the instructions in the Dockerfile and build the container image for you accordingly.
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-eks2/kubernetes-comic2.png)
> 
>   
> 
> The container image lets Kubernetes set up multiple, identical containers so your application runs consistently across different environments. Whether you're deploying in development, testing, or production, your app behaves the same way because Kubernetes refers to your image each time a new instance/node needs to be created.
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-eks2/kubernetes-comic3.png)
> 
>   
> 
> 💡 **What do these commands do?**  
> `-t nextwork-flask-backend` names your container image `nextwork-flask-backend`, and the `.` tells Docker to find the Dockerfile in the current directory.



-   Yikes! An error...
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_64.png)

  

> **💡 What is this error about?**  
> Remember what a "command not found" error usually tells you?
> 
> Building a container image using Docker won't work as Docker isn't installed in your EC2 instance yet.

  
  

**Install and Configure Docker**

-   Install Docker:
    


```bash
sudo yum install -y docker

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_63.png)

  

> **💡 What is Docker?**  
> Docker is the tool we're using to **build** a container image of our backend. In general, you'd use Docker to create containers and container images, while Kubernetes coordinate multiple containers (clusters) running the same/related applications.
> 
> If you're new to Docker or container images, check out our [intro project to Docker!](https://link.nextwork.org/projects/aws-compute-eb?utm_source=project-app)

-   Start Docker:
    



```bash
sudo service docker start

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_18.png)

![Screenshot 2025-05-17 003452](https://github.com/user-attachments/assets/f12c259e-2909-4083-92a4-429384aaa449)  

**Build the Docker Image**

-   Run the command to build your container image again:
    



```bash
docker build -t nextwork-flask-backend .

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_21.png)

  ![Screenshot 2025-05-17 003526](https://github.com/user-attachments/assets/033acb31-ba29-43e1-861a-aa5f26ba4c72)

> **💡 What! What's the error this time**  
> The command fails because **ec2-user**, which is the user you've used to access this instance, doesn't have permission to run Docker commands. When Docker was installed, it was set up for the **root** user.
> 
> The previous Docker commands you ran worked because they're prefixed with `sudo`, which lets a non-root user run commands with root user rights. But, it's good practice to give your ec2-user the permission instead of using `sudo` each time.
> 
>   
> 💡 **Why am I logged in as ec2-user instead of the root user?**  
> When you launch an EC2 instance using certain AMIs like Amazon Linux, the default user for SSH access is **ec2-user.** This user comes pre-set up with the AMI as a normal user that's allowed to have root user privileges if you run a command with `sudo`.
> 
> When you access your instance as ec2-user, it’s like logging into an AWS account as an IAM admin user—you’ve got a lot of control but not _the_ absolute top level unless you're using `sudo`. If you need to run Docker commands, those require root privileges because Docker needs root-level access to create containers or build container images.



-   To confirm which user you're using in the terminal, run the command `whoami`
    
-   You should see **ec2-user** in the terminal response.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_57.png)

  ![Screenshot 2025-05-17 004112](https://github.com/user-attachments/assets/39e0c173-2700-4d98-8dad-d53cfa331933)

-   Add **ec2-user** to the **Docker** group:
    



```bash
sudo usermod -a -G docker ec2-user

```

> 💡 **What is the Docker group?**  
> The Docker group is a group in Linux systems that gives users the permission to run Docker commands. By default, only the root user can run Docker commands. When you add a user (e.g., ec2-user) to the Docker group, it lets that user run Docker commands without typing `sudo` every time.
> 
>   
> 💡 **What does this command do?**  
> The command `sudo usermod -a -G docker ec2-user` adds the **ec2-user** to the **docker** group.
> 
> -   `usermod` is used to **modify** a user's account in the system. It allows you to update attributes like their groups, home directory, login name, and more.
>     
> -   The `-a` flag (**append**) makes sure your user doesn't get removed from any other groups they might already belong to. Without `-a`, the user would be removed from all groups not listed in the command.
>     
> -   The `-G` flag (**group**) specifies the groups a user should be added to. In this case, it's the docker group.
>     



-   Restart your **EC2 Instance Connect** session by refreshing your current tab.
    

> 💡 **Why are we refreshing our tab?**  
> User group changes don’t take effect until you start a new session, so reconnecting to your EC2 instance makes sure your **ec2-user** picks up the new `docker` group permissions.

![Good as new](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_22.png)

Good as new

  

-   Make sure your ec2-user has been added to the Docker group:
    



```bash
groups ec2-user

```

> 💡 **What does this command do?**  
> This command will list all the groups that ec2-user is a part of.
> 
> If you see `docker` listed, then ec2-user is in the Docker group and can run Docker commands without using `sudo`. Nice work!

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/ec2-user.png)

  

-   Can you run the command to build your Docker image now? You can press the **up arrows** (⬆) in your keyboard until you get the command pre-filled in your terminal.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_23.png)

![Screenshot 2025-05-17 004112](https://github.com/user-attachments/assets/39e0c173-2700-4d98-8dad-d53cfa331933)  

> 💡 **Ooof, another error!**  
> Yup! Your command won't work because your terminal needs a Dockerfile to build a container image, but it can't seem to find one right now...

-   Run `ls` to find your subdirectories.
    

> 💡 **What are the results telling me?**  
> The terminal is showing us the directories and files from our EC2 instance's root directory. In this case, we see a subdirectory called **nextwork-flask-backend.**
> 
> This is the cloned GitHub repository that contains our backend application code and its related files, like the Dockerfile. To build the Docker image, we need to navigate our terminal **into** the nextwork-flask-backend subdirectory. Otherwise, Docker can't find a Dockerfile to build your container image.

-   Can you tell what you'll need to do to build your Docker image now?
    
-   Navigate to the application directory, which contains the Dockerfile:
    



```bash
cd nextwork-flask-backend

```

-   Run `ls` to see the contents inside nextwork-flask-backend.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_61.png)

  

-   Nice - the terminal should show you all the files inside nextwork-flask-backend, which should include the Dockerfile.
    
-   Run the command to build your Docker image again:
    



```bash
docker build -t nextwork-flask-backend .

```

-   Phew! The command works now. Watch your terminal update as Docker builds the container image.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_24.png)

  ![Screenshot 2025-05-17 004627](https://github.com/user-attachments/assets/84496806-6357-474a-a895-b8f61ed6bc91)

----

## 🫸 Step #4

### Push Your Container Image to Amazon ECR

  

Now that your container image is all built, where should Kubernetes find your container image?

**Container registries,** like **Amazon Elastic Container Registry (ECR),** are storage spaces for container images. They give container images somewhere to live so they can be accessed by Kubernetes/other services.

> 💡 **Recap: Why are we using Docker and ECR?**  
> We’re using Docker to package up the backend and then pushing that container image to Amazon ECR (Elastic Container Registry). When it's time for Kubernetes to deploy your application, Kubernetes can just pull the image directly from ECR.
> 
> This setup is the standard way for deploying containerized apps with Kubernetes (instead of deploying code on your local machine) because it helps with consistency and scaling.

**In this step, get ready to:**

-   Store the Docker image of your backend in ECR.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/architecture-3.0.png)

  
![Screenshot 2025-05-17 005135](https://github.com/user-attachments/assets/44c15af7-b715-4e7f-90dc-fe8fb8affb43)



-   Create a new Amazon ECR repository using this command:
    
![Screenshot 2025-05-17 005217](https://github.com/user-attachments/assets/17544337-a662-4c7a-94e5-7f510d2bab3d)



```bash
aws ecr create-repository \
  --repository-name nextwork-flask-backend \
  --image-scanning-configuration scanOnPush=true \

```

> **💡 Why are we using ECR?**  
> **Amazon ECR (Elastic Container Registry)** is a container registry service by AWS, which means you use it to securely store, share, and deploy container images.
> 
> ECR is an excellent choice for storing your container image because it's an AWS service, which lets Elastic Kubernetes Service (EKS) deploy your container image with minimal authentication setup.
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-eks2/deploying_plan.png)
> 
>   
> 




![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_12.png)

![Screenshot 2025-05-17 005348](https://github.com/user-attachments/assets/d9c316b8-aa36-4fff-8003-cb78d982adc0)
  

> 💡 **Woah! What does the terminal's response mean?**  
> This response confirms that your ECR repository has been created - it's ready for you to push Docker images!
> 
>   
> 💡 **Extra for PROs: Here's a breakdown of the terminal response**
> 
> -   `repositoryArn`: The Amazon Resource Name (ARN) i.e. unique ID for your ECR repository.
>     
> -   `repositoryUri`: This is the URL you'll use to push and pull container images. It shows where your images will be stored.
>     
> -   `repositoryName`: The name you've given to your repository—in this case, **nextwork-flask-backend**.
>     
> -   `imageTagMutability`: Whether image tags are mutable or immutable. "MUTABLE" means you can overwrite which image has a tag e.g. the **latest** tag can be taken by a newer image at any time.
>     
> -   `imageScanningConfiguration`: Whether images will be scanned for vulnerabilities when pushed.
>     
> -   `encryptionConfiguration`: Your images are encrypted using AES256 for security.
>     

-   In a new tab, head to the `ECR` console.
    
-   Confirm that you can see a new repository called **nextwork-flask-backend**!
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_19.png)

  ![Screenshot 2025-05-17 005408](https://github.com/user-attachments/assets/a11adc3d-fb84-4eda-ba8a-2f07284da615)

Nice, our Amazon ECR repository is live. We're ready to push our container image into ECR!

  
  

**Push your container image to ECR**

-   Select your new repository.
    
-   Select **View push commands**.
    

> **💡 What is a push command?**  
> A push command in Amazon ECR is used to upload your Docker container images to an ECR repository.

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_18.png)

  

-   Copy the first command.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_24.png)

![Screenshot 2025-05-17 005500](https://github.com/user-attachments/assets/bed71ada-be44-44f0-a1bc-7dc1581c1bfe)  

-   Run the command in your EC2 Instance Connect window.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_19.png)

  
  
![Screenshot 2025-05-17 005715](https://github.com/user-attachments/assets/234aea21-9ae5-494b-ac10-8aec7d2c44aa)

-   Head back to your **ECR** console's push commands window.
    
-   We've already built out container image so we can skip the second command.
    
-   Copy the last two push commands.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_23.png)

  
![Screenshot 2025-05-17 005500](https://github.com/user-attachments/assets/bed71ada-be44-44f0-a1bc-7dc1581c1bfe)

-   Run the last two in your EC2 Instance Connect terminal to tag and push your container image.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_26.png)

  

> **💡 What do tagging and pushing the image do?**  
> Since your ECR repository can hold many versions of the same container image, tags help you keep things organized. **Tagging** your Docker image is like giving it a nickname so you can easily refer to a specific version.
> 
> Here, we're tagging our Docker image with **latest** so Kubernetes knows where it can find the right container image version when it’s time to deploy.
> 
> Pushing uploads the tagged image to a remote repository. In our case, we've just uploaded our container image to our ECR repository!

-   Head back to the **ECR** console.
    
-   Close the push commands window.
    
-   Select the refresh button to refresh your console.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_22.png)

  

-   Wooo! Confirm that a new container image is in your console now.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_21.png)

   ![Screenshot 2025-05-17 005954](https://github.com/user-attachments/assets/75db1f4c-c277-4507-9ea1-cafe90dbb4b5)

> 💡 **Does Kubernetes only run containerized applications from a repository?**  
> Nope, Kubernetes doesn’t _have_ to pull container images from a remote repository like ECR or Docker Hub.
> 
> But using a container registry is a great way to deploy containerized apps. Your cluster can pull whatever is the **latest** image in your repository on demand, which makes deployments stay consistent across all nodes automatically.
> 
> If you didn't use a container registry, you’d need to preload every node in your Kubernetes cluster with the image. You'd also need to update each node manually with every change to your container image.

---
## 💎 Secret Mission

### Dive into the Backend Code

  

Welcome to your 🤫 exclusive 🤫 secret mission.

Your mission, should you choose to accept it, is to explore the backend repository you cloned. By the end of this mission, you’ll truly know what was inside the Docker image you built and pushed in this project.

  
  

**💎 In this secret mission, get ready to:**

-   Open the backend repository on GitHub.
    
-   Explore the three files that make up the backend.
    
-   Showcase your secret mission in your **project documentation.**
    

> 💎 **Congratulations** - Secret Mission unlocked!

It's time for a little exploration into the backend code 🧙



  
  

-   To show you what the backend does, imagine that your team member sends you a link to **Search Hacker News** and asks you to enter a search query in there.
    

> 💡 **What is Search Hacker News?**  
> [**Hacker News**](https://news.ycombinator.com/news) is an online platform and community where you can read and discuss tech-related news and industry trends.
> 
> **Search Hacker News** is the Hacker News platform's search engine. You'd use it to quickly find relevant content based on your search terms.

-   Open this link to Search Hacker News in a new tab, which already has the search query `aws` pre-filled: [https://hn.algolia.com/?q=aws](https://hn.algolia.com/?q=aws)
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_54.png)

![Screenshot 2025-05-17 010314](https://github.com/user-attachments/assets/9998b4b4-4215-45eb-b36d-1f2405d67b3a)


-   Now try changing the `aws` part of the URL to other topics like `cloud` or `amazon` to see different results.
    

  
  

Your coworker explains that the backend app is a tool that:

1.  Takes a user’s input (e.g. `aws`).
    
2.  Runs the input as a search query in Hacker News Search.
    
3.  Processes the search results and formats them into JSON data.
    

  
  

Although we haven't seen the JSON output from our backend yet (since we haven't deployed it), using Search Hacker News now gives you an idea of the type of data the backend will produce.

So how does the backend code do all this? 🤔

Let's find out.

  
  

**Explore the Code**

-   Open the [backend GitHub repository](https://github.com/NatNextWork1/nextwork-flask-backend.git) in your browser.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_50.png)

  

> 💡 **What's in this GitHub repository?**  
> This GitHub repository holds all the source code for your app’s backend.
> 
> There are three main characters in your backend app's code:
> 
> 1.  **requirements.txt** lists the dependencies your app needs.
>     
> 2.  The **Dockerfile** provides a set of instructions for building a Docker image for your app.
>     
> 3.  **app.py** is the core of your backend. It contains the actual code that determines what your app does and the kind of responses it sends back to the client.
>     

-   Look at **requirements.txt**. This file lists the dependencies your application needs to run properly.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_53.png)

  

> 💡 **Extra for PROs: Can you break down the dependencies in requirements.txt?**
> 
> -   `Flask==2.1.3`: **Flask** is the web framework used to build the backend code, which you'll see in **app.py.**
>     
> -   `flask-restx==0.5.1`: Our app creates an **API** using an extension **Flask-RESTx** so that users or other applications can make requests to our backend.
>     
> -   `requests==2.28.1`: The **Requests** library is used to get data from the Hacker News **API**.
>     
> -   `werkzeug==2.1.2`: **Werkzeug** helps Flask handle application-level routing. For example, when a user/service makes a request to our backend, Flask uses its routing system (powered by Werkzeug) to direct that request to the right function in app.py, which then processes the request and responds to it.
>     

-   Select the **Dockerfile**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_51.png)

  

> 💡 **What does this Dockerfile do?**  
> The Dockerfile defines how a Docker image of the backend should be built.
> 
> Notice the contents of this file and how it builds your Docker image step-by-step.
> 
> When we talk about the benefits of using container images and containers—such as consistent, reliable deployment across different environments—these commands in a Dockerfile are exactly what make the magic happen!
> 
> It installs the necessary dependencies, copies the application code, and sets up the commands a container needs to run to start your Flask app.
> 
>   
> 💡 **Can you break down the commands in this Dockerfile?**
> 
> -   `FROM python:3.9-alpine` sets up the environment for your app by using **Python 3.9** on Alpine Linux, which is a very lightweight version of Linux. This keeps your app size small, making it faster to build and run.
>     
> -   `LABEL Author="NextWork"` adds **author** metadata to the image.
>     
> -   `WORKDIR /app` sets `/app` as the **working directory** in the container, so the commands in the rest of this Dockerfile will be run from there.
>     
> -   `COPY requirements.txt requirements.txt` copies the **requirements.txt** file from your local machine (i.e. your EC2 instance) into the container's /app directory.
>     
> -   `RUN pip3 install -r requirements.txt` installs the dependencies in **requirements.txt**.
>     
> -   `COPY . .` copies all the files from your current directory i.e. **requirements.txt** and **app.py** into the **/app** directory in the container.
>     
> -   `CMD ["python3", "app.py"]` says the container should run the command `python3 app.py` to start your Flask app.
>     



-   Now select **app.py**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_52.png)

  

> 💡 **What's happening in app.py?**  
> **app.py** is the main code for your backend. It has three main parts:
> 
> 1.  **Setting up the app and routing:** The code starts by importing the Flask framework and tools for creating an API. It defines a route (`/contents/<topic>`) that directs incoming requests to the SearchContents class. This means users visiting your backend will need to visit a URL that ends with `/contents/<topic>` to see any results
>     
> 2.  **Fetching data:** In the **SearchContents** class, the `get()` method extracts the topic from the URL, sends a request to the Hacker News Search API to find related content, and collects important details like id, title, and url.
>     
> 3.  **Sending the response:** The collected data is turned into a formatted JSON response.
>     
> 
>   
> 💡 **What is an API?**  
> An API (Application Programming Interface) is like a bridge that lets different programs talk to each other. It lets one app to ask for data or services from another and get a response.
> 
> For example, when our backend app runs a search using the Hacker News Search API, it sends a request, gets data back, and processes it into JSON format to return to the user. This helps different parts of software work together easily.
> 
> In our own backend app, **we also create our own API** using Flask. This API takes user input, connects to the Hacker News API to get the data, processes that data, and then sends it back as JSON.
> 
> APIs make it easy for our backend to collect data from Hacker News and then share information back to our users and other services.9



Phew, that's the backend code investigation all done!

Let's wrap up with a quick summary:

1.  Your app's backend **fetches data** based on a search topic you enter.
    
2.  The backend code uses **Flask** to connect with an **external API** (Hacker News Search API) and process the data.
    
3.  The backend then sends the data back as formatted JSON.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/api-plan.png)

  

You've just learnt how to set up your app for deployment with Kubernetes 🤯

That's awesome! Give yourself a pat on the back.

You've learned how to:

-   👩‍💻 Use Git to pull the code for the backend of your app.
    
-   🐳 Build a Docker image of the backend.
    
-   💿 Push Docker image to ECR.
    
-   🕵️ Troubleshoot installation and configuration issues.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/architecture-complete.png)

  

In the **next project** of this Kubernetes series, you'll **deploy** the backend to see your work come to life in a live app!

  
----

## Create Kubernetes Manifests

Introducing the key to Kubernetes deployments - manifest files!

COST

$0.30 USD (for EKS)

![Tool icon](https://learn.nextwork.org/static/tool.svg)

WHAT YOU'LL NEED

-   An AWS account -  [Create one here!]()
-   [Launch Kubernetes Clusters with EKS]()

KEY CONCEPTS

-   [Amazon EKS]()
-   [Amazon ECR]()
-   [Git & GitHub]()
-   [Amazon EC2]()

Now, it's time to create the key files called **manifests** that tells Kubernetes how to **deploy** and **manage** your containerized backend!

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/architecture-complete.png)

**By the end of this project, you will...**

-   🛫 Set up a **Deployment manifest** that tells Kubernetes how to **deploy** your backend.
    
-   🚚 Set up a **Service manifest** that tells Kubernetes how to **expose** your backend to your users.
    
-   💎 (Secret Mission) Dive into the details of your manifest files and discover new learnings!

----


### Set Up Your App for Deployment

  

With our image safely stored in ECR, we're ready to deploy our application to our EKS cluster. We'll use **Kubernetes manifests** to tell Kubernetes how we want it to deploy our application.

> 💡 **What are Kubernetes manifests?**  
> Just like a Dockerfile tells Docker how to build a container image, **Kubernetes manifest files** tell Kubernetes how to run your application in a cluster.
> 
> They act as blueprints that define the desired state of your app, including which container images to use and how to make your app available to end users or other services.

**In this step, you're going to:**

-   Create the **Deployment manifest,** which gives Kubernetes instructions on deploying your containerized backend to your Kubernetes cluster.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/architecture-5.0.png)

  



  
  

**Create Kubernetes Manifest Files**

-   Create a new directory from your instance's root called **manifests**. Run the following commands:
    



```bash
cd ..
mkdir manifests
cd manifests

```

![Screenshot 2025-05-17 013343](https://github.com/user-attachments/assets/f38a50ef-3e4e-4916-adfe-1284b1ceeb3e)



> **💡 What are Kubernetes manifests?**  
> Think of a **Kubernetes manifest** as a set of instructions that tells Kubernetes how to run your app.
> 
> Manifests are important for deployment because Kubernetes uses this information to know what your app needs, like which containers to run, how many copies to create, and how much memory to allocate.
> 
> Without manifests, Kubernetes wouldn’t know how to set up and manage your app automatically. This means you'd have to manually configure each container every time you deploy, which would be confusing, error-prone, and hard to repeat. Manifests make deployment simple, clear, and consistent.
> 
> **Tip:** In general (even outside of Kubernetes), a **manifest** is an instruction/manual that tells a system how to set up and manage something.
> 
>   
> **💡 What was the command I just ran?**  
> The commands you ran did three things:
> 
> 1.  `cd ..` navigates the terminal out of the amazon-eks-backend folder and back to the root.
>     
> 2.  `mkdir manifests` creates a new directory called **manifests**.
>     
> 3.  `cd manifests` navigates the terminal into the newly created manifests directory.
>     



-   Create the `flask-deployment.yaml` file:
    



```bash
cat << EOF > flask-deployment.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nextwork-flask-backend
  namespace: default
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nextwork-flask-backend
  template:
    metadata:
      labels:
        app: nextwork-flask-backend
    spec:
      containers:
        - name: nextwork-flask-backend
          image: YOUR-ECR-IMAGE-URI-HERE
          ports:
            - containerPort: 8080
EOF

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_28.png)

  ![Screenshot 2025-05-17 013639](https://github.com/user-attachments/assets/63fa9968-c093-454a-97b9-f29f1add9c87)

> **💡 What is a Deployment manifest?**  
> When you **deploy** an app with Kubernetes, Kubernetes' job is to set up and manage several copies of your app across different containers in the cluster.
> 
> A **Deployment manifest** tells Kubernetes exactly how to manage these tasks. It includes details like the how many copies of your app should run across your cluster, and which settings to apply (e.g. CPU limits, container image, or network settings).
> 
> We’re only deploying the backend of our app, but a Deployment manifest can manage multiple components, like frontend servers, databases, and other services; each with its own specific configuration.
> 
>   
> **💡 How does this command create the Deployment manifest?**  
> The `cat` command in Linux is a quick way to see what's inside a file or create a new one without opening a text editor.
> 
> When you use cat with `<< EOF`, like `cat << EOF > flask-deployment.yaml`, you're telling the system: "Take the content I type here and save it in a new file called flask-deployment.yaml."

-   Run `nano flask-deployment.yaml` in your terminal to see your work.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_29.png)

![Screenshot 2025-05-17 013837](https://github.com/user-attachments/assets/556304ff-d5f2-4e0c-b6db-c89f869a0fac)
  

> 💡 **Woah! Where am I, how did that happen?**  
> You’re now in **nano**, a built-in text editor within the terminal! Unlike a regular text editor, nano doesn’t use a mouse – you’ll navigate and edit with the keyboard.
> 
> p.s. nano is a software that usually comes pre-installed in Linux and Unix systems e.g. this EC2 instance. You'd have to install it manually if you'd like to use it in your local Windows computer's terminal!

-   Use the arrow keys on your keyboard to navigate down the file.
    
-   Notice the third to last line... is there anything you should replace?
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_30.png)

  


> 💡 **What does the containers section of this file mean?**  
> The containers section tells Kubernetes how it should set up each container that will run inside the pods created by this deployment. It includes:
> 
> -   The name of the container.
>     
> -   The container image to use.
>     
> -   The ports that the container will use, which lets the application communicate within the cluster and with external traffic.
>     
> 
>   
> 💡 **What should I be replacing 'YOUR-ECR-IMAGE-URI-HERE' with?**  
> You should replace `YOUR-ECR-IMAGE-URL-HERE` with the URI of the Docker image you pushed to Amazon ECR. This lets Kubernetes know where to pull the container image from when it deploys your application.

-   Head back into your **ECR** console, and copy the URI of your image tagged **latest**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_20.png)

  ![Screenshot 2025-05-17 013804](https://github.com/user-attachments/assets/d688022c-50ad-4e1b-8010-c4a65277edb1)

-   Use the arrow keys on your keyboard to get to the correct line, and then replace the placeholder text with the URL you've just copied.
    

> 🙋‍♀️ **Ahh I think I accidentally messed up my file!**  
> All sorts of formatting things can happen when you're using nano, especially if you try to highlight or delete multiple lines!
> 
> To start over, you could select **Ctrl + X** on your keyboard to exit out of the file, and then press **N** on your keyboard to tell nano you don't want to save your changes.

-   Your updated **flask-deployment.yaml** file should look like this:
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_34.png)

  
![Screenshot 2025-05-17 014209](https://github.com/user-attachments/assets/6ab6fab3-755e-46f9-969a-6d8c8e731919)



-   Press **Ctrl + S** on your keyboard to save your work.
    
-   Press **Ctrl + X** to exit out of the file.
    
----


### Create your Service Manifest

  

Woohoo! That was your very first manifest file created. We still have one more...

**In this step, you're going to:**

-   Create the **Service manifest,** which tells Kubernetes how to expose your application and route traffic to it.
    



-   Create the `flask-service.yaml` file:
    



```bash
cat << EOF > flask-service.yaml
---
apiVersion: v1
kind: Service
metadata:
  name: nextwork-flask-backend
spec:
  selector:
    app: nextwork-flask-backend
  type: NodePort
  ports:
    - port: 8080
      targetPort: 8080
      protocol: TCP
EOF

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_32.png)

 ![Screenshot 2025-05-17 014453](https://github.com/user-attachments/assets/d237cbd0-8caf-4c91-b946-5223cc69ae9b)
 

> **💡 What is a Service manifest?**  
> A **Service** in Kubernetes is like a traffic controller that makes sure traffic gets to the right pods inside your app.
> 
> When you create a Kubernetes Service, you're essentially **exposing** your application i.e. making it accessible to network traffic (from within the cluster or from external sources).
> 
> A **Service manifest** tells Kubernetes to create/update a Service using details like which pods to route traffic to, the type of traffic it should handle, and which ports should be used.
> 
> In our case, the Service manifest we created sets up a Service that routes external traffic to port 8080 on pods labeled app: nextwork-flask-backend. This allows traffic from outside the cluster (e.g., your users) to reach your app!
> 
>   
> **💡 What's the difference between the the Deployment and the Service manifests?**  
> The Deployment manifest focuses on **deploying** and managing your app inside Kubernetes, while the Service manifest is what you use to **expose** your app to the outside world or other parts of your system. Both work together to create a fully functional application setup.



Congratulations! You've just learnt how to create your manifest files, which are the final missing pieces for your Kubernetes deployment.

----

## 💎 Secret Mission

### Annotate your Deployment Manifest

  

Welcome to your 🤫 exclusive 🤫 secret mission!

Your mission, should you choose to accept it, is to dive into the details of your Deployment manifest, and share and annotated version back with your team!

  
  

💎 **Get ready to:**

-   Review and annotate your **Deployment manifest.**
    
-   Showcase your secret mission in your **project documentation.**
    

> 💎 **Congratulations** - Secret Mission unlocked!

By annotating your deployment manifest, you'll gain a much deeper understanding of Kubernetes architecture and how Kubernetes deployments work.

There are new concepts and definitions coming your way, but don't forget that exploring new things is all a part of the learning journey. You've got this 💪



**Deployment manifest**

Let’s begin by taking a closer look at your `flask-deployment.yaml` file.

-   Open it in your text editor:
    


```bash
nano flask-deployment.yaml

```

  
  

Welcome back!

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_29.png)

  ![Screenshot 2025-05-17 015213](https://github.com/user-attachments/assets/de425efa-53c7-463b-9397-913b5f308340)


Now that's we're back in our Deployment manifest, let’s go line by line to break it down.

-   Check the first line of the Deployment manifest: `apiVersion: apps/v1`
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_23.png)

  

> **💡 What is `apiVersion`?**  
> `apiVersion` tells Kubernetes which version of its API you’re using to create this resource. Since we’re defining a **Deployment**, we use `apps/v1`, which is the version for managing applications.
> 
>   
> 💡 **What's an API?**  
> An API (Application Programming Interface) is a way for different software components to communicate with each other.
> 
> In Kubernetes, the API is how **you** tell **Kubernetes** what resources to create, update, or delete.
> 
> The **apps/v1** API lets Kubernetes know you’re working with applications. Other options include security policies (`policy/v1`), storage resources (`storage/k8s.io/v1`) and more.

-   Now let's annotate it to remember what it means!
    
-   Move your cursor to the end of the `apiVersion: apps/v1 line`, then add:
    



```text
# Specifies the API version for this Deployment

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_16.png)

  ![Screenshot 2025-05-17 015213](https://github.com/user-attachments/assets/de425efa-53c7-463b-9397-913b5f308340)

> **💡 What does the `#` do?**  
> The `#` in a YAML file is used to add **comments**. Anything written after `#` is ignored by Kubernetes and is not processed as part of the manifest.
> 
> Comments are useful for adding explanations, reminders, or notes about what each part of the manifest does. This helps you (and your team) understand the file better when you revisit it later.
> 
> In this line, we’re using a comment to explain the purpose of the apiVersion line.

Sweet, that's the first one DOWN - not bad at all 😎

-   On to the second line: `kind: Deployment`
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_22.png)

  

> **💡 What is `kind`?**  
> `kind` specifies the type of Kubernetes resource we’re creating, such as a Deployment or a Service.
> 
> `kind` is a key part of a Kubernetes manifest because it sets the tone for how Kubernetes will process the rest of the file. For example, if the kind is **Deployment**, Kubernetes will focus on managing and scaling groups of containers. If the kind is **Service,** Kubernetes will set up networking to expose those groups of containers.

Time to add a comment!

-   At the end of your `kind: Deployment` line, add the following comment:
    



```bash
# This is a Deployment object

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_9.png)

![Screenshot 2025-05-17 015213](https://github.com/user-attachments/assets/de425efa-53c7-463b-9397-913b5f308340)  

Nice work, that's the two of the most important lines ticked off.

That was also the last comment we'll provide for you — we’ll let you take the lead on the rest!

-   Navigate your keyboard to the next section of your Deployment manifest:
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_21.png)

  

> **💡 What is `metadata`?**  
> `metadata` holds details about the resource, like its name and labels to help organize it.
> 
> `name` is the unique name we’re giving to this Deployment. Other metadata fields that could get added in a Deployment manifest are labels (e.g. if you wanted to note that this Deployment manifest is for the production environment, you could add an `environment: production` label), descriptions, or a unique ID you'd like to assing it.
> 
>   
> **💡 What is namespace?**  
> A **namespace** is like a virtual "folder" within a Kubernetes cluster. All resources in Kubernetes belong to a namespace, and namespaces help you organize resources by separating them into different groups.
> 
> In this example, the Deployment is placed in the `default` namespace, which is the built-in, catch-all namespace for resources that don’t belong to a specific group.
> 
> **Extra for PROs:** In real-world examples, you could use namespaces to split resources across teams or environments i.e. 'dev', 'staging' and 'prod' namespaces.

-   Spice up the lines `metadata:`, `name: nextwork-flask-backend` and `namespace: default` with your comments.
    
-   Don't be shy and write whatever comes to mind first. You can always edit your comments later! The most important part is to give it a try.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_10.png)

  ![Screenshot 2025-05-17 015213](https://github.com/user-attachments/assets/de425efa-53c7-463b-9397-913b5f308340)

-   Once you're ready, head to the next section `spec:`
    

> **💡 What is `spec`?**  
> `spec` stands for **specification**. This section is the “blueprint” for how Kubernetes should set up and manage this Deployment.
> 
> The spec section tells Kubernetes things like what type of containers it should use, how many groups of containers it should be running, and any special configurations it needs.
> 
> Importantly, the Deployment uses spec to define the **desired** state of your application, and Kubernetes will constantly work to maintain that state. More on this in the next line!

-   Write your comment next to `spec:`
    
-   Next up, replicas!
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_20.png)

![Screenshot 2025-05-17 015419](https://github.com/user-attachments/assets/6e335172-1dbd-4032-9923-5a5d8c1ac8fe)  

> **💡 What are `replicas`?**  
> **Replicas** are identical copies (or instances) of the app Kubernetes should run. Here, we’re asking for **3 replicas**, which means 3 identical Pods will be created.
> 
> The Deployment is responsible for making sure that if one Pod crashes, a new one is created to **maintain 3 replicas.** Don't forget that anything under the `spec` section defines a **desired** state that Kubernetes will always maintain!
> 
> You can scale up replicas to handle increased traffic or scale down to save resources during low-traffic periods.
> 
>   
> **💡 What is a Pod?**  
> While we've been thinking about a Kubernetes cluster as a bunch of **nodes** running your containerized applications together, you can zoom in and break down a node even further... introducing Pods!
> 
> In Kubernetes, **Pods** are groups of containers that are bundled together so they can work as a unit.
> 
> Pods are the smallest things you can deploy - **you can't deploy containers on their own;** they must be inside a Pod. In more technical terms, this means Pods are the **smallest deployable units** in Kubernetes.
> 
> Containers in a Pod share the same network space and storage so they can communicate and share data more efficiently.

-   Note down your comments for `replicas: 3`
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_11.png)

  

![Screenshot 2025-05-17 015419](https://github.com/user-attachments/assets/6e335172-1dbd-4032-9923-5a5d8c1ac8fe)

-   Now, scroll down to the `selector` section:
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_19.png)

  ![Screenshot 2025-05-17 020027](https://github.com/user-attachments/assets/470d7953-c6e7-4960-a742-0d3ff9da55f3)


> **💡 What is `selector`?**  
> The `selector` acts like a filter. Kubernetes looks for Pods with labels that match the filters you define here, and only the Pods that match all of them will be a part of this Deployment.
> 
> `matchLabels` matches Pods with a specific label (`app: nextwork-flask-backend`). Without `matchLabels`, Kubernetes wouldn’t know which Pods belong to this Deployment!

-   Add your comments for the `selector` section. What do these lines do?
    
-   Take your time and make sure you've written these comments before you move on. Not many left to go 🔥
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_12.png)

  ![Screenshot 2025-05-17 020027](https://github.com/user-attachments/assets/470d7953-c6e7-4960-a742-0d3ff9da55f3)


-   Next, scroll down to the `template` section:
    

> **💡 What is `template`?**  
> The `template` is the blueprint for the Pods that this Deployment will create. It defines exactly how each Pod should look and behave.

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_18.png)

![Screenshot 2025-05-17 020027](https://github.com/user-attachments/assets/470d7953-c6e7-4960-a742-0d3ff9da55f3)
  

> **💡 What is `labels`?**  
> `labels` are tags that help you organize and identify Pods. Here, every Pod will be labeled with `app: nextwork-flask-backend`.
> 
> **Extra for PROs:** Remember `matchLabels` from the previous section? Note that the label created in this section is exactly the same as matchLabels!
> 
> When a Deployment creates new Pods, it uses the `template` section to define the labels for those Pods. If the labels match the matchLabels filter, Kubernetes automatically links those Pods to the Deployment.
> 
> Kubernetes uses this match to monitor and enforce the desired state of the Deployment. For example, if a Pod crashes or is removed, Kubernetes will create a new Pod with the matching labels to replace it.
> 
> If the matchLabels and labels don’t align, the Deployment will try to create and maintain the desired number of Pods, but it won’t manage them correctly because it can’t identify them.

-   Add your comments for the `template` section of the Deployment manifest.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_13.png)

  

-   And finally, we've arrived at the `spec` for the Pods themselves.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_17.png)

  ![Screenshot 2025-05-17 020027](https://github.com/user-attachments/assets/470d7953-c6e7-4960-a742-0d3ff9da55f3)


> **💡 What does `spec` mean here?**  
> You might notice that there was already a `spec` section earlier in this manifest!
> 
> In a Kubernetes Deployment manifest, the two `spec` sections serve different purposes, because they work at two different levels:
> 
> 1.  The first `spec` earlier in this file tells Kubernetes what to do with the Deployment **as a whole**. It defines things like the number of replicas (Pods) in the Deployment, or which Pods the Deployment should manage (via selector). In other words, it works at the Deployment level.  
>       
>     
> 2.  The `spec` you see in this template section is the blueprint for the individual **Pods** that the Deployment will create. It defines what each Pod is running, so it works at the Pod level.
>     
> 
>   
> **💡 What's the difference between the Pod level spec and `template`?**  
> The `template` is the overall blueprint for Pods, think of it as an "outer envelope" that packages the Pod level `spec` together with metadata like labels and names.
> 
> The Pod-level `spec` focuses only on the **containers** and **operational** details of the Pods themselves, such as what’s running inside them and how they behave.

-   Write your comments for the Pod's `spec:`
    





```yaml
    spec:
      containers:
        - name: nextwork-flask-backend
          image: YOUR-ECR-IMAGE-URI-HERE

```

> **💡 What is `containers`?**  
> `containers` define the actual applications running **inside** each Pod:
> 
> -   `name` is the name of the container.  
>       
>     
> -   `image` is the container image that Kubernetes will use to run the app.
>     

-   You've got this - write your comments on the first half of the `containers` section!
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_14.png)

![Screenshot 2025-05-17 020437](https://github.com/user-attachments/assets/7b73d68b-ef88-48d7-9589-57f3575fb13b)  

-   The last bit of the containers section is all about ports:
    



```yaml
          ports:
            - containerPort: 8080

```

> **💡 What is `ports`?**  
> A **port** is like an entry point that allows data to enter or leave an application running inside a container. A container can have many different ports, and each port handles a specific type of traffic.
> 
> In other words, if your container is a house, the ports are doors, and each door leads to a specific app (or part of an app, e.g. the backend). In Kubernetes, ports allow Kubernetes to map incoming traffic to the correct container inside a Pod.
> 
> Typically, a Deployment manifest might have more ports if the app handles multiple types of traffic (e.g., one port for HTTP requests and another for secure HTTPS).
> 
>   
> **💡 What is `containerPort`?**  
> `containerPort` is the port number used by **the app inside the container** to send and receive traffic.
> 
> Here, our backend **listens on** port **8080**, which means it’s ready to receive requests sent to that port. Requests need to specify the correct port to reach the app. If the port is incorrect or missing, the app won’t receive the request.
> 
>   
> **💡 Extra for PROs: How does a request end up at the right port?**  
> Requests are routed to the correct port through a combination of DNS, port numbers, and Kubernetes Services. Here's how it works:
> 
> -   **DNS and IP addressing:**  
>     When you visit a website or make a request, DNS translates the domain name (e.g., `example.com`) to the server's IP address. This makes sure your request is sent to the correct server.
>     
> -   **Port numbers in the request:**  
>     The client (e.g., your browser or API tool) specifies the port number in the request.
>     
>     -   Example: `http://example.com:8080` explicitly tells the system to send the request to port **8080**.  
>           
>         
>     -   If the port is omitted (e.g., `http://example.com`), a default port is used (e.g., **80** for HTTP or **443** for HTTPS).  
>           
>         
> -   **Routing and Services in Kubernetes:**  
>     In Kubernetes, **Services** are responsible for directing traffic to the correct application too.
>     
>     -   Even if external traffic arrives on a different port, you can set up the Service to forward it to the correct **containerPort** inside the container.
>         

-   Finish off your annotations with a comment on the containerPort line 🔥
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_15.png)

  ![Screenshot 2025-05-17 020437](https://github.com/user-attachments/assets/7b73d68b-ef88-48d7-9589-57f3575fb13b)

Wow! That's your Deployment manifest all annotated.

Notice how as we move down the Deployment manifest file, we’re essentially peeling back layers of Kubernetes’ architecture, going from the **API** level all the way down to the **container** level.

1.  At the very top of the file, we’re interacting with the **Kubernetes API**, which is the interface that lets us define resources. At this level, we’re telling Kubernetes, “Hey, I want to create a Deployment using this version of the API.”
    
2.  Then, we’re looking at the big-picture configuration for the entire **Deployment**. How many Pods we need (via `replicas`), which Pods to manage (via `selector`), and how Kubernetes should maintain them. The Deployment makes sure Kubernetes maintains the **desired** state of your app by watching over the Pods it manages and recreating them if they fail.
    
3.  As we move deeper, we reach the `template` section, which defines the blueprint for the **Pods** the Deployment will create.
    
4.  Finally, we reach the core of each Pod: the **containers**. This is where the actual application (in this case, our backend) lives and runs. Our `containers` section defines the image and port for the app inside the Pod.
    

  
  

Take a moment to review the annotations you’ve made.



Great job!

The Deployment manifest and how it describes the desired state of your application is truly a **core** concepts in Kubernetes.

Well done for going above and beyond to understand literally 👏 every 👏 single 👏 piece of it.

  You've just set up **Kubernetes manifest files** for your app's backend deployment!

That's awesome, give yourself a pat on the back 😮‍💨

You've learned how to:

-   🐳 Build and push a **container image** of the backend of your app.
    
-   📝 Write a **Deployment manifests** to tell Kubernetes how to manage and scale your backend app.
    
-   📝 Write a **Service manifests** to tell Kubernetes how to expose your backend app to handle traffic.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/architecture-done.png)

  

Ready to keep learning? In the ** project** of this Kubernetes series, you will **deploy** the backend with Kubernetes using kubectl 🚢

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/architecture-next.png)

  
----

# Deploy Backend with Kubernetes

Welcome to the final project in our Kubernetes x AWS series!

COST

$0.30 USD (for EKS)

![Tool icon](https://learn.nextwork.org/static/tool.svg)

WHAT YOU'LL done above


-   [Part 1: Launch Kubernetes Clusters with EKS]()
-   [Part 2: Set Up Kubernetes Deployment]()
-   [Part 3: Create Kubernetes Manifests]()

KEY CONCEPTS

-   [Amazon EKS]((https://docs.aws.amazon.com/eks/))
-   [Amazon ECR]((https://docs.aws.amazon.com/ecr/))
-   [Amazon EC2]((https://docs.aws.amazon.com/ec2/))


In the first three projects of this series, you've learnt how to:

1.  [Deploy an EKS cluster,](https://link.nextwork.org/projects/aws-compute-eks1?utm_source=project-app) which is a group of containers that EKS (Elastic Kubernetes Service) will manage.
    
2.  [Build a container image,](https://link.nextwork.org/projects/aws-compute-eks2?utm_source=project-app) which packages up an app's backend code that you want to deploy into a format that Kubernetes can run.
    
3.  [Set up manifest files,](https://link.nextwork.org/projects/aws-compute-eks3?utm_source=project-app) which are instructions that tell Kubernetes how to deploy and run your container image on your EKS cluster.
    

  

In the **final** part of this series, it's finally time to **deploy** that backend with Kubernetes!

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/architecture-complete.png)

**Get ready to...**

-   🚢 Set up the backend of an app for **deployment.**
    
-   ⬇️ Install **kubectl.**
    
-   🚀 **Deploy** the backend on a Kubernetes cluster.
    
-   💎 (Secret Mission) **Track** your Kubernetes deployment using EKS.

-----



### Deploy Your Backend Application

  

Now for the moment you've been waiting for...

Let's deploy our backend application! We'll be using a command-line tool called **kubectl** to do this.

  
  

**In this step, you're going to:**

-   Install kubectl, a command-line tool for using Kubernetes.
    
-   Deploy your app with Kubernetes.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/architecture-complete.png)

  



  
  

-   Apply the manifests:
    



```bash
kubectl apply -f flask-deployment.yaml
kubectl apply -f flask-service.yaml

```

> **💡 What does it mean to 'apply' manifests?**  
> Now that you've set up the manifest files, this command tells Kubernetes toto create or update resources (i.e. the Deployment and Service) based on the instructions in your manifest files.
> 
> Since this is our first time running `apply`, Kubernetes will **create** the Deployment and Service resources in the cluster.
> 
> The next time you run the same apply command with updated manifests, Kubernetes will recognize that these resources already exist and will **update** them to match the new configurations.

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_33.png)

  ![Screenshot 2025-05-17 023306](https://github.com/user-attachments/assets/b56b1749-9936-498a-92bf-b29188e6eca8)

> **💡 Ah... an error**  
> If you've done the previous projects in this series, you might recognize this error message - you haven't installed the key tool you're using in this command, kubectl!
> 
>   
> **💡 What is kubectl?**  
> **kubectl** is the command-line tool for interacting with Kubernetes resources (e.g. , Deployment or Service resources) once your cluster is up and running. We're using it to apply our manifests and deploy our application.
> 
>   
> **💡 Don't we already have another tool called eksctl?**  
> Good question! eksctl, which you installed in Step #1 of this project, is great for **setting up** and deleting your EKS cluster and configuring its settings.
> 
> But, when it comes to **deploying applications** and managing resources within the cluster, kubectl is the tool to use.


-   Install **kubectl**:
    



```bash
sudo curl -o /usr/local/bin/kubectl \
https://s3.us-west-2.amazonaws.com/amazon-eks/1.31.0/2024-09-12/bin/linux/amd64/kubectl

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_35.png)

 ![Screenshot 2025-05-17 023714](https://github.com/user-attachments/assets/30ea2d60-dc96-4a36-8534-eff3cf799975)
 

-   Just like what you did with Docker, you'll need to give yourself the permission to use kubectl:
    



```bash
sudo chmod +x /usr/local/bin/kubectl

```

-   Check you've installed kubectl properly:
    



```bash
kubectl version

```

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_36.png)

![Screenshot 2025-05-17 023737](https://github.com/user-attachments/assets/681a5672-8d0f-4ee2-924f-bfa7b7462305)  

-   Run the commands to apply your manifest files again. We've tried running both commands before, so you should know what they are!
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks2/processed_image_37.png)

  ![Screenshot 2025-05-17 023850](https://github.com/user-attachments/assets/14ecaacc-bf61-45b3-94ec-0c3b68ed11b1)


Nice work! You've just used kubectl to apply your manifest files, which deploys your app across your cluster.

Wondering how you can **check** that you've deployed the app? Look no further than today's secret mission...

----
## 💎 Secret Mission

### Verify your EKS deployment

  

Welcome to your 🤫 exclusive 🤫 secret mission!

Your mission, should you choose to accept it, is to investigate your deployment's progress using Amazon EKS.

  
  

💎 **Get ready to:**

-   View your EKS cluster in the console.
    
-   Verify your backend's deployment in EKS.
    
-   Showcase your secret mission in your **project documentation.**
    

> 💎 **Congratulations** - Secret Mission unlocked!



-   In a new tab, open up the `EKS` console.
    
-   Select the **nextwork-eks-cluster** cluster you've created for this project.
    
-   Welcome to your EKS cluster's dedicated page!
    
-   Select the **Compute** tab.
    
-   Scroll down to the **Node groups** panel - nice, your node group is here.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_12.png)

![Screenshot 2025-05-17 024054](https://github.com/user-attachments/assets/0382dc5a-01da-4d13-8611-331e6dbc8ecb)  

-   Scroll back up to the top of your cluster's page. Notice that there are two banners in blue.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_10.png)

  

> 💡 **What are these two banners saying?**  
> The two blue banners in the EKS console are letting you know that while you have created a node group, you might not have the permission to see the nodes inside.
> 
>   
> 💡 **But my IAM User has AdministratorAccess - how could it not have permission?**  
>   
> 
> AWS permissions alone don’t automatically carry over to Kubernetes — Kubernetes has its own way of managing access within a cluster.
> 
> Even if you have AdministratorAccess in AWS, which grants full access to AWS resources, Kubernetes will only let you into different parts of the cluster if you have permissions under its own system too.

  
  

**Set up access to your cluster nodes**

To give yourself access to your cluster, we went through how to set up IAM access policies in the EKS console in the [first project](https://link.nextwork.org/projects/aws-compute-eks1?utm_source=project-app) of this Kubernetes series.

This time, we'll use terminal commands instead for a faster, more efficient way to grant access.

-   Head back to your **EC2 Instance Connect** tab.
    
-   Use the following command to give yourself access to your Kubernetes clusters
    
-   Don't forget to replace `[USER_ARN]` and `[YOUR-REGION]` with your actual IAM User ARN:
    


```bash
eksctl create iamidentitymapping --cluster nextwork-eks-cluster --arn [USER_ARN] --group system:masters --username admin --region [YOUR-REGION]

```

> 🙋‍♀️ **Where's my IAM User ARN?**
> 
> -   In a new tab, visit the **IAM** console.
>     
> -   From the left hand sidebar, select **Users**.
>     
> -   Select the IAM User you've logged into for today's project. If you're not sure about your IAM User's name, check the top right corner of your console.
>     
> -   Copy your IAM User's ARN from the Summary panel.
>     
>     ![](https://learn.nextwork.org/projects/static/aws-compute-eks4/iam-user.png)
>     
>       
>     
![Screenshot 2025-05-17 024119](https://github.com/user-attachments/assets/36550506-ef09-4b96-bcb4-86201498ed9e)


Your final command should look similar to this:

![](https://learn.nextwork.org/projects/static/aws-compute-eks3/processed_image_2.png)

  

-   Select the **refresh** button on the console. You should now see your nodes listed under your node group.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_13.png)

  ![Screenshot 2025-05-17 024137](https://github.com/user-attachments/assets/9e61631b-b814-4960-ae40-5ba70c58ed5d)

> 💡 **Why are there three nodes but one node group?**  
> The **node group** is a group of nodes that share the same configuration, like instance type and scaling settings. In this case, our node group has three nodes, which means there are three EC2 instances that will run containers like a single unit.
> 
>   
> 🙋‍♀️ **I don't see any nodes**  
> Totally possible!
> 
> 1.  Head to your **CloudFormation** console.
>     
> 2.  Is your **nodegroup** stack in **CREATE_COMPLETE** too? If not, wait a few more moments.
>     
> 3.  Is your **nodegroup** cluster showing **ROLLBACK_COMPLETE** in red? Select the **Events** tab for that Stack and select **Detect root cause** to check why it's failed. See if you can resolve the root cause on your own,
> 4.  Refresh your EKS console again, 
>     



-   Click into one of the nodes to view its details.
    
-   Scroll down to the **Pods** section.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_17.png)

  ![Screenshot 2025-05-17 025845](https://github.com/user-attachments/assets/4cf5539d-6bc2-47d7-9612-b41a2275e66f)

> **💡 What is a pod?**  
> While we've been thinking about a Kubernetes cluster as a bunch of **nodes** running your containerized applications together, you can actually zoom in and break down a node even further... introducing pods!
> 
> In Kubernetes, **pods** bundle containers together so they can work as a unit. Pods are the smallest things you can deploy - you can't deploy containers on their own; they must be inside a Pod. In more technical terms, we'd call pods the **smallest deployable units** in Kubernetes.
> 
> Containers in a pod share the same network space and storage so they can communicate and share data more efficiently.



-   Select the pod that starts with **demo-flask-backend-xx.**
    
-   Check out the **Events** section to see the latest updates for this pod.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_16.png)

  ![Screenshot 2025-05-17 030154](https://github.com/user-attachments/assets/c99c2cea-49e1-412e-9d27-381d123e09cf)

> 💡 **What do these events mean?**  
> These events show the steps that happened when Kubernetes was creating your pod:
> 
> Here's what each step means:
> 
> 1.  `Successfully assigned default/demo-flask-backend...`: Your pod has been given an internal IP address in the cluster.
>     
> 2.  `Pulling image...`: The pod is getting your container image from Amazon ECR.
>     
> 3.  `Successfully pulled image...`: The image was successfully downloaded to the cluster.
>     
> 4.  `Created container demo-flask-backend`: The container was built from your image and prepared for launch.
>     
> 5.  `Started container demo-flask-backend`: The container has been successfully started and is now running in your pod.
>     
> 
>   
> 💡 **What does assigning an image to an IP mean?**  
> This means a container, built from the container image your pod pulled, is now deployed and running at an internal IP address inside the cluster.
> 
> In simpler terms, your backend is up and working and can be accessed within the cluster's network.

Long story short, your backend has definitely deployed _somewhere_. We know the IP address of where our backend has been deployed, but we haven't visited that location yet.

You can challenge yourself to find and visit that location, or wait for a continuation of the Kubernetes series coming to you in the future... stay tuned!



---  

## 🗑️ Before You Go

### Delete Your Resources

  

✋ **STOP**

AWS **will charge you** for resources you leave in your account, especially your EKS cluster (it's not Free Tier eligible).

Challenge yourself to delete everything in this project **on your own!**

Keeping track of all the resources you've created and deleting them is a skill you should practice so you don't get charged.

  
  

🛑 **STEPS BELOW IF YOU NEED HELP:**

  
  

**Delete EKS Cluster**

-   Delete your EKS cluster within the terminal this time (replace `[YOUR-REGION]` with your region's code):
    


```bash
eksctl delete cluster --name nextwork-eks-cluster --region [YOUR-REGION]

```

This command deletes the EKS cluster and all associated resources! It takes a bit of time before everything's gone, so we can move on to other resources.

![Screenshot 2025-05-17 033140](https://github.com/user-attachments/assets/5e096f12-3998-4493-a715-6096c28b6516)
  
  ![Screenshot 2025-05-17 032438](https://github.com/user-attachments/assets/b642c6a5-1315-4f61-b67a-8b1ee895c29e)

![Screenshot 2025-05-17 033356](https://github.com/user-attachments/assets/f09678e0-7e2b-4a79-a069-a353d6419aec)

**Terminate EC2 Instance**

-   Head to the `EC2` console.
    
-   Select the checkbox next to **nextwork-eks-instance.**
    
-   Select **Instance state** -> **Terminate (delete) instance**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/processed_image_9.png)

![Screenshot 2025-05-17 033343](https://github.com/user-attachments/assets/facdc8f5-3e84-4b0d-8fca-9ed3b98cfe74)
 ![Screenshot 2025-05-17 033519](https://github.com/user-attachments/assets/5ce5f1ce-7617-4a13-a75e-c896e1243067) 

**Delete ECR Repository**

-   Head in the AWS console.
    
-   Select the `nextwork-flask-backend` repository.
    
-   Click **Delete** and confirm.

![Screenshot 2025-05-17 033436](https://github.com/user-attachments/assets/fa590abe-7ac5-4ba0-b2fb-3151568197f9)
    
![Screenshot 2025-05-17 033444](https://github.com/user-attachments/assets/c7d7d718-76fd-4c78-b44a-8fd2d995d413)

> 💡 **Please check - is your EKS cluster removed? Is everything in the CloudFormation stack deleted?**  
> Please also check for an **Elastic IP** address in the EC2 console - some students have been charged by the Elastic IP still being in their account!



----------



  

You've just **deployed** the backend of an app with Kubernetes!

That's awesome, give yourself a pat on the back 😮‍💨

  
  

**You've learned how to:**

-   🐳 Build and push a **container image** of the backend of an app.
    
-   📝 Write **manifests** that tell Kubernetes how you'd like to deploy the backend.
    
-   🚢 **Deploy** the backend with Kubernetes using kubectl.
    

![](https://learn.nextwork.org/projects/static/aws-compute-eks4/architecture-done.png)

  

Ready to keep learning about Kubernetes? This project wraps up the current Kubernetes series, but stay tuned for more Kubernetes projects that will get you too:

-   See your deployed backend in action.
    
-   Troubleshoot network issues.
    
-   Deploy the frontend for the same app!




🎉 Mission Accomplished

### That's a wrap!
