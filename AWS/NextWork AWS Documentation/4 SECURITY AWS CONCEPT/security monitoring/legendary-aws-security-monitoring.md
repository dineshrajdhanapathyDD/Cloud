<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Security Monitoring System

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-monitoring)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

![Screenshot 2025-06-04 120410](https://github.com/user-attachments/assets/7e28a0cb-ea3d-4f16-9af1-1bed2f7498cd)

---



# Build a Security Monitoring System

Create alerts for when your sensitive information is accessed using AWS CloudTrail, CloudWatch, and SNS.



WHAT YOU'LL NEED

-   An AWS account -  [Create one here!](https://signin.aws.amazon.com/signup?request_type=register)

KEY CONCEPTS

-   [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/)
-   [AWS CloudTrail](https://aws.amazon.com/cloudtrail/)
-   [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/)
-   [Amazon SNS](https://aws.amazon.com/sns/)
-   [Amazon S3](https://aws.amazon.com/s3/)
-   [AWS CLI](https://aws.amazon.com/cli/)


------
## ⚡️ 30 second Summary

Welcome to this project on **setting up a monitoring system** with AWS CloudTrail, CloudWatch and SNS! 🔔

Ever wondered how to keep tabs on who’s accessing your most sensitive data in AWS? Whether it’s API keys, database credentials, or other critical secrets, it's a security risk every time someone accesses your confidential information. That's why companies invest _heavily_ in robust monitoring systems to track and alert on any unusual activity.

In this project, you'll build your own powerful monitoring system using AWS. Protecting data is an essential skill for roles like **Security Engineer**, **DevOps Engineer**, and **Systems** or **Cloud Administrator**.

### In this project, get ready to...

🏞️ Set up **AWS CloudTrail** to track secret access events.
🔎 Use **AWS CloudWatch** to log access attempts and trigger notifications.
🔔 Create **SNS alerts** to get notified when your secrets are accessed.
💎 Build a _second_ notification system and compare which approach delivers better security alerts.

![Architecture Diagram](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-complete.png)

---
  
## 👀 Step #0

###  Before we start Step #1...

By the end of this project, you'll learn how to securely store secrets, track who's accessing them, and get notified instantly when something suspicious happens.

We’ll break down today's project into **two stages**:

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-annotated.png)

  

-   **Stage 1: Set up the secret & logging**
    
    -   In 🔑 Step #1, you'll create a**secret** in AWS Secrets Manager.
        
    -   In 🏞️ Step #2, you'll enable**CloudTrail** to record logs of your AWS account's activity.
        
    -   In 😈 Step #3, you'll test your CloudTrail set up - let's check whether it records a log when you access your secret!  
          
        
-   **Stage 2: Set up the monitoring & alert system**
    
    -   In 🔎 Step #4, you'll set up a**CloudWatch** filter that looks for logs about accessing your secret.
        
    -   In 🔔 Step #5, you'll configure a**CloudWatch Alarm** and **SNS** to send you an email when a new event passes the filters (i.e. when your secret's been accessed).
        
    -   In 💌 Step #6, you'll test and troubleshoot your entire monitoring system!

------
## 🔑 Step #1

### 

Create a Secret

Let's start by creating a secret in AWS Secrets Manager. This secret will be something we want to monitor access to.

  
  

**In this step, you're going to:**

-   Create a new Secrets Manager secret.
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-1.png)

  


  
  

**Create a New Secret**

-   Log in to the AWS Management Console [as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    
-   In the AWS Management Console search bar at the top, search for `Secrets Manager` and select **Secrets Manager** from the results.
    

> 💡 **What is AWS Secrets Manager?**  
> **AWS Secrets Manager** helps you protect secrets, which are passwords, API keys, credentials and sensitive information. Instead of storing important credentials in your code (yikes!) or sharing them via email (double yikes!), you can tuck them safely away in Secrets Manager.
> 
> In our project, we're just storing a dummy secret, but in real life, this is where you'd keep database passwords, API keys, and other sensitive information that would cause a major headache if they leaked.

![Secrets Manager service in AWS Console.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-0.png)

Secrets Manager service in AWS Console.

![Screenshot 2025-05-01 211829](https://github.com/user-attachments/assets/f3310ef4-ab82-4503-be97-bf0f2a645bb7)
  



-   Select **Store a new secret** to begin creating your secret.

![Screenshot 2025-05-01 211843](https://github.com/user-attachments/assets/dfde7bd6-7230-43b9-ab0e-1e2da9c71cc0)

    
-   Under **Choose secret type**, select **Other type of secret**.
    

> 💡 **What are the different secret types?**  
> Secrets Manager gives you a few different options depending on what you're trying to protect...
> 
> -   **Credentials for RDS database**: Perfect when you need to store and automatically rotate passwords for your MySQL, PostgreSQL, or SQL Server databases.
>     
> -   **Credentials for DocumentDB database**: Similar to RDS, but specifically for DocumentDB - one of AWS's document database services.
>     
> -   **Credentials for other databases**: When you need to store credentials for other database types that don't fit the first two options.
>     
> -   **API keys and other secrets**: This is the catch-all category we're using today! It's for anything that isn't a database credential - API keys, OAuth tokens, encryption keys, or just plain text secrets like our demo value.
>     

![Other type of secret selected.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-2.png)

Other type of secret selected.

  

  
  

**Enter Your Secret**

-   In the **Key/value** tab, enter `The Secret is` as the **Key**.
    
-   Enter a random secret or hot take that you have as the **Value**! For example, `I need 3 coffees a day to function`, or `rice is the best carb`
   
   ![Screenshot 2025-05-01 212140](https://github.com/user-attachments/assets/3af3003b-9d56-4b91-ab6d-3690b4e8603b) 

> 💡 **Extra for Experts: Why does Secrets Manager use key-value pairs?**  
> A key-value pair is a simple way to store data by associating a name or label (the key) with a specific value. In AWS Secrets Manager, key-value pairs help you structure secrets in a way that makes them easy to retrieve. The key acts as an identifier e.g. "The Secret is", and the value is the actual data you want to protect ("I need 3 coffees a day to function").
> 
> A key-value pair structure makes it much easier for your applications to grab exactly what they need when you have different pieces of information (such as a username, password, and website) in a single secret. Rather than parsing through a blob of text to find the password, your app can just ask for the value of the specific key it wants.
> 
> Some common real-world examples include:
> 
> -   Database credentials where keys might be "username", "password", "host", "port", and "database_name"
>     
> -   API authentication where keys could be "api_key", "client_id", "client_secret", and "endpoint_url"
>     
> -   Encryption keys with identifiers like "primary_key", "rotation_date", and "algorithm"
>     

![Key and value entered for the secret.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-5.png)

Key and value entered for the secret.

  

-   We'll keep the default **Encryption key** setting.
    

> 💡 **Extra for Experts: What is Encryption?**  
> **Encryption** is like scrambling a message so that only someone with the right key can unscramble it and read it. In our case, Secrets Manager uses an encryption service called AWS KMS (Key Management Service) to encrypt your secrets, so your secret can't be read by anyone without the right access.
> 
>

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-3.png)

  

-   Select **Next**.
    
-   Welcome to the **Configure secret** page!
    
-   Under **Secret name**, enter `TopSecretInfo`
    

![Entering a secret name.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-6.png)

Entering a secret name.

  

-   Under **Description - optional**, add a description like `Secret created for NextWork's project on Building a Monitoring System`
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-4.png)

  ![Screenshot 2025-05-01 212256](https://github.com/user-attachments/assets/c14e7ed1-9d13-429b-8aac-545c9356d49b)

> 💡 **What are the other settings we're skipping?**  
> In AWS Secrets Manager, there are several additional settings we're not configuring in this basic project:
> 
> **Tags** are like digital sticky notes that help you organize and categorize your AWS resources. They consist of a key and value (e.g., "Environment: Production" or "Project: Security-Training") and are useful for tracking costs, filtering resources, or enforcing security policies across large AWS environments.
> 
> **Resource permissions** allow you to control which users, roles, or AWS services can access your secret. This is powerful for implementing the principle of least privilege, where you grant only the minimum necessary permissions to each entity that needs to use the secret.
> 
> **Secret replication** lets you copy your secret to multiple AWS regions, ensuring applications running in different geographic locations can access the secret quickly without having to make cross-region calls. This improves performance and provides redundancy if a region experiences issues.
> 
> These advanced settings are extremely valuable in production environments but aren't essential for our initial learning project.

-   Click **Next**.
    
-   Click **Next** again to skip the **Configure rotation - optional** section.
    

> 💡 **Extra for Experts: What does configure rotation mean in Secrets Manager?**  
> When you enable rotation, Secrets Manager will periodically automatically replace your credentials (like passwords or API keys) with new values, typically every 30, 60, or 90 days. This limits how long a compromised secret would be useful to an attacker.

![Skipping rotation configuration.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-10.png)

Skipping rotation configuration.

![Screenshot 2025-05-01 212323](https://github.com/user-attachments/assets/ebaa4746-83de-44bd-83c9-98d5c77d69ec)  

Let's review your secret set up:  
  

Secret type: **Other type of secret**

Encryption key: **aws/secretsmanager**

Secret name: **TopSecretInfo**

Description: **Secret created for NextWork's project on Building a Monitoring System**

Secret replication: **Disabled**

Automatic rotation: **Disabled**

![Review.](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-26.png)

Review.

![Screenshot 2025-05-01 212449](https://github.com/user-attachments/assets/72017299-9f14-4e54-87fc-feb660829ba9)
  
![Screenshot 2025-05-01 214623](https://github.com/user-attachments/assets/5353e03e-eb81-4f7d-a2d7-02eb1eb866d0)

-   Click **Store** at the bottom of the review page.
    

![Store button on the review page.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-13.png)

Store button on the review page.

  ![Screenshot 2025-05-01 214610](https://github.com/user-attachments/assets/09735144-31b7-4941-903b-b768d48f80b9)

> 💡 **Extra for Experts: What's the sample code in the Secrets Manager setup? Why is it there?**
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-monitoring/unframed/screenshot-12.png)
> 
>   
> 
> AWS provides these ready-to-use code snippets in multiple programming languages (like Python, Java, JavaScript, .NET) showing exactly how to securely fetch your secret using code.
> 
> Instead of developers having to figure out the right approach themselves, they can simply copy this pre-written code into their application, perhaps modify it slightly, and immediately start using the secret securely. A pretty convenient way to adopt good security practices rather than cutting corners with hardcoded credentials or insecure storage methods!

-   You should see a green banner at the top.
    
-   In the green banner, select **View details**.
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-6.png)

  ![Screenshot 2025-05-01 214638](https://github.com/user-attachments/assets/f6af70bc-9d0b-435f-80a4-fb95f9a4ecd1)


-   You can now see your newly created secret `TopSecretInfo`

![Screenshot 2025-05-01 214804](https://github.com/user-attachments/assets/d5e71347-c6f5-459c-b220-5275287e63f2)
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-7.png)

  
![Screenshot 2025-05-01 214709](https://github.com/user-attachments/assets/b6d46c41-0b29-4b9d-80c3-126efc2dc0b1)

  
  

**Awesome! You've created your first secret in Secrets Manager.** It's looking great. Ready to set up CloudTrail to track access to this secret?

-----
## 🏞️ Step #2

###  Configure CloudTrail

Now, let's configure CloudTrail to track access to our secret. CloudTrail is a **monitoring** service - it records events that happened in your AWS account, like creating resources, updating a name or setting... and accessing secrets in Secrets Manager 👀

  ![Screenshot 2025-05-01 215617](https://github.com/user-attachments/assets/681111f0-d2f9-404c-bb8b-192d7939d680)
  

**In this step, you're going to:**

-   Create a new CloudTrail **trail** to record your account's activity.
- 


    
-   Configure the trail to store logs in an **S3 bucket.**
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-2.png)

  


  
  

**Create a New Trail**

-   In the AWS Management Console, head to the `CloudTrail` console.

![Screenshot 2025-05-01 215645](https://github.com/user-attachments/assets/5258b569-022e-4286-9385-84d0b67dd622)
    

> 💡 **What is AWS CloudTrail?**  
> AWS CloudTrail is a **monitoring** service - think of it as an activity recorder throughout your AWS account. It documents every action taken, like who did what, when they did it, and where they did it from.
> 
> This continuous recording is super valuable for security (spotting unusual activity), troubleshooting (figuring out what changed when something breaks), and meeting compliance requirements (proving you're following the rules).
> 
> In our project, we're using it to keep an eye on who's accessing our secret 👀

![CloudTrail service in AWS Console.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-14.png)

CloudTrail service in AWS Console.

  

-   From the left hand navigation panel, select **Trails.**  
      
    
-   Select **Create trail** to start setting up a new trail.
    

![Create trail button in CloudTrail.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-15.png)

Create trail button in CloudTrail.

  ![Screenshot 2025-05-01 215757](https://github.com/user-attachments/assets/208d37ea-30ec-45ff-ba1a-71c7081b75df)


-   Welcome to the **Choose trail attributes** page! Let's create a trail!

![Screenshot 2025-05-01 215810](https://github.com/user-attachments/assets/5b761f5b-cd3b-4e89-b70b-78fb2faeb489)
    

> 💡 **What is a trail?**  
> A trail tells CloudTrail exactly what activity to record and where to save those recordings. When you create a trail, you're essentially saying "Hey CloudTrail, please keep track of all xyz activities and store the data in this specific location."
> 
> You can have multiple trails for different purposes - you'll learn about the different types of trails in the next page!



-   Under **Trail name**, enter `secrets-manager-trail`.
    

![Trail name entered.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-16.png)

Trail name entered.

  

-   In the **Storage location** section, select **Create new S3 bucket**.
    

> 💡 **Why use S3 for CloudTrail logs?**  
> CloudTrail logs can grow a _lot_ over time - you're recording every action on your account! S3 gives you practically unlimited storage that's both super durable (your logs won't get lost) and cost-effective (you only pay for what you use).
> 
> Plus, S3 works seamlessly with other AWS services, so when you want to analyze those logs later with tools such as Athena or Lambda, you can integrate them easily.

![Create new S3 bucket selected.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-17.png)

Create new S3 bucket selected.

  

-   Under **Trail log bucket and folder**, enter a unique bucket name:
    
![Screenshot 2025-05-01 220127](https://github.com/user-attachments/assets/81cd953b-3d86-4a1a-87f9-9747c76495b4)


```text
nextwork-secrets-manager-trail-yourinitials
```

![Unique S3 bucket name entered.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-18.png)

Unique S3 bucket name entered.

![Screenshot 2025-05-01 220249](https://github.com/user-attachments/assets/cd52e28d-1440-4953-a2a5-d23ea9ff79a7)
  

-   🚨 Make sure to uncheck **Log file SSE-KMS encryption** - otherwise, you'll get charged for creating a new customer managed KMS key!
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-8.png)

  

-   Keep the other default settings.
    

> 💡 **Extra for experts: What are these other settings?**  
> These additional settings give you more control over your CloudTrail configuration:
> 
> -   **Log file validation** lets you verify that your log files haven't been tampered with after CloudTrail delivered them. When enabled, CloudTrail creates a digital signature alongside each log file, which you can use later to confirm the logs are authentic and unchanged.
>     
> -   **SNS notification delivery** sends you a notification whenever a new log file is delivered to your S3 bucket. This helps you know immediately when new activity has been logged, rather than having to check manually.
>     
> -   **CloudWatch Logs** integration forwards your CloudTrail logs to CloudWatch Logs in addition to S3. This is super useful because it lets you set up real-time monitoring, create metric filters, and trigger alarms based on specific activities in your logs - exactly what we're doing in this project! We'll enable this in Step #4 and focus on CloudTrail for now.
>     

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-9.png)

![Screenshot 2025-05-01 220308](https://github.com/user-attachments/assets/f0793560-7113-4ad6-af84-d14a66e7073e)
  

-   Scroll down and select **Next**.
    

  
  

**Configure Log Events**

-   On the **Choose log events** page, ensure **Management events** is selected under **Event type**.
    

> 💡 **What are the different types of CloudTrail events?**  
> CloudTrail captures different types of events, each showing you a different view into what's happening in your AWS account:
> 
> -   **Management events**: These show you admin actions that configure your AWS resources - creating an EC2 instance, updating a security group, or in our case, accessing a secret. We're focusing on these in our project since secret access gets recorded here.
>     
> -   **Data events**: These track high-volume actions that operate ON your resources rather than creating or configuring them - like uploading a file to S3 or running a Lambda function.
>     
> -   **Insights events**: These detect unusual patterns in your management events, like someone suddenly creating 100x more IAM users than normal.
>     
> -   **Network activity events**: These track network-related activities, like changes to your VPC configuration or traffic to a subnet.
>     

![Management events selected.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-25.png)

Management events selected.

  

> 💡 **Extra for Experts: Why is retrieving a secret a management event, not a data event?**  
>   
> 
> This is a really good question! When you retrieve a secret value using the GetSecretValue API, you're not just reading raw data - you're using a control-plane (i.e. management) action to decrypt and access protected configuration information. The secret itself is considered a configuration resource for your applications.
> 
> The distinction matters for practical reasons too - management events are enabled by default in CloudTrail and generally included in your basic CloudTrail costs, while data events require additional configuration and can increase your CloudTrail charges because of their volume. By classifying secret retrieval as a management event, AWS makes it easier to monitor this security-critical operation without incurring the higher costs associated with data event logging.



-   Under **API activity**, keep both **Read** and **Write** checked.
    

> 💡 **What are Read vs Write activity?**
> 
> -   **Read API activity** happens when someone views but doesn't change anything. For example, listing your S3 buckets, describing your EC2 instances, or in our project, viewing (but not changing) metadata about a secret.
>     
> -   **Write API activity** occurs when changes happen - creating, deleting, modifying resources, or even retrieving the value of a secret (which is what we want to monitor).
>     
> 
>   
> 💡 **Extra for Experts: Why is retrieving a secret value considered a "Write" API activity?**  
>   
> 
> This is quite helpful for security monitoring! By treating secret retrieval as a "Write" operation, it ensures these critical security events are captured in your CloudTrail logs even if someone configures CloudTrail to only log write events (which is a common cost-saving measure).
> 
> As you come across more and more Secrets Manger API calls, you'll notice a pattern - operations that only access metadata about secrets (like ListSecrets or DescribeSecret) are classified as "Read" operations, while those that access the actual sensitive values or modify secrets are classified as "Write" operations.

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-10.png)

![Screenshot 2025-05-01 220345](https://github.com/user-attachments/assets/eeda48d1-c595-48fe-9314-0b824b54a9da)  



-   Check **Exclude AWS KMS events**.
    
-   Check **Exclude Amazon RDS Data API events**.
    

> 💡 **Extra for Experts: Why are we excluding these events?**  
> KMS, AWS's encryption service, encrypts most resources in AWS and works behind the scenes whenever you access and open an AWS resource you've created. Because of this, KMS events can make up more than 99% of all your CloudTrail events - that's a lot of noise when you're trying to spot important activities!
> 
> Similarly, we're excluding Amazon RDS Data API events because they can generate lots of routine database access logs that aren't relevant to our secrets monitoring.

![Management events and API activity configured.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-32.png)

Management events and API activity configured.

![Screenshot 2025-05-01 220734](https://github.com/user-attachments/assets/adce3f2e-1c3f-45f0-a947-2c5796126c47)  

-   Select **Next**.
    
-   Review your trail setup on the **Review and create** page:
    

![Review trail configuration before creation.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-33.png)

Review trail configuration before creation.



**Step 1: Choose trail attributes**  
  

Trail name: `secrets-manager-trail`

Multi-region trail: **Yes**

Apply trail to my organization: **Not enabled**

Trail log location: **nextwork-secrets-manager-trail-yourinitials/AWSLogs**

Log file SSE-KMS encryption: **Not enabled**

Log file validation: **Enabled**

SNS notification delivery: **Disabled**

![Review trail configuration before creation.](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-11.png)

Review trail configuration before creation.

![Screenshot 2025-05-01 220756](https://github.com/user-attachments/assets/3ed2a1be-93ed-405f-8cf3-e21e36200615)
    

**Step 2: Choose log events**  
  

API activity: **All**

Exclude AWS KMS events: **Yes**

Exclude Amazon RDS Data API events: **Yes**

![Review Step 2.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-36.png)

Review Step 2.

  ![Screenshot 2025-05-01 220804](https://github.com/user-attachments/assets/1348ed40-fb1e-428d-b771-6cabe476fd24)


-   Click **Create trail**.
    

![Create trail button on review page.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-37.png)

Create trail button on review page.

  

-   You should see a green banner at the top - congrats! You've created your trail.
    

  ![Screenshot 2025-05-01 220944](https://github.com/user-attachments/assets/ab9aaf65-96ce-492d-b215-4b729fd94a27)

  

**Fantastic! You've set up CloudTrail to monitor API calls.**

It's all set to track access to your secret. Let's generate some secret access events in the next step!

-----
## 😈 Step #3

### Generate Secret Access Events

Now that CloudTrail is set up, let's generate some secret access events. We'll access our secret in a couple of ways to make sure CloudTrail logs these events.

  
  

**In this step, you're going to:**

-   Expose your own secret (aka open and see the secret you recorded)!
    
-   Check that CloudTrail recorded what you did 👀
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-3.png)

  



  
  

**Access Your Secret**

-   Navigate back to the `Secrets Manager` console.
    

![Secrets Manager service in AWS Console.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-0.png)

Secrets Manager service in AWS Console.

![Screenshot 2025-05-01 221130](https://github.com/user-attachments/assets/5917d818-25cc-4f7b-a855-f0cdf7ab56d0)  

-   Pick your `TopSecretInfo` secret.

![Screenshot 2025-05-01 221233](https://github.com/user-attachments/assets/f55000c7-e5e1-4e65-b99f-1dbbd26a957a)
    
-   On the secret details page, scroll down to the **Overview** section.
    
-   Select **Retrieve secret value**.
    

> 💡 **What does Retrieve secret value do?**  
> When you click **Retrieve secret value**, you're opening the actual content of your secret. Behind the scenes, this triggers what's called a `GetSecretValue` API call to AWS. It's this specific API call that we want to monitor with CloudTrail, because it represents someone reading your secret!

![Retrieve secret value button.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-38.png)

Retrieve secret value button.

![Screenshot 2025-05-01 221303](https://github.com/user-attachments/assets/f67efbb7-91b3-41cb-8ed8-dabb830bf73f)  

-   You should now see the secret value displayed!
    

![Secret value displayed with close button.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-39.png)

Secret value displayed with close button.

![Screenshot 2025-05-01 221348](https://github.com/user-attachments/assets/7725c8c5-3c6a-4586-aa37-945f840b3678)
  

-   Select **Close** to close the secret value display.
    

![Select Close.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-45.png)

Select Close.

  

  
  

**Access Your Secret Over AWS CLI**

Turns out, the console is not the only way to access a secret.

If you'd like to be a little 💅 extra 💅, here's your chance at accessing your secret in a second way - the AWS CLI!

-   Open **AWS CloudShell** - click on the CloudShell icon in the AWS Management Console's top navigation bar.
    

![CloudShell icon in AWS Console.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-40.png)

CloudShell icon in AWS Console.

  

> 💡 **What is AWS CloudShell?**  
> AWS CloudShell gives you a command-line terminal that's already logged into your AWS account and ready to go. This saves you the time you'd usually have to spend on the AWS CLI on your computer, remembering to configure credentials, and keeping everything updated.
> 
>   
> 💡 **What is AWS CLI?**  
> The AWS Command Line Interface (CLI) is like a text-based remote control for all your AWS services. Instead of clicking around in the web console, you can type commands to make things happen. For example, rather than clicking through several screens to create a trail or secret, you can just type a single command as we did. Developers love the CLI because it's fast, can be scripted for automation, and gives you more precise control.

-   The CloudShell terminal should now be opened and ready (it can take up to 30 seconds).
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-12.png)

  


-   In the CloudShell terminal, run the following command.
    
-   Make sure to replace `your-region-code` at the end of the command. Use the region code you see when you select your Region dropdown (e.g. `us-east-2` for the Ohio region):
    



```bash
aws secretsmanager get-secret-value --secret-id "TopSecretInfo" --region your-region-code
```

![AWS CLI command in CloudShell.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-41.png)

AWS CLI command in CloudShell.

  ![Screenshot 2025-05-01 221643](https://github.com/user-attachments/assets/ea3d0dc7-9fb3-4861-8d72-3a98f060075d)

-   The command should run successfully and give you the secret's value in JSON format.
    

![Command output in CloudShell.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-44.png)

Command output in CloudShell.

  ![Screenshot 2025-05-01 221704](https://github.com/user-attachments/assets/00145d1c-09d2-49c4-b4fe-4e6c17e01054)



You've generated **secret access events** through the console and the AWS CLI. Consider this our secret accessed. Do you think CloudTrail knows what you just did?

Let's see whether CloudTrail captured the events 👀

  
  ![Screenshot 2025-05-01 221923](https://github.com/user-attachments/assets/0bd02421-c592-405c-bf7c-4b706e79e608)

**Analyse Your CloudTrail Events**

-   Head to the `CloudTrail` console again.
    

![CloudTrail service in services menu.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-48.png)

CloudTrail service in services menu.
![Screenshot 2025-05-01 221949](https://github.com/user-attachments/assets/12ee46e2-da4f-4d02-b46b-52cb88e5a50f)



  

-   You should now be on the **CloudTrail** dashboard.
    
-   In the left navigation pane, select **Event history**.
    

> 💡 **What is CloudTrail Event history?**  
> **Event history** is where you can find all of your account's management events from the last 90 days. Let's use it to quickly confirm whether CloudTrail captured our secret access events, without having to dig through the raw log files in S3.

![Event history in CloudTrail navigation.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-49.png)

Event history in CloudTrail navigation.

  

-   Welcome to the **Event history** page!
    

![Event history page.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-51.png)

Event history page.

  ![Screenshot 2025-05-01 222005](https://github.com/user-attachments/assets/43cb0daa-255f-447f-aec9-f6188905b6a9)

-   Under **Lookup attributes**, select the dropdown and choose **Event source**.
    

![Event source selected in lookup attributes.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-52.png)

Event source selected in lookup attributes.

  

-   In the search bar next to **Event source**, enter `secretsmanager.amazonaws.com`

![Screenshot 2025-05-01 222111](https://github.com/user-attachments/assets/30787d28-cc1a-4686-a0d8-9f9e56a898e4)    

> 💡 **What are lookup attributes and event source?**  
> **Lookup attributes** are like search filters that help you find specific events in your CloudTrail logs:
> 
> -   **Event source** - the AWS service that generated the event (like secretsmanager.amazonaws.com)
>     
> -   **Event name** - the specific action that was performed (like GetSecretValue)
>     
> -   **User name** - who performed the action
>     
> -   **Resource type** - what kind of resource was involved
>     
> 
>   
> We're using **Event source** to filter for only Secrets Manager events, which helps us quickly spot if and when our secret was accessed without wading through tons of unrelated events!

![secretsmanager.amazonaws.com entered in search bar.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-53.png)

secretsmanager.amazonaws.com entered in search bar.

  

-   You should now see events related to `secretsmanager.amazonaws.com`.
   
![Screenshot 2025-05-01 222122](https://github.com/user-attachments/assets/b06e41a7-ef7c-4c65-b968-60d47685fb96)

 
-   Scroll through the event list - check for an event caled `GetSecretValue`. This events means your secret's value was retrieved or used. Woah!
    

![GetSecretValue events in CloudTrail event history.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-54.png)

GetSecretValue events in CloudTrail event history.

  
![Screenshot 2025-05-01 222310](https://github.com/user-attachments/assets/66354c73-3021-4e6b-a792-ba74d4d24ead)


  
  

Interesting! Now you've confirmed that CloudTrail records an event when someone accesses your secret.

![Screenshot 2025-05-01 222608](https://github.com/user-attachments/assets/fe54ca3d-7611-426e-b369-eb1fbb3da9be)


What's next? Imagine if you want to be alerted too... Let's add a **notification** system so that AWS automatically emails you whenever your secret's being viewed by someone.

----
## 🔎 Step #4

Track Secrets Access Using CloudWatch Metrics

Alright! We know CloudTrail can track events for us, next up is to figure out how we can get alerts when your secret _does_ get accessed.

We'll start by sending all of CloudTrail's logs to CloudWatch. Once it's in CloudWatch, we can set up helpful tools like CloudWatch metrics and alarms that can trigger notifications based on events!

  
  

**In this step, you're going to:**

-   Enable CloudWatch **Logs** for your CloudTrail trail.
    
-   Define a CloudWatch **Metric** to track secret access.
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-4.png)

  


  
  

**Analyse Your CloudWatch Logs**

Let's start this step by telling CloudTrail that we want a copy of all logs sent to another service - CloudWatch!

-   Still in your `CloudTrail` console, select **Trails** in the left navigation pane.
    
-   Select your trail `secrets-manager-trail`
    
-   You should now be seeing the details of your trail.
    

![CloudTrail trails page with your trail selected.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-64.png)

CloudTrail trails page with your trail selected.

  ![Screenshot 2025-05-01 222627](https://github.com/user-attachments/assets/3ee60e37-fb3c-4b13-b190-e359a73fdc97)


-   Scroll down to the **CloudWatch Logs** section.
    
-   Select **Edit**.
    

![Edit button next to CloudWatch Logs.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-66.png)

Edit button next to CloudWatch Logs.

  ![Screenshot 2025-05-01 222715](https://github.com/user-attachments/assets/09009c42-8721-4ac1-812f-e86cec3091d4)

-   Check the **Enabled** checkbox for **CloudWatch Logs**.
    

> 💡 **What are Amazon CloudWatch Logs?**  
> **Amazon CloudWatch Logs** is a service that helps you bring together your logs from different AWS services, including CloudTrail, for visibility, troubleshooting, and analysis.
> 
> It's especially powerful because once your logs are in CloudWatch, you can create **alerts** based on specific patterns (such as someone accessing your secret), visualize trends, or trigger automated responses.
> 
> For this project, we're sending our CloudTrail logs to CloudWatch Logs so we can set up alerts when someone accesses our secret.

![Enable CloudWatch Logs.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-67.png)

Enable CloudWatch Logs.

  

> 💡 **Extra for Experts: What other logs can CloudWatch Logs store?**  
> CloudWatch Logs can store and monitor logs from a wide variety of sources, not just CloudTrail! Here's what else you can send to CloudWatch Logs:
> 
> -   **Application logs** from your applications running on EC2, ECS, or Kubernetes
>     
> -   **On-premises server logs** using the CloudWatch agent
>     
> -   **Network logs** like VPC Flow Logs and Route 53 DNS query logs
>     
> -   **IoT device logs** for monitoring your connected devices
>     
> -   **CloudFront access logs** to track viewer requests to your CDN content
>     



-   Select **New** log group.
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-14.png)

  

-   Under **Log group name**, enter `nextwork-secretsmanager-loggroup`.
    
![Screenshot 2025-05-01 222907](https://github.com/user-attachments/assets/7200452e-3060-442a-9114-6bcc091dede6)

> 💡 **What's a log group?**  
> A log group represents a collection of logs from a specific application or service. We're creating a new log group to store CloudTrail logs that came from our CloudTrail trail.

![Log group name.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-68.png)

Log group name.

  

-   Under **IAM Role**, select **New**.
    
-   Under **Role name**, enter `CloudTrailRoleForCloudWatchLogs_secrets-manager-trail`
    

> 💡 **Extra for Experts: Why create an IAM Role for CloudWatch Logs?**  
> Instead of giving CloudTrail unlimited access to write anywhere it wants, AWS is creating a **role** that specifically allows it to write logs to CloudWatch Logs - and nothing else!
> 
> This follows a security principle called "least privilege" - only giving services exactly the permissions they need, nothing more. This way, even if something unexpected happens, the potential impact remains contained to just what that role can do.

![Log group and IAM Role configured.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-70.png)

Log group and IAM Role configured.

  

-   Select **Save changes** to save the new CloudWatch Logs setup.
    
![Screenshot 2025-05-01 223015](https://github.com/user-attachments/assets/9438bda9-640d-4134-8fc6-4f096d2fcfc7)


![Save changes button for CloudWatch Logs.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-71.png)

Save changes button for CloudWatch Logs.

  
![Screenshot 2025-05-01 223031](https://github.com/user-attachments/assets/bd63ffc4-e8a8-4955-a75f-cdc14e45953d)
  
  

**Verify Your CloudWatch Logs**

-   Head to the `CloudWatch` console. Let's verify that CloudTrail is really passing the logs to a new log group.
    

![CloudWatch service in services menu.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-72.png)

CloudWatch service in services menu.

![Screenshot 2025-05-01 223120](https://github.com/user-attachments/assets/e0f22ddc-0174-4913-b539-c755b4cec4e4)  

-   In the left navigation pane, expand **Logs** and select **Log groups**.
    

![Log groups in CloudWatch navigation.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-73.png)

Log groups in CloudWatch navigation.

  ![Screenshot 2025-05-01 223259](https://github.com/user-attachments/assets/f36d5a48-3973-4d75-8867-745563c4d693)



-   Welcome to the **Log groups** page!
    
-   In the **Log groups** page, search for and select `nextwork-secretsmanager-loggroup`
    

![Log group nextwork-secretsmanager-loggroup selected.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-76.png)

Log group nextwork-secretsmanager-loggroup selected.

  

-   You might see multiple **Log streams** (i.e. subfolders of log groups). Pick any one of them. If you only see one, that's fine too!
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-16.png)

  
![Screenshot 2025-05-01 223400](https://github.com/user-attachments/assets/9241062d-7248-44a0-9fd0-26f8105653ca)

-   You should now see _heaps_ of logs inside the stream. If you don't see rows and rows of logs straight away, you might need to wait a few minutes and refresh your page first.
    

![Details of nextwork-secretsmanager-loggroup.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-77.png)

Details of nextwork-secretsmanager-loggroup.

![Screenshot 2025-05-01 223456](https://github.com/user-attachments/assets/b88387a3-7f3d-48bc-8550-1bcc93ac3010)

  

-   Amazing! You can even expand one of the logs to see all the spicy details inside.
    

> 💡 **Okay... so what? Couldn't I see events in CloudTrail anyway?**  
> Great question! Yes, you _could_ see the same events in CloudTrail Event History, which is great for quick investigations on recent events. Sending logs to CloudWatch Logs is big milestone for us, because:
> 
> 1.  CloudWatch Logs is where we can set up **alerts** and **automated responses** when specific events happen, which we'll start setting up in this step.
>     
> 2.  CloudTrail Event History only keeps events for **90 days**, while CloudWatch Logs can store them for as long as you'd like.
>     
> 3.  CloudWatch Logs has powerful filtering tools that let us focus on exactly the events we care about.
>     

![Details of nextwork-secretsmanager-loggroup.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-78.png)

Details of nextwork-secretsmanager-loggroup.

![Screenshot 2025-05-01 223557](https://github.com/user-attachments/assets/95176713-6126-4e1a-a4f0-15c019b2fb45)
  



  
  

**Create Metric Filter**

-   Head back to your log group.
    
-   At the top of your log group, select **Actions** and then **Create metric filter** from the dropdown menu.
    

![Create metric filter in Actions dropdown.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-80.png)

Create metric filter in Actions dropdown.

  ![Screenshot 2025-05-01 223719](https://github.com/user-attachments/assets/e8a22dde-8389-41e9-b835-1fc9aa6c1e99)

-   Welcome to the **Define pattern** page! This is where we tell CloudWatch about the kind of actions we're looking for.
    

![Let's define a metric filter.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-81.png)

Let's define a metric filter.

![Screenshot 2025-05-01 223848](https://github.com/user-attachments/assets/3b00a171-3963-4f0d-a759-e8c2f260c00d)  

-   In the **Filter pattern** field, enter `"GetSecretValue"`
    


> 💡 **What are CloudWatch metric filters?**  
> **Metric filters** automatically scan through your logs looking for specific patterns. Instead of you manually reading thousands of log entries to find mentions of `"GetSecretValue"`, a metric filter automatically detects these patterns and keeps count for you.
> 
> We're creating a filter to specifically detect when someone retrieves our secret's value, which is defined by the action "GetSecretValue".

![Filter pattern for GetSecretValue events.](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-17.png)

Filter pattern for GetSecretValue events.

  ![Screenshot 2025-05-01 224250](https://github.com/user-attachments/assets/10c0e454-4ba0-4a9d-9968-fd07a4dafb3b)

-   We'll get to know the **Test pattern** section in Step #6 - for now, let's focus on creating the metric filter!
    
-   Select **Next**.
    
-   For the **Filter name**, let's use `GetSecretsValue`
    
-   Under **Metric details**, name the **Metric namespace**: `SecurityMetrics`
    
![Screenshot 2025-05-01 223918](https://github.com/user-attachments/assets/033325e9-02d0-4f7f-a73b-d7da806a9f8a)

> 💡 **What is a metric namespace?**  
> A **metric namespace** is a like a folder for your CloudWatch metrics. Namespaces help you organize your metrics and prevent naming conflicts with metrics from other AWS services or applications. We're creating a namespace called `SecurityMetrics` to group all our security-related metrics.

![Metric namespace.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-89.png)

Metric namespace.

  

-   **Metric name**: Enter `Secret is accessed`.
    

![Metric names.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-90.png)

Metric names.

  

-   **Metric value**: Enter `1`.
    
-   **Default value**: Enter `0`.
    
![Screenshot 2025-05-01 224307](https://github.com/user-attachments/assets/1ce0b5a3-fba0-4a6c-877e-aec2c9ced109)

> 💡 **What are metric and default values?**
> 
> -   **Metric value** is what gets recorded when our filter spots a match in the logs. We're setting it to `1` so that each time someone accesses our secret, the counter increases by exactly one.
>     
> -   **Default value** is what gets recorded when our filter doesn't find any matches during a given time period. We're setting it to `0` so that time periods with no secret access show up as zero on our charts, rather than not showing up at all. This gives us a complete picture - we can see both when access happened AND when it didn't.
>     



-   Select **Next** - let's review our work!
    

![Next button.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-94.png)

Next button.

  ![Screenshot 2025-05-01 224705](https://github.com/user-attachments/assets/08a2f74b-461e-4c4e-a5e1-16b044a091b8)

-   Welcome to the **Review and create** page for the metric filter.  
      
    

Filter pattern: `GetSecretValue`

Filter name: `GetSecretValue`

Metric name: `Secret is accessed`

Metric namespace: `SecurityMetrics`

Applied on transformed logs: `-`

Metric value: `1`

Default value: `0`

Unit: `-`

![Review your filter pattern.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-96.png)

Review your filter pattern.

  

-   Select **Create metric filter** to finalize and create your metric filter.
    

![Create metric filter button on review page.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-97.png)

Create metric filter button on review page.

  

-   You should see a green banner at the top confirming metric filter creation.
    

![Success!](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-98.png)

Success!

![Screenshot 2025-05-01 224816](https://github.com/user-attachments/assets/45c250fa-644c-4cf1-9b9e-faec91144998)
  

  
  

**Fantastic! You've created a metric filter and metric to track secret access.** Next, we'll create a CloudWatch Alarm to notify us when the secret is accessed.

----
## 🔔 Step #5


Create CloudWatch Alarm and SNS Topic

Now, let's create a CloudWatch Alarm that triggers when our `SecretIsAccessed` metric exceeds a threshold. We'll also set up an **SNS** topic to receive email notifications when the alarm is triggered.

> 💡 **What is Amazon SNS?**  
> **Amazon Simple Notification Service (SNS)** is AWS's built-in messaging system. It lets your AWS resources send notifications to people (via email, SMS, or mobile push) or even to other applications.
> 
> In our project, we're using SNS to send an email alert when CloudWatch detects that someone accessed our secret, so you can respond quickly to potential security issues.

**In this step, you're going to:**

-   Create a CloudWatch Alarm based on the `SecretIsAccessed` metric.
    
-   Create an SNS topic to send email notifications.
    
-   Subscribe your email address to the SNS topic.
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-5.png)

  



  
  

**Create CloudWatch Alarm**

-   Still in your CloudWatch Alarm's page, select the **Metric filters** tab.
    

![Select your metric filter.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-99.png)

Select your metric filter.

  ![Screenshot 2025-05-01 225811](https://github.com/user-attachments/assets/fe10379e-e54f-49b6-8625-32a47ccd89e6)

-   Scroll down and check the box next to the `GetSecretValue` metric filter.
    

![Select your metric filter.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-104.png)

Select your metric filter.

  

-   Select **Create alarm**.
    
-   Now, welcome to the CloudWatch alarm setup!
    

![Select your metric filter.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-105.png)

Select your metric filter.

  ![Screenshot 2025-05-01 225918](https://github.com/user-attachments/assets/c28198df-b586-4600-a49f-035713e4a8e3)

-   Under **Metric**, let's use the following values:  
      
    

Namespace: **SecurityMetrics**

Metric name: `Secret is accessed`

Statistic: `Average`

Period: `5 minutes`

> 💡 **What do Statistic and Period mean?**
> 
> -   **Statistic** tells CloudWatch _how_ to analyze the CloudWatch metric. In this case, we're saying that the we're looking for the average number of times the secret is accessed.
>     
> -   **Period** is how often CloudWatch checks in on your metric - we've chosen 5 minutes. You can think of it as checking every 5 minutes to see if anyone accessed the secret during that time.
>     

![Start creating an alarm.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-105.png)

Start creating an alarm.

  

-   Under **Conditions**, set **Threshold type** to **Static**.
   
   ![Screenshot 2025-05-01 230016](https://github.com/user-attachments/assets/14ae4633-36a8-4b40-9c5b-b9706958c7f6) 

> 💡 **Extra for Experts: What does the other setting (anomaly detection) mean?**  
> Anomaly detection is where CloudWatch studies your metric over time (usually two weeks) to understand its typical patterns, including daily and weekly cycles. It then creates a band of "expected values" that automatically adjusts based on your workload.
> 
> While Static thresholds are better for clear security boundaries like "alert whenever my secret is accessed" (which is why we're using Static for this project), Anomaly Detection are great for metrics where "normal" changes over time or follows patterns. It reduces false alarm while still catching true anomalies that might indicate problems.

-   Set **Whenever SecretIsAccessed is...** to **Greater/Equal**.
    
-   Set **than...** to `1`.
    

> 💡 **What are alarm thresholds?**  
> The alarm threshold is **when** the alarm should trigger. We're setting up a static threshold so that your alarm goes off when the `SecretIsAccessed` metric is greater than or equal to `1` in a 5-minute period.
> 
> This is a very sensitive setting (i.e. it's easy for this alarm to go off) - which is great for high-security scenarios! In a real production environment, you might adjust this depending on how sensitive your secret is. For instance, if it's normal for your application to access a secret 10 times every 5 minutes, you might set a higher threshold to only alert on unusual access patterns.

![Alarm conditions set up.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-106.png)

Alarm conditions set up.

  



-   Select **Next**.
    

![Next button for configure actions.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-107.png)

Next button for configure actions.

  

-   We're now on the **Configure actions** page! This is _how_ we tell CloudWatch what to do when we want to be alerted.
    
-   Under **Notification**, keep the default setting **In alarm**
    

![Notifications.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-108.png)

Notifications.

 
 

-   Under the heading **Select a notification to the following SNS topic**, Select **Create new topic**.
    

![Topic name configured.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-109.png)

Topic name configured.

  ![Screenshot 2025-05-01 230323](https://github.com/user-attachments/assets/a8081d8c-2661-45d3-ac27-fbb59ef3e8ad)

-   Under **Topic name**, enter `SecurityAlarms`.
    

![Topic name configured.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-110.png)

Topic name configured.

  


-   Under **Email endpoints**, enter your email address that you can access. In the next step, you'll check this inbox for emails (when the alarm goes off)!
    

> 💡 **What is an SNS topic?**  
> An SNS (Simple Notification Service) topic is like a broadcast channel for your notifications. First, you create the channel (topic), then you invite subscribers (such as your email), and finally, you send messages to the topic. SNS automatically delivers that message to all subscribers.
> 
> The beauty of this approach is **flexibility** - you could start by just emailing yourself about security alerts, but later add a text message notification, trigger an automated response via Lambda, or even integrate with your team's Slack channel - all without changing how the alert is generated, just by adding more subscribers to your topic.

![SNS email endpoint configured.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-111.png)

SNS email endpoint configured.

  

-   Select **Create topic**.
    
-   The SNS topic should now be created!
    

![Your created topic.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-112.png)

Your created topic.

  
![Screenshot 2025-05-01 230343](https://github.com/user-attachments/assets/5d1b2edf-bb2b-48ad-9e08-7dfa541cbd5a)


-   Select **Next** - we'll head to add name and description for the alarm.
    

![Next button for name and description.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-114.png)

Next button for name and description.

![Screenshot 2025-05-01 230501](https://github.com/user-attachments/assets/3647c7b1-f3ae-43e5-bb3d-f3c6e83ac9ad)
  

-   Under **Alarm name**, enter `Secret is accessed`
    
-   Under **Alarm description**, enter a description like `This alarm goes off whenever a secret in Secrets Manager is accessed.`
    

![Alarm name and description entered.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-115.png)

Alarm name and description entered.

  ![Screenshot 2025-05-01 230547](https://github.com/user-attachments/assets/ac99a502-8d82-4329-99af-56dc723e79de)


-   Select **Next** to review and create the alarm.
    

![Next button for review and create.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-116.png)

Next button for review and create.

  

Let's review your alarm set up:  
  

Namespace: **SecurityMetrics**

Metric name: **Secret is accessed**

Statistic: **Average**

Period: **5 minutes**

![Let's review your alarm.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-117.png)

Let's review your alarm.

  ![Screenshot 2025-05-01 230713](https://github.com/user-attachments/assets/18113b85-02d2-471c-bb67-4e04bc8f1e80)


Threshold type: **Static**

Whenever Secret is accessed is: **Greater/Equal (>=)**

than...: **1**

Notification: **When In alarm, send a notification to "SecurityAlarms"**

![Let's review your alarm.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-118.png)

Let's review your alarm.

  ![Screenshot 2025-05-01 230724](https://github.com/user-attachments/assets/8e416206-7b3d-4aa4-b082-d698c37695aa)

Name: **Secret is accessed**

Description: **This alarm goes off whenever a secret is Secrets Manager is accessed.**

![Let's review your alarm.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-120.png)

Let's review your alarm.

  

-   Select **Create alarm**.
    

![Create alarm button on review page.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-121.png)

Create alarm button on review page.

  

-   You should see a green banner at the top confirming that your alarm was created!
    
-   There's also blue banner below it, telling us that a subscription is **pending confirmation.**
    

> 💡 **A subscription? What's that?**  
> Think of a subscription as an email address that will receive the messages you publish to your SNS topic.

![Create success!](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-122.png)

Create success!

  
![Screenshot 2025-05-01 230813](https://github.com/user-attachments/assets/f9644488-0160-40a7-8f55-2fd874a917fd)
  
  

**Confirm SNS Subscription**

-   Ooo check your created alarm's row too - there's a **Warning** sign under the **Actions** heading.
    
-   Select the warning sign.
    

> 💡 **What does this warning say?**  
> Just like the blue popup, this warning tells us that your alarm is allllllmost working. When you set up your email with SNS, AWS doesn't just start sending you emails right away - that would be a bit intrusive! Instead, they want to make sure it's really you asking for these alerts. That's why they've sent a confirmation email to your inbox.
> 
> You'll need to head into your email inbox to confirm your subscription to this alarm.

![Warning.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-124.png)

Warning.

  

-   Check your email inbox for an email from **AWS Notifications** with the subject `AWS notification - Subscription Confirmation`.
    
-   This email is to confirm your subscription to the SNS topic you created!
    

![Email confirmation request from AWS SNS.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-125.png)

Email confirmation request from AWS SNS.

  ![Screenshot 2025-05-01 230855](https://github.com/user-attachments/assets/27d22de6-dc11-4f0e-910c-064b7e3ba9da)


-   Select **Confirm subscription**.
    
-   You should now see a **Subscription confirmed!** page in your browser.
    

![SNS subscription confirmation page.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-126.png)

SNS subscription confirmation page.

  ![Screenshot 2025-05-01 230938](https://github.com/user-attachments/assets/5ce6d8f5-2734-4da9-9800-f2dbf3c01c0c)

![Screenshot 2025-05-01 231050](https://github.com/user-attachments/assets/01ada42f-61b3-4a77-9dfe-d9f67308987e)

**Excellent! You've set up a CloudWatch Alarm and SNS topic.** Now, let's test the email notification in the next step.

----
## 💎 Secret Mission

### Apply your Solutions Architect skills

Now that we've built out an entire monitoring system, you might be wondering _why_ this solution has as many components as it does.

There's CloudTrail, CloudWatch, alarms, SNS and more! So if we took away CloudWatch and alarms from the solution... what do you think would happen?

Your secret mission, should you choose to accept it, is to configure **direct CloudTrail notifications** and compare that against using CloudWatch and alarms. This challenge will build your **critical thinking** skills around how architecture decisions (like using CloudWatch) are made when building cloud solutions (like this monitoring system).

  
  

**In this secret mission, you're going to:**

-   Configure direct SNS notifications from CloudTrail
    
-   Compare notification methods between CloudWatch and CloudTrail
    
-   Showcase advanced **cloud architecture decision-making skills** in your documentation!
    

![What we're doing in this secret mission.](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-secret-mission.png)

What we're doing in this secret mission.

  

> 💎 **Congratulations** - Secret Mission unlocked!

**Configure Direct CloudTrail SNS Notifications**

-   Head to the `CloudTrail` console again.
    

![CloudTrail service in services menu.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-166.png)

CloudTrail service in services menu.

  

-   In the left navigation pane, select **Trails**.
    
-   Select your trail `nextwork-secrets-manager-trail` in the list.
    

![Select your nextwork-secrets-manager-trail in Trails list.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-167.png)

Select your nextwork-secrets-manager-trail in Trails list.

 ![Screenshot 2025-05-01 231321](https://github.com/user-attachments/assets/a827adfb-c0a0-4cea-93b6-04889030cc94) 

-   You should now be on the detail page for your trail.
    
-   Select **Edit** in the General details section.
    

![Edit General details in CloudTrail.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-168.png)

Edit General details in CloudTrail.

  ![Screenshot 2025-05-01 231331](https://github.com/user-attachments/assets/53318690-224a-412b-8991-d592d1399d82)

-   Scroll down to the **SNS notification delivery** section.
    
-   Check the **Enabled** checkbox to enable direct SNS notifications from CloudTrail.
    

![Enable SNS notification delivery in CloudTrail.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-169.png)

Enable SNS notification delivery in CloudTrail.

  

-   Select **Use existing SNS topic**.
    
-   From the dropdown menu, select your existing SNS topic `SecurityAlarms` that you created earlier.
    

> 💡 **What does SNS notification delivery do in CloudTrail?**  
> When you enable SNS notification delivery in CloudTrail, it will send a notification to your SNS topic **every time** a new log file is delivered to your S3 bucket. This is different from your CloudWatch Alarm, which only triggers when a specific pattern (like accessing your secret) is detected in the logs.

![Select existing SNS topic for CloudTrail notifications.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-170.png)

Select existing SNS topic for CloudTrail notifications.

  ![Screenshot 2025-05-01 231432](https://github.com/user-attachments/assets/02f599e0-d52c-4bdf-989f-b2f36b2e8c05)

-   After selecting the SNS topic, scroll down and select **Save changes**.
    

![Save CloudTrail changes with SNS notification enabled.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-171.png)

Save CloudTrail changes with SNS notification enabled.

  

  
  

**Access Your Secret Again**

-   Now that we have direct CloudTrail SNS notifications set up, let's generate another secret access event.
    
-   Head back to the `Secrets Manager` console.
    

![Secrets Manager service in AWS Console.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-0.png)

Secrets Manager service in AWS Console.

  

-   Navigate to your `TopSecretInfo` secret again.
    
-   Select **Retrieve secret value** to access the secret.
    
-   This will trigger another secret access event that should now be captured by both our CloudWatch Alarm and the direct CloudTrail notifications.
    

![Retrieve secret value button.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-38.png)

Retrieve secret value button.

  ![Screenshot 2025-05-01 231518](https://github.com/user-attachments/assets/5142e8d3-fde6-4a9c-8b3c-559d8b798e8c)


  
  

**Check Your Email for CloudTrail Notifications**

-   Wait a few minutes for CloudTrail to deliver the log files to S3 and send notifications.
    
-   While we wait...
    


-   Check your email inbox again.
    
-   Look for new email notifications from AWS Notifications with subjects related to CloudTrail.
    

![CloudTrail validation message email.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-172.png)

CloudTrail validation message email.

![Screenshot 2025-05-01 231835](https://github.com/user-attachments/assets/91f7f4dc-266f-4944-8b08-bfc70ad4720d)

  

-   In fact should see _several_ new emails from CloudTrail SNS notifications.
    

![New messages notification in inbox.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-184.png)

New messages notification in inbox.

  ![Screenshot 2025-05-01 232250](https://github.com/user-attachments/assets/76c6b83a-d535-43df-91ee-3eaee2b45acd)



> 😭 **Ahhhh - that's too many emails!**  
> Right?! The huge wave of emails will continue to happen as long as you keep your trail's SNS notification setting on, and there is any activity in your account.
> 
> Recap: CloudTrail typically batches events over a period (usually 5-15 minutes) and creates a new log file each time, triggering an SNS notification for each file. Since CloudTrail captures all kinds of management events happening in your AWS account - not just secret access - you end up with multiple log files and therefore multiple notifications.
> 
> This is actually why the CloudWatch Alarm approach is more **targeted and useful** for specific event monitoring like tracking secret access. With CloudWatch, you're filtering for exactly the events you care about and only triggering notifications when those specific conditions are met.
> 
> In a production environment, direct CloudTrail SNS notifications are usually sent to comprehensive security monitoring systems or audit tools that process all your AWS activity logs programmatically, while CloudWatch alarms are better for specific, actionable alerts that humans need to respond to.



**Stop emails from CloudTrail**

-   Head to the `CloudTrail` console again.
    

![CloudTrail service in services menu.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-166.png)

CloudTrail service in services menu.

  

-   In the left navigation pane, select **Trails**.
    
-   Select your trail `nextwork-secrets-manager-trail` in the list.
    

![Select your nextwork-secrets-manager-trail in Trails list.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-167.png)

Select your nextwork-secrets-manager-trail in Trails list.

  ![Screenshot 2025-05-01 232429](https://github.com/user-attachments/assets/64a78ea7-a452-44d0-9aa1-3825fb90d893)



-   You should now be on the detail page for your trail.
    
-   Select **Edit** in the General details section.
    

![Edit General details in CloudTrail.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-168.png)

Edit General details in CloudTrail.

  ![Screenshot 2025-05-01 232440](https://github.com/user-attachments/assets/121a0a1e-5798-4a68-a6d3-0b51aa1e0677)


-   Scroll down to the **SNS notification delivery** section.
    
-   _Uncheck_ the **Enabled** checkbox to disable direct SNS notifications from CloudTrail.
    
![Screenshot 2025-05-01 232746](https://github.com/user-attachments/assets/a42325d0-ac22-4942-b8ae-2c02e466e2b7)



  
----
## 💌 Step #6


Test Email Notification

Let's test if our email notification system works as expected. We'll trigger the alarm by accessing the secret again and check if we receive an email notification.

  
  

**In this step, you're going to:**

-   Retrieve your secret value again to trigger the alarm.
    
-   Troubleshoot your monitoring system - why aren't you getting notified?
    

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-6.png)

  
![Screenshot 2025-05-01 233215](https://github.com/user-attachments/assets/166e064d-7a78-47a7-adf0-d7740dc7c109)



  
  

**Trigger Alarm**

-   Head back to the **Secrets Manager** console. Let's try to trigger our own alarm by retrieving the secret value again!
    

> If you'd like, you could choose to retrieve the secret value over CloudShell instead - do you remember how to do it? Give it a go!
> 
> ![Using CloudShell to access the secret, if you're cool like that](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-163.png)
> 
> Using CloudShell to access the secret, if you're cool like that
> 
>   
![Screenshot 2025-05-01 233340](https://github.com/user-attachments/assets/b635f5a2-2533-45d2-8dbf-5ff25571c91f)

-   Head to your `TopSecretInfo` secret again.
    
    ![Screenshot 2025-05-01 233413](https://github.com/user-attachments/assets/f3961e41-289d-4b6a-966f-d9bbbfb9d069)

![TopSecretInfo secret.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-132.png)

TopSecretInfo secret.

  ![Screenshot 2025-05-01 233423](https://github.com/user-attachments/assets/fe0241b6-3d70-4bb9-b560-5701cca25d33)

-   Select **Retrieve secret value.**
    

![Retrieve secret value.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-134.png)

Retrieve secret value.

  ![Screenshot 2025-05-01 233557](https://github.com/user-attachments/assets/60436ded-b8c7-4daa-af81-26b15804a952)


-   Aha! Secret exposed again!
    

![Secret exposed!](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-135.png)

Secret exposed!
![Screenshot 2025-05-02 001717](https://github.com/user-attachments/assets/e3891ff8-adba-4c42-84df-3e9808a3bfc8)
  

-   What do you think will happen now - are you going to get the alert email about your secret getting accessed?
    
-   Check your email inbox after a few minutes (it might take up to 5 minutes for the alarm to trigger and the email to arrive).
    

> 🙋‍♀️ **Ummmm, I didn't get an email**  
> Huh, neither did we... Looks like we have some troubleshooting to do (yay)!
> 
> You're super close to the finish line - this is the final thing to do before you see a working monitoring and notification system. You've GOT THIS 🔥



Looks like we're not receiving the email after we trigger the alarm! This is actually a common scenario in real-world cloud environments.

Setting up a monitoring system is one thing, but making sure all the parts work together correctly often requires some troubleshooting.

  
  

**Troubleshoot Your Notification Setup**

There are a few places in our monitoring system where things could be breaking:

**CloudTrail** didn't record the `GetSecretValue` event.

CloudTrail isn't **sending logs** to CloudWatch.

CloudWatch's **metric filter** isn't filtering logs correctly.

CloudWatch's **Alarm** isn't triggering an action.

**SNS** isn't delivering emails to you.

  
## Cloud trail

Do we think CloudTrail actually recorded the event? What if CloudTrail missed it, and didn't know you've retrieved your secret's value?
![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-error1.png)
You've done this before in 😈 Step #3  
and we'll do it again! Do you remember how to check your CloudTrail logs?

-   Head to the CloudTrail console again.
    
![CloudTrail service in services menu.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-48.png)
-   You should now be on the **CloudTrail** dashboard.
    
-   In the left navigation pane, select **Event history**.
    
![Event history page.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-51.png)

![Screenshot 2025-05-01 233924](https://github.com/user-attachments/assets/b768a35d-e14e-4abd-88b0-ec7a8a3c9890)

-   Under **Lookup attributes**, select the dropdown and choose **Event source**.
    
![Event source selected in lookup attributes.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-52.png)
-   In the search bar next to **Event source**, enter secretsmanager.amazonaws.com
    
![secretsmanager.amazonaws.com entered in search bar.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-53.png)
-   You should see at least one GetSecretValue event at the top of the list, which matches the time you viewed your secret. There should be more than one row, since it's now your second time retrieving a secret.
    
![GetSecretValue events in CloudTrail event history.](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-25.png)
Nice - that should mean CloudTrail _did_ capture the event!

![Screenshot 2025-05-01 234011](https://github.com/user-attachments/assets/9b0a0d38-ce8d-41e1-9164-096fd73cdeeb)

![Screenshot 2025-05-01 234331](https://github.com/user-attachments/assets/eeea56d4-d63d-4283-91a4-73ffba6e7ba1)

![Screenshot 2025-05-01 234405](https://github.com/user-attachments/assets/84da9330-8855-4ffb-ba56-355b8cb54cbe)

![Screenshot 2025-05-01 234433](https://github.com/user-attachments/assets/2ffc137d-5c69-488a-8724-03fb353ebbc2)
> ⬆️ Don't forget to jump back up to the top of these tabs!
> 
> Let's check off all the troubleshooting steps.  


## Log delivery

Hmmm... could it be that CloudTrail isn't sending Logs to CloudWatch?

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-error2.png)

  

-   Stay in the `CloudTrail` console.
    
-   Select **Trails** in the left navigation pane.
    
-   Click on your `secrets-manager-trail`.
    
-   Check the **Last log file delivered** timestamp - it should be recent if logs are being delivered properly!
    

> 🙋‍♀️ **I don't see a last delivery timestamp!**  
> If CloudTrail isn't delivering logs to CloudWatch:
> 
> -   Click **Edit** next to CloudWatch Logs.
>     
> -   Ensure **Enabled** is checked.
>     
> -   Verify the log group name is correct.
>     
> -   Make sure the IAM role has permissions to write to CloudWatch Logs.
>     
> -   Save your changes.
>     

-   Scroll down to the **CloudWatch Logs** section.
    
-   Make sure it shows the correct log group name i.e. `nextwork-secretsmanager-loggroup`.
    

  
  

Nice - that should mean CloudTrail _is_ sending logs over to CloudWatch!

> ⬆️ Don't forget to jump back up to the top of these tabs!
> 
> Let's check off all the troubleshooting steps.






## Metric Filter
What if something went wrong with the CloudWatch metric filter? Maybe the filter is rejecting the events we're actually trying to capture...

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-error3.png)

-   Head to the CloudWatch console.
    
-   In the left navigation pane, select **Log groups**.
    
![Screenshot 2025-05-01 234456](https://github.com/user-attachments/assets/47b71f7f-a42d-46f6-a3c5-61ca7ae1dc7f)
-   Find and click on your nextwork-secretsmanager-loggroup.
    
-   Select the **Metric filters** tab.

![Screenshot 2025-05-01 234632](https://github.com/user-attachments/assets/08ce5092-a7bd-4fb9-b7ad-d7fcff3a0dd0)
    
-   Check the checkbox for your filter GetSecretsValue and select **Edit**.

![Screenshot 2025-05-01 234812](https://github.com/user-attachments/assets/1a1dd8fe-e63e-42a7-92ea-24b94ef2405d)
    
-   Let's put your filter to the test! Here's a bunch of test log events. Enter them in the **Log event messages** panel.

```
{"Records":[
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAXXXXXXXXXXXXXXXX","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T18:44:29Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetSecretValue","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"1471f5f6-aee8-4c56-92c8-eadd8ea4b3a2","eventID":"06e83132-44aa-412c-8e1d-da427a6dc6b1","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAXXXXXXXXXXXXXXXX","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T18:44:27Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetResourcePolicy","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"6ca2b8cb-1da9-4f0b-8e2d-244aa0ef95d0","eventID":"88a52c53-19ce-4341-a49f-e08a07fc1c32","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAXXXXXXXXXXXXXXXX","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T10:18:06Z","eventSource":"secretsmanager.amazonaws.com","eventName":"ListSecretVersionIds","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68","maxResults":100},"responseElements":null,"requestID":"9541d6b3-10c7-4356-aedf-9da4a0bebb67","eventID":"ac01a292-7781-408c-a04c-c41e9dfb241f","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAXXXXXXXXXXXXXXXX","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T10:18:01Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetResourcePolicy","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"5c396be9-cf7e-4815-9dc9-043625394106","eventID":"f1b6f551-66d9-46c3-a6b4-3adfc6948fcd","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAXXXXXXXXXXXXXXXX","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T10:17:54Z","eventSource":"secretsmanager.amazonaws.com","eventName":"ListSecretVersionIds","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68","maxResults":100},"responseElements":null,"requestID":"a2e29de0-0f66-48e0-948e-777c821c3f56","eventID":"32a3cc8f-12d2-41f9-8ead-7f499ef87980","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAXXXXXXXXXXXXXXXX","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T10:17:50Z","eventSource":"secretsmanager.amazonaws.com","eventName":"DescribeSecret","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"TopSecretInfo"},"responseElements":null,"requestID":"b6504118-1361-46b0-a1af-229f5701924e","eventID":"a559b1cb-6633-451e-914c-993f1eb77bc6","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAXXXXXXXXXXXXXXXX","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T10:17:50Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetResourcePolicy","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"cca46a10-d504-4d42-b8a0-e3df56907c13","eventID":"c97eb70f-6eaa-46c7-830c-118672429622","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAF2VAB6VVO","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T10:16:39Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetSecretValue","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"3cc2aa25-f1cd-429f-9ede-7bd245fb8263","eventID":"8948ce7e-42bc-4f01-848d-09439980b454","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAF2VAB6VVO","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T10:14:26Z","eventSource":"secretsmanager.amazonaws.com","eventName":"DescribeSecret","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"TopSecretInfo"},"responseElements":null,"requestID":"ab02eb00-acfa-4dcf-802b-8feb329c1534","eventID":"2517d82f-b182-4bcd-9b60-f14545addf00","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAF2VAB6VVO","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T10:14:26Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetResourcePolicy","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"92d2f0c3-30ca-4d1c-a858-1bd691e97a83","eventID":"b7913e5c-dabf-464b-89fd-760185a82902","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAF3UQQZW7R","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T10:11:42Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetResourcePolicy","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"5a820410-fa2e-41be-89b4-a56a9b60c310","eventID":"58daeab8-96b4-42f7-9f8d-a3ced4246480","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAF3UQQZW7R","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T10:11:42Z","eventSource":"secretsmanager.amazonaws.com","eventName":"DescribeSecret","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"TopSecretInfo"},"responseElements":null,"requestID":"de945614-69f1-462f-8ca0-2b45fd8bd85f","eventID":"a63ef733-892d-429e-8afb-2dd2b18f969d","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAFYGPUHL43","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T09:34:11Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetSecretValue","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"048367e2-093a-411c-a23f-7c2784a2ce3b","eventID":"98012fdf-147c-49a1-903a-6cb7ce80d24e","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAFYGPUHL43","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T09:34:08Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetResourcePolicy","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"b4e9ad41-1e3b-4d0e-a5f2-705ebb8bbf1a","eventID":"0f34638c-c399-4e81-80e2-b349e1e5e0ee","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAFYGPUHL43","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-19T09:17:54Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-19T09:34:08Z","eventSource":"secretsmanager.amazonaws.com","eventName":"DescribeSecret","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"TopSecretInfo"},"responseElements":null,"requestID":"b812abcb-f102-4c57-b99e-43702b73f377","eventID":"643a639f-a697-4990-875d-b716e60a2cbb","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAFXQ3ZA6E6","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-17T21:06:59Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-17T23:21:57Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetSecretValue","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"5462961f-9a07-4ac0-89ac-358bda01422d","eventID":"c4c54144-834e-4b61-afba-58107f102e82","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAFXQ3ZA6E6","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-17T21:06:59Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-17T23:20:47Z","eventSource":"secretsmanager.amazonaws.com","eventName":"GetResourcePolicy","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"responseElements":null,"requestID":"e57086d3-6562-422e-9030-500cb09377a3","eventID":"41fe58d3-5279-4c91-82af-9a34ea1a3092","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAFXQ3ZA6E6","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-17T21:06:59Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-17T23:20:47Z","eventSource":"secretsmanager.amazonaws.com","eventName":"DescribeSecret","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"secretId":"TopSecretInfo"},"responseElements":null,"requestID":"c0d24117-034a-42dc-b296-cf54667f958a","eventID":"9230b624-5280-4f93-9304-e3eff8671113","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAF5BIR5VCI","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-17T21:06:59Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-17T22:40:42Z","eventSource":"secretsmanager.amazonaws.com","eventName":"CreateSecret","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","requestParameters":{"name":"TopSecretInfo","clientRequestToken":"6d546fbc-ebd0-45a7-8ddc-3617337d741f","description":"Secret for monitoring project","forceOverwriteReplicaSecret":false},"responseElements":{"arn":"arn:aws:secretsmanager:us-west-2:00000000000:secret:TopSecretInfo-lvRO68"},"requestID":"c206b241-000e-4bcc-88da-bb78208ea93e","eventID":"cb618040-e1ec-4102-a39d-f4670210f08f","readOnly":false,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"},
{"eventVersion":"1.11","userIdentity":{"type":"IAMUser","principalId":"AIDAXXXXXXXXXXXXXXXX","arn":"arn:aws:iam::00000000000:user/IAM-Admin","accountId":"00000000000","accessKeyId":"ASIAW3MEFRAF5BIR5VCI","userName":"IAM-Admin","sessionContext":{"attributes":{"creationDate":"2025-03-17T21:06:59Z","mfaAuthenticated":"false"}}},"eventTime":"2025-03-17T22:36:14Z","eventSource":"secretsmanager.amazonaws.com","eventName":"DescribeSecret","awsRegion":"us-west-2","sourceIPAddress":"000.00.00.00","userAgent":"Some user agent info here","errorCode":"ResourceNotFoundException","errorMessage":"Secrets Manager can't find the specified secret.","requestParameters":{"secretId":"TopSecretInfo"},"responseElements":null,"requestID":"8ac10643-61cf-462a-9cde-70a522f26670","eventID":"2b9df39e-9c8a-4bb2-a880-995800ebe35f","readOnly":true,"eventType":"AwsApiCall","managementEvent":true,"recipientAccountId":"00000000000","eventCategory":"Management","tlsDetails":{"tlsVersion":"TLSv1.3","cipherSuite":"TLS_AES_128_GCM_SHA256","clientProvidedHostHeader":"secretsmanager.us-west-2.amazonaws.com"},"sessionCredentialFromConsole":"true"}]}
```
> 💡 **What is this test log data?**  
> This block of text contains sample CloudTrail log entries that simulate various activities related to AWS Secrets Manager. Each entry represents a different API action that might occur when interacting with your secrets.
> 
> The data is formatted as JSON and includes multiple event records showing different operations like GetSecretValue (accessing a secret), DescribeSecret (viewing secret metadata), CreateSecret (creating a new secret), and other common Secrets Manager actions.
> 
> We're providing this test data so you can easily validate your metric filter without having to generate many different types of events yourself. When you paste this into the test field, CloudWatch will analyze it using your filter pattern and highlight which events match your criteria (in this case, looking for GetSecretValue events).
> 
> This is a common technique used by AWS administrators to test their monitoring rules before deploying them to production environments.

-   Select **Test pattern**.
    
![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-19.png)

-   Aha! Some successfull results.

![Screenshot 2025-05-01 234835](https://github.com/user-attachments/assets/591a9964-207d-4de1-9505-2726461c8f67)

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-20.png)

-   If you scroll further down the results, you'll notice that they record an event called GetSecretValue
![Screenshot 2025-05-01 235500](https://github.com/user-attachments/assets/3f492c86-2272-4825-83f0-aee87dbaa10f)
    
![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-21.png)

This tells us the metric filter _does_ correctly filter for events where your secret is accessed.
![Screenshot 2025-05-01 235527](https://github.com/user-attachments/assets/c1801399-e5b7-4cc0-bf04-ff76107eca45)

> ⬆️ Don't forget to jump back up to the top of these tabs!
> 
> Let's check off all the troubleshooting steps.


Alarm Configuration

Maybe your CloudWatch alarm isn't getting triggered properly?

Let's see if the alarm can be triggered at all.

  ![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-error5.png)

**Trigger the alarm manually**

-   Open **AWS CloudShell.**
    
![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-23.png)
-   First, let's learn about how to write a CLI command for manually triggering

```
aws cloudwatch set-alarm-state help

```

-   Nice! We get an introduction to the cloudwatch set-alarm-state command. Continuing scrolling down the terminal response by pressing the down arrow on your keyboard.
    
-   This will show you the exact syntax and required parameters, which are:
    
    -   --alarm-name: The name of the CloudWatch alarm
        
    -   --state-value: Possible values are ALARM, OK, or INSUFFICIENT_DATA
        
    -   --state-reason: Some text explaining why you're changing the state

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-24.png)

![Screenshot 2025-05-01 235921](https://github.com/user-attachments/assets/b09f2f97-93f5-4f17-9386-677fcd02e26b)
-   Gotcha! Let's manually set the alarm to ALARM state.
    
-   First, run q in the CloudWatch terminal to quit 'reading' mode.
    
-   Next, let's trigger our alarm manually.

```
aws cloudwatch set-alarm-state \
    --alarm-name "Secret is accessed" \
    --state-value ALARM \
    --state-reason "Manually triggered for testing"

```
-   Check your email inbox. There should be a notification email that your alarm is in alarm, and Manually triggered for testing as the resason!
    

> 🙋‍♀️ **I didn't get an email!**  
> Ah interesting! Here are some troubleshooting tips:
> 
> -   Check your alarm - is it in **in alarm** state? If it's not - maybe the command didn't work properly.
>     
> -   Make sure you use the exact alarm name in your command as it appears in CloudWatch
>     
> -   Wait a few minutes for the email to land in your inbox, and check your spam.
>     
> -   Make sure your SNS subscription is in **Confirmed** state.
>

**Adjust Your Alarm Settings**

Hmm... so we know the alarm _can_ trigger an email. Since it's not triggering an email at the moment, we're down to the final investigation. Maybe your CloudWatch alarm isn't being triggered when it should!

Let's check a few critical settings:

-   Head back to the CloudWatch console.
    
-   Select **All alarms** from the left hand navigation panel.
    
-   Check the checkbox for your alarm.
    
-   Select the **Actions** dropdown, and select **Edit**.
    
![Screenshot 2025-05-02 000135](https://github.com/user-attachments/assets/2e7204f7-aaab-4a28-9fb0-308d19c2c1b4)
-   On the alarm details page, look at the **Statistic** field.
    
-   Aha - maybe the statistic should be set to **Sum**, not **Average** or any other statistic!
    
-   This is crucial because:
    
    -   **Sum** adds up **all** occurrences of secret access in the period (what we want).
        
    -   **Average** would calculate an average rate (i.e. the average number of times our secret was accessed _per second_ over the 5 minute period), which might never cross our threshold.
        

  

-   Change the **Statistic** dropdown from **Average** to **Sum**.
    
-   You can also update the **Period** from **5 minutes** to **1 minute**, so we can trigger the alarm even faster when we see the Secret's value.
    
    ![Change statistic to Sum in alarm configuration](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-150.png)

-   Check that the **Threshold type** is set to **Static**.
    
-   Confirm that the condition is **Greater/Equal than 1**.
    
-   Select **Skip to Preview and create**.
    
-   In the review page, make sure **Statistic** is now **Sum**.
    
-   Select **Update alarm** at the bottom of the page.
   ![Screenshot 2025-05-02 000300](https://github.com/user-attachments/assets/cd5b1a81-2510-414a-b4c8-61d05be028eb) 

![Screenshot 2025-05-02 000325](https://github.com/user-attachments/assets/fe55d55f-2aec-454a-86ae-7b301958f0cd)

![Screenshot 2025-05-02 000334](https://github.com/user-attachments/assets/15e81c11-d843-4a84-9f2c-7d29f2d9f520)


![Screenshot 2025-05-02 000347](https://github.com/user-attachments/assets/46944dd6-7099-43c2-a930-ce4b3193e1ac)

> ⬆️ Don't forget to jump back up to the top of these tabs!
> 
> Let's check off all the troubleshooting steps.

## SNS Subscription

  > Aha! If you're here because you skipped to the last one, we see you! Try again 😼

Since we've confirmed our email's subscription to SNS, surely that means you should be receiving emails?

Let's confirm this by going directly to **SNS** 🏃

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-error6.png)

-   Head to the SNS console.
    
![](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-136.png)

-   In the left hand navigation panel, select **Topics**.
- 
![Screenshot 2025-05-02 000435](https://github.com/user-attachments/assets/67d18176-782d-43bf-bd37-000508f3695e)
  
  ![Screenshot 2025-05-02 000542](https://github.com/user-attachments/assets/45c1b868-3fdd-489d-b85d-3f8d72d67d38)
    
![](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-138.png)

-   Select your topic i.e. SecurityAlarms
    ![](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-140.png)

![Screenshot 2025-05-02 000609](https://github.com/user-attachments/assets/3d5ed601-2565-41b9-8aad-d240a12b266e)

-   Select **Publish message**. Let's try to manually send a message to all the emails subscribed to this topic!
 ![](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-142.png)
    
![Screenshot 2025-05-02 000641](https://github.com/user-attachments/assets/e4de6bb6-d2f6-4e5c-8f51-6895683d8d65)

-   Add a message **Subject** like Testing
    
-   In the **message body**, enter a quick message like Wassup
    
![](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-143.png)
-   That's it! Select **Publish message**.
    
![Screenshot 2025-05-02 000719](https://github.com/user-attachments/assets/022998a7-642b-4e34-9029-f799720c4232)

> 💡 **Extras for Experts: What are the Message attributes we skipped?**  
> **Message attributes** are extra bits of information about the SNS message itself - like the timestamps, location data, signatures, or IDs - that you can send along with your main message. Think of it as your message's metadata!
> 
> The cool thing is that whoever receives your message can check these attributes (or use automatic filters) to figure out what to do with it without having to open the message. For example, a banking app might use message attributes to mark certain notifications as "urgent" or "standard," allowing receiving systems to prioritize the processing of critical alerts.
> 
> For our project, we're keeping things simple and skipping these extras, but they're super handy when you need more sophisticated message handling!

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/new-22.png)

-   You should see a confirmation message at the top of the page.
    
![](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-145.png)
-   Let's dash back to your inbox - it's the moment of truth! _Can_ SNS send emails to you?
    
![Screenshot 2025-05-02 000736](https://github.com/user-attachments/assets/062bf2d0-1d4a-41c8-8aae-8b2da6e18ec7)

-   Ooo, message received!
    

> 🙋‍♀️ **Wait, I didn't receive an email!**  
> Hmmmm, looks like we have a side quest to do back in your **SNS** console:
> 
> -   Head back to the SNS service
>     
> -   In the left navigation pane, select **Subscriptions**.
>     
> -   Look for your email subscription in the list.
>     
> -   Check the **Status** column - it should say "Confirmed". If it says "Pending confirmation," that's our issue!
>     
> -   Check your email inbox (including spam/junk folders) for an email from AWS Notifications.
>     
> -   Open the confirmation email and click on the **Confirm subscription** link.
>     
> -   If you can't find the confirmation email, you can request a new one by selecting your subscription and choosing **Request confirmation** from the **Actions** menu.
>     
> 
>   

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-147.png)
This means SNS is actually set up properly (no issues here either, haha)

![Screenshot 2025-05-02 000759](https://github.com/user-attachments/assets/7603e4fd-a935-4044-b370-e109f76afb78)

> ⬆️ Don't forget to jump back up to the top of these tabs!
> 
> Let's check off all the troubleshooting steps.
  

🏁 **Only continue below when you've completed all the troubleshooting steps!**



Let's try accessing the secret again after you've made these fixes, and see if you receive a notification this time!

  
  

**Access Your Secret Again**

-   Now that we have direct CloudTrail SNS notifications set up, let's generate another secret access event.
    
-   Head back to the `Secrets Manager` console.
    

![Secrets Manager service in AWS Console.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-0.png)

Secrets Manager service in AWS Console.

  

-   Navigate to your `TopSecretInfo` secret again.
    
-   Select **Retrieve secret value** to access the secret.
    
-   This will trigger another secret access event that should now be captured by both our CloudWatch Alarm and the direct CloudTrail notifications.
    

![Retrieve secret value button.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-38.png)

Retrieve secret value button.

  

  
  

**Verify Your Alarm**

-   Head back to the `CloudWatch` console.

![Screenshot 2025-05-02 001801](https://github.com/user-attachments/assets/4f19df3b-a807-4324-b765-921a15259107)
    
-   Refresh your **Secret is accessed** alarm.
    
-   It should be in the **In alarm** state!
    

![CloudWatch Alarm in ALARM state](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-164.png)

CloudWatch Alarm in ALARM state

  ![Screenshot 2025-05-02 002213](https://github.com/user-attachments/assets/519a8966-411c-4530-8b5f-61242fd94865)

-   You should receive notifications now.
    
    ![Screenshot 2025-05-02 002012](https://github.com/user-attachments/assets/85f2305b-975c-4d63-91a9-0b15bdf17097)

> 🙋‍♀️ **My alarm isn't in alarm**  
> Try retrieving your secrets value again, and wait 2-5 minutes. It can take up to 5 minutes for CloudTrail pick up on the event and for CloudWatch to sound the alarm!
> 
> If it's still not in alarm after 5 minutes (and you've accessed the secret multiple times), there's an issue with the metric or filter. Double check that you've ticked off everything in the troubleshooting tips (you can do this).



Is this a success?!

-   Now that you see your alarm in **alarm** state, head back to your inbox!
    
-   Look for an email from **AWS Notifications** with the subject `ALARM: "SecretIsAccessedAlarm"`.

![Screenshot 2025-05-01 235936](https://github.com/user-attachments/assets/04a054b6-6306-49ef-8b45-7f75772e16bb)
    
-   YESSSSSS - that's your monitoring system at work!
    

![Email notification from AWS SNS.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-165.png)

Email notification from AWS SNS.

  
![Screenshot 2025-05-01 235936](https://github.com/user-attachments/assets/45e4c8ba-90f1-47da-a0c9-459efe569bca)


**Congratulations!**

You've successfully set up and tested your secret access monitoring and notification system. You should now receive email alerts whenever your secret is accessed.

---
## 🗑️ Before you go

### Delete your resources

It's important to clean up the resources we created in this project - it saves us from getting charged!

  
  

**Resources to delete:**

The **CloudTrail** trail.

The **S3** bucket for CloudTrail logs.

The **CloudWatch** alarm and log group.

The **Secrets Manager** secret.

The **SNS** topic and subscription.

  
  

## CloudTrail

-   Head to the CloudTrail console.
    
-   Select **Trails** in the left navigation pane.
    
-   Select the checkbox next to secrets-manager-trail.
    
-   Select **Delete**.

![Screenshot 2025-05-02 003800](https://github.com/user-attachments/assets/53447264-58f0-4f60-8fc1-1cab910939f5)
    
-   In the confirmation dialog box, type Delete to confirm deletion.
    
-   Select **Delete**.

![Screenshot 2025-05-02 003811](https://github.com/user-attachments/assets/fde9d23a-0b7e-4621-a008-07c2c582caba)



## S3

-   Head to the S3 console.
    
-   Select **Buckets** in the left navigation pane.
    
-   Select your CloudTrail S3 bucket (e.g., nextwork-secrets-manager-trail-yourinitials).

![Screenshot 2025-05-02 003119](https://github.com/user-attachments/assets/c4f0ef65-dc9d-4d69-8999-740a9fe6ae01)
    
-   Select **Empty** to empty the bucket before deletion.
    
-   In the confirmation dialog box, type permanently delete to confirm.
    
-   Select **Delete objects**.

![Delete S3 bucket objects dialog.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-197.png)    

![Screenshot 2025-05-02 003352](https://github.com/user-attachments/assets/1f80fca9-a39c-4259-b704-105ffd3cd56a)

![Screenshot 2025-05-02 003405](https://github.com/user-attachments/assets/24903726-7418-4791-85de-cafaed2d4c56)

-   Wait until the bucket is empty.
    
-   Select your CloudTrail S3 bucket again.
    
-   Select **Delete**.

![Delete S3 bucket action.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-200.png)
    

-   In the confirmation dialog box, enter your bucket name to confirm deletion.
    
-   Select **Delete bucket**.
  ![Confirm delete S3 bucket dialog.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-205.png)

  ![Screenshot 2025-05-02 003428](https://github.com/user-attachments/assets/53e5a780-f5cf-4c8b-a9f3-f684b0fd82c3)

-   The S3 bucket should now be deleted.

![Screenshot 2025-05-02 003441](https://github.com/user-attachments/assets/91fe75e7-9920-413a-86ab-3bde27bbfd41)

## CloudWatch

**Alarm**

-   Head to the CloudWatch console.
    
-   Select **Alarms** in the left navigation pane.
    
-   Select the checkbox next to SecretIsAccessedAlarm.
    
-   Select **Actions** and then **Delete** from the dropdown menu.
    
    ![Delete alarm action.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-175.png)

![Screenshot 2025-05-02 004046](https://github.com/user-attachments/assets/ff878fda-e253-4d60-814d-841ac680d0ff)

-   Select **Delete** to confirm the deletion.
    
![Confirm delete alarm dialog.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-176.png)
  

![Screenshot 2025-05-02 004055](https://github.com/user-attachments/assets/b30eda41-c685-45dc-a6d3-e89923868ae3)


**Log group**

-   Select **Log groups** in the left navigation pane.
    
-   Search for and select the checkbox next to nextwork-secretsmanager-loggroup.
    
-   Select **Actions** and then **Delete log group(s)** from the dropdown menu.
    
-   In the confirmation dialog, select **Delete** to confirm the deletion.

![Screenshot 2025-05-02 004150](https://github.com/user-attachments/assets/3f700cf2-431d-49ab-9e0d-05440c7e73f3)
    
-   The log group should now be deleted from the CloudWatch Log groups list.

![Screenshot 2025-05-02 004158](https://github.com/user-attachments/assets/ab9cd0ed-2760-45db-8828-c13c9ce744ed)

## Secrets Manager

-   Head to the Secrets Manager console.
    
-   Select **Secrets** in the left navigation pane.
    
-   Select the checkbox next to TopSecretInfo secret.
    
-   Select **Actions** and then **Delete secret** from the dropdown menu.

![Delete secret action.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-179.png)    

-   Welcome to the **Schedule secret deletion** page!
    
-   Under **Schedule secret deletion**, set the **Waiting period** to 7 days (default).
    
-   Select **Schedule deletion**.
    
    ![Schedule secret deletion dialog.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-183.png)

![Screenshot 2025-05-02 004340](https://github.com/user-attachments/assets/be17047a-c233-4336-9e54-c1768f7abba8)

-   The secret should now be scheduled for deletion.

![Screenshot 2025-05-02 004351](https://github.com/user-attachments/assets/b25e81b5-9875-472f-b8ec-62b2dd85c041)



## SNS

**Topic**

-   Head to the `SNS` console.
    
-   Select **Topics** in the left navigation pane.
    
-   Select the checkbox next to `SecurityAlarms` topic.
    
-   Select **Delete**.
    

![Delete SNS topic action.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-190.png)

Delete SNS topic action.

  ![Screenshot 2025-05-02 004452](https://github.com/user-attachments/assets/02422e7d-cb60-4f9f-8d1a-42f3bf47aad2)

-   In the confirmation dialog box, type `delete me` to confirm deletion.
    
-   Select **Delete**.
    
-   The SNS topic should now be deleted.
    
![Screenshot 2025-05-02 004459](https://github.com/user-attachments/assets/b9e2951d-36a2-4b01-a5c8-68b123e8329e)
  
  

**Subscription**

-   Select **Subscriptions** in the left navigation pane.
    
-   Select the checkbox next to the subscription you created.
    
-   Select **Delete**.
    

![Delete SNS subscription action.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-192.png)

Delete SNS subscription action.

  

-   Select **Delete** to confirm the deletion.
    

![Confirm delete SNS subscription dialog.](https://learn.nextwork.org/projects/static/aws-security-monitoring/screenshot-193.png)

Confirm delete SNS subscription dialog.

  

-   The SNS subscription should now be deleted.
    

> ⬆️ Don't forget to jump back up to the top of these tabs until you've deleted everything!



----
🎉 Mission Accomplished

### 

Get your documentation!

Nice work! 🛡️ You've successfully set up an AWS security monitoring system to track and alert on secret access!

![](https://learn.nextwork.org/projects/static/aws-security-monitoring/architecture-complete.png)

  

**You've learned how to:**

-   🔑 Securely store and manage secrets using **AWS Secrets Manager**.
    
-   📜 Monitor secret access by enabling **AWS CloudTrail** logging.
    
-   🔎 Investigate security events in **CloudTrail Event History** and **S3 logs**.
    
-   📈 Create **CloudWatch Metric Filters** to track secret access events.
    
-   🔔 Set up **CloudWatch Alarms** and **SNS notifications** for real-time security alerts.

--------
content owner : **Nextwork**
------


