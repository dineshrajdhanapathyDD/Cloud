<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Website Delivery with CloudFront

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-cloudfront)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

# Website Delivery with CloudFront

Learn why Content Delivery Networks (CDNs) exist with Amazon CloudFront!

Welcome to the **Deploy a Website with CloudFront**! 🚀

In today's digital world, fast and reliable websites are 👏 crucial 👏

**Slow loading times** can make your users frustrated and can even turn into lost business.

That's why Content Delivery Networks (CDNs), like **Amazon CloudFront,** are a business' secret weapon for delivering content quickly and efficiently around the world.

This project is highly relevant for roles like **Cloud Network Engineer,** **Frontend Engineer,** or **DevOps Engineer**—where it is a key responsibility to optimize website performance and ensure scalable, efficient content delivery.

### In this project, get ready to...

🪣 Create a storage space in S3 for your website's files.🌐 Set up CloudFront to distribute your website globally.🔑 Manage permissions for both S3 and CloudFront.💎 Compare different methods for hosting your website and analyze their performance.

  

### Three-Tier Architecture

This is also the FIRST project in an awesome **three-tier architecture** series.

Three-tier architecture splits applications into three essential layers: presentation, logic, and data.

In this project, you're diving into the **presentation tier,** which is all about how your application interacts with the user — it's the face of your website!

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/three-tier.png)

By focusing on the presentation layer first, you're creating a lightning-fast first impression for your users (thanks to CloudFront).

We'll talk more about this architecture in later projects - for now, let's focus on CloudFront. Make sure to follow the rest of this series to build up a fully functional three-tier solution! 🚀

-   PART TWO (Logic Tier): **APIs with Lambda + API Gateway**
    
-   PART THREE (Data Tier): **Fetch Data with AWS Lambda**
    
-   PART FOUR (putting all three layers together): **Build a Three-Tier Web App**

  ------
## 🪣 Step #1

### Set Up an S3 Bucket

  

Let's start by creating a storage space for our website's files. Amazon S3 (Simple Storage Service) is our go-to service for storing all sorts of data in the cloud. Think of it as a massive, secure, and reliable hard drive in the sky.

  
  

**In this step, you're going to:**

-   Create a new S3 bucket.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/architecture-1.0.png)

  



**Log into the AWS Management Console**

-   Log in to the AWS Management Console [as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    
-   Make sure you're in the AWS region closest to you.
    
-   Head to the `S3` console.


![Screenshot 2025-04-11 182858](https://github.com/user-attachments/assets/740df2e3-0287-44dc-8730-605543121ec4)

> **💡 What are S3 buckets?**  
> S3 buckets are like containers in the cloud where you can store your files, just like folders on your computer.
> 
> These buckets hold "objects," which are simply your files. We're creating an S3 bucket so it can hold the files that make up our website.
> 
>   
> **💡 Why are we using S3 in this project?**  
> While the star AWS service in this project is CloudFront, CloudFront is **not** a storage solution. CloudFront is a content delivery network that simply hosts content that is stored somewhere else, like Amazon S3.

  
  

**Create an S3 Bucket**

-   Select **Create bucket**.
    
-   Enter a unique **Bucket name,** like `nextwork-three-tier-[your-name]-[random-numbers]`. Replace `[your-name]` and `[random-numbers]` with your actual name and a random string of characters.
    
-   Leave all other settings as default.
    
-   Select **Create bucket.**
    
-   Click into your created bucket.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_1.png)

  ![Screenshot 2025-04-11 183701](https://github.com/user-attachments/assets/6bd475fa-7e7c-423f-a0d8-65fd0958f4e1)

Nice work! Step 1 down, you've just created the bucket that will hold your website files.

  ---
## ⬆️ Step #2

### Upload Website Files

  

Now that we have our storage bucket set up, let's fill it with the actual content of our website. Website files include HTML files, CSS stylesheets, JavaScript code, and any other assets like images or videos.

  
  

**In this step, you're going to:**

-   Upload your website files to the S3 bucket.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/architecture-2.0.png)

  



-   Download the following website files (right click on each link, and select **Save link as...**):
-  [index.html](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Website%20Delivery%20with%20CloudFront/index.html)
- [style.css](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Website%20Delivery%20with%20CloudFront/style.css)
- [script.js](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Website%20Delivery%20with%20CloudFront/script.js)

![Screenshot 2025-04-11 183805](https://github.com/user-attachments/assets/8b63c477-0d74-465d-8ecf-faa6b6db9ae6)

    

> **💡 What is index.html?**  
> index.html is the main file for a website. It's where you organise the text, pictures, and everything that makes up your webpage.
> 
>   
> **💡 What is style.css?**  
> style.css is where you write down the visual appearance of your website's HTML elements. It controls everything from font sizes and colors to layout designs, helping you keep a consistent style across your website.
> 
>   
> **💡 What is script.js?**  
> script.js refers to a JavaScript file that adds interaction to your website. It's where you would write the instructions for making things on your website move or change when you click a button or submit a form.

-   Verify what you've downloaded by heading to the **Downloads** folder in your local computer.
    
-   Open **index.html** in your browser.
    

> 🙋‍♀️ **How can I open index.html in my browser?**
> 
> 1.  Right click on index.html.
>     
> 2.  Select **Open With** > select your preferred browser.
>     

-   Do you see a simple web page?
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_2.png)

  



> **💡 Am I setting up a static website?**  
> Yup! A static website consists of a set of HTML, CSS, and JavaScript files that serve website content.
> 
> Whether a site is a static website or a web app depends on where the code is run:
> 
> -   **Static websites** don't need to communicate with any backend cloud resources, like databases, so code or logic is run on the client side i.e. the browser.
>     
> -   **Web apps**, on the other hand, execute code on the server side. For example, apps that use databases, APIs or Lambda functions in the backend.
>     

  
  

**Upload Your Website Files**

-   Head back to the S3 console.
    
-   Select **Upload**.
    
-   Select **Add files.**
    
-   Select the three website files in your **Downloads** folder.
    
-   Select **Upload.**
    
-   Upload success!
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_3.png)

  ![Screenshot 2025-04-11 183841](https://github.com/user-attachments/assets/177a14c3-747b-4cf3-bdb2-95eaaa93dd2d)

---
## 🌐 Step #3

### Set Up a CloudFront Distribution

  

Now that our website files are uploaded, it's time to introduce **Amazon CloudFront**, our secret weapon for delivering it all over the world.

  
  

**In this step, you're going to:**

-   Set up **CloudFront** to host your site.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/architecture-3.0.png)

  



**Navigate to CloudFront**

-   Head to the `CloudFront` console.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_4.png)

![Screenshot 2025-04-11 183950](https://github.com/user-attachments/assets/39fab906-49e3-4ee9-a6c6-83c914adba23)  

> **💡 What is Amazon CloudFront?**  
> Amazon CloudFront is a Content Delivery Network (CDN), which means it speeds up the distribution of your static and dynamic web content, such as .html, .css, .js, and image files.
> 
>   
> **💡 How does CloudFront speed up distributions?**  
> By using **caching!**
> 
> Caching is the process of storing copies of files in a **cache**, i.e. a temporary storage location, so that they can be accessed more quickly.
> 
> CloudFront caches your website content in multiple servers around the world. When a user requests content that you're serving with CloudFront, the request is routed to the edge location that provides the lowest latency (time delay), so content is delivered with the best possible performance.



  
  

**Create a CloudFront Distribution**

-   Select **Create a CloudFront distribution**.
    

> **💡 What is a CloudFront distribution?**  
> A CloudFront **distribution** is a set of instructions that tells CloudFront how to deliver your content.
> 
> It specifies where your website's files are stored (called the **origin**), how they should be cached, and other delivery settings like security standards.

-   Under **Origin domain,** select your S3 bucket from the dropdown list. Your S3 bucket's name should start with `nextwork-three-tier`
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_5.png)

  

-   For the origin's **Name**, enter `nextwork-three-tier S3 bucket`
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_6.png)

  ![Screenshot 2025-04-11 184413](https://github.com/user-attachments/assets/552bdb67-7242-4f33-9eb9-99e4742c418d)

> 💡 **Extra for PROs: What about origin path, what does it mean?**  
> Great question! First of all, a **path** in a URL is a specific location/page on a website. It's the part of the URL that comes after the domain name - for example, in `www.nextwork.org/projects/aws-networks-cloudfront`, the path is `/projects/aws-networks-cloudfront`, which takes you directly to this CloudFront project instead of another project on our website.
> 
> Paths help organize and structure the content on websites, making it easier for both users and systems like search engines or CDNs like CloudFront find specific information.
> 
> When you set up a CloudFront distribution, you don't have to get CloudFront to distirbute your entire website - you can cherry pick a specific file or section of your website to distribute. To do this, you'd configure your distribution with a specific **origin path.**



-   Keep **Origin accesss** as the default setting i.e. **Public**.
    

> **💡 What is Origin Access Control (OAC)?**  
> An **OAC** is a new method of authentication that lets CloudFront prove its identity when requesting content from an S3 bucket.
> 
> This adds an extra layer of security to your website. We'll come back to OAC at Step #6 in this project!
> 
> For now, we're picking the default **Public** setting. This means we're **not** using an OAC and opting to make our entire bucket public instead.

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_7.png)

![Screenshot 2025-04-11 184806](https://github.com/user-attachments/assets/8721d416-bf75-42e9-8f40-e471e25c1bd0)  

-   We'll leave the default settings for **Default cache behavior**.
    

> 💡 **Extra for PROs: What is cache behaviour?**  
> **Cache behavior** settings affects how CloudFront handles caching at edge locations, i.e. the AWS data centers around the world that cache copies of content closer to users. There are over 400 edge locations worldwide!
> 
> Cache behaviour settings include options for how long to cache resources, what to do if content isn't cached in an edge location, and more.

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_9.png)



  

-   We'll leave the default settings for **Cache key and origin requests**.
    

> 💡 **Extra for PROs: What are cache key and origin requests?**  
> Cache keys and origin requests help CloudFront provide faster access to content, so your users' browsing experience is quicker and more responsive.
> 
> A **cache key** is like a label that helps a system like CloudFront remember a specific version of a webpage or file.
> 
> When you visit a website, the URL you use might have extra bits of information like `"?sort=price"` at the end. These parameters tell the website how you want to view its content, like sorting products by price.
> 
> So, one cached version of a website might show products sorted by price, and another by popularity, each stored under a different cache key.
> 
> **Origin requests** come into play when the cache doesn't have what you're looking for, or it's outdated. These are instructions that tell CloudFront how to update content from the website's original server (the origin). CloudFront can grab the latest content or get versions it hasn't stored yet, so you see up-to-date and relevant information.

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_10.png)

![Screenshot 2025-04-11 184958](https://github.com/user-attachments/assets/7de40d03-7d2f-450d-9018-29f4d8a6f968)  

-   We'll leave the default settings for **Function associations - optional**.
    

> 💡 **Extra for PROs: What are function associations?**  
> **Function associations** in CloudFront let you connect AWS Lambda functions with CloudFront events, like automatically updating content before delivery or after it's been viewed by the end user.

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_11.png)



  

-   For **Web Application Firewall (WAF),** select **Do not enable security protections.**
    

> 💡 **What is Web Application Firewall (WAF)?**  
> AWS WAF is a **web application firewall**. A WAF protects your website from common threats. For example, a WAF could block traffic from IP addresses that are known for malicious behaviour.

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_16.png)


![Screenshot 2025-04-11 185114](https://github.com/user-attachments/assets/38af1c12-a8d0-45bf-b648-92736b5d678f)  

-   Under the **Settings** section, scroll to the **Default root object** heading.
    

> 💡 **Extra for PROs: We skipped a few settings, what were they about?**  
> In the **Settings** section, we skipped a few options that fine-tune how CloudFront handles your distribution. No stress, the default selections already give you excellent performance and security:
> 
> -   **Anycast static IP lists:** This setting lets you deliver traffic from a specific set of IP addresses. It's optional and useful if you need more control over the source of your content delivery.
>     
> -   **Price class:** This lets you choose the price class for your CloudFront distribution, which directly impacts how much you'll pay. The more regions you'd like CloudFront to cover, the more expensive (but, don't expect to pay as we're using the Free Tier of CloudFront).
>     
> -   **Alternate domain names (CNAMEs):** Here, you can add custom domain names (like www.example.com) that you want to use with your CloudFront distribution, instead of the default CloudFront domain name (like d1234.cloudfront.net).
>     
> -   **Custom SSL certificate:** An SSL certificate is a digital certificate that proces the identity of a website and enables an encrypted connection. Whenever you visit a website securely using HTTPS (instead of HTTP), an SSL certificate is protecting the connection between your browser and the server, so your interactions with the site are private and secure.
>     
> -   **Supported HTTP versions:** The HTTP version you're using affects how data is delivered between your users' browsers and the CloudFront server. Each new version aims to improve web performance and security, making your site faster and more enjoyable.  
>     Again, even if you stick with the default settings, CloudFront is designed to provide excellent performance and security, so your content is delivered efficiently and safely to users around the world.
>     

-   Enter `index.html` as your **Default root object**.
    

> 💡 **What is the default root object?**  
> The **default root object** is the file that CloudFront should serve when someone visits the root URL of your website.
> 
>   
> **💡 What is the root URL of a website?**  
> The root of a website is the main URL without any additional paths. For example, `https://www.example.com/` is the root URL.
> 
> When a user visits the root URL, the web server looks for a specific file to serve. In our case, the web server looks for index.html because it is the default root object in our CloudFront distribution.
> 
>   
> **💡 Extra for PROs: How do website links work?**  
> When you click on a website link, your browser sends a request to the web server for a specific file or resource. The server then sends back the requested file, which your browser renders and displays.
> 
> The URL structure determines which file is requested. For example, `https://www.example.com/about.html` would request the file `about.html`.

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_14.png)

  



Ready to review your distribution settings? Before you hit **create**, check that:

Your **Origin domain** is set to your S3 bucket.

Your origin's **Name** is set to `nextwork-three-tier S3 bucket`

Your **Origin accesss** is using the default setting i.e. Public.

Your **Web Application Firewall (WAF)** is set to **Do not enable security protections.**

Your **Default root object** is `index.html`

  
![Screenshot 2025-04-11 185235](https://github.com/user-attachments/assets/c1b8e890-ad6d-40e7-876f-8d0e991deef5)  

-   Select **Create distribution.**
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_17.png)

  
![Screenshot 2025-04-11 185338](https://github.com/user-attachments/assets/58861300-dd98-4f47-93fb-e657a5163b35)

You've just set up a CloudFront distribution from scratch - nice work.

-----

## ✅ Step #4

### Verify your CloudFront Distribution

  

Now that our CloudFront distribution is created, let's see if it's working!

  
  

**In this step, you're going to:**

-   View your CloudFront distributed site.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/architecture-4.0.png)

  



**Verify Your CloudFront Distribution**

-   Copy the distribution domain name. This is the URL that CloudFront will use to serve your website.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_18.png)

  

-   Paste the domain name into your web browser.
    
-   Whoops! You'll see a **Site can't be reached** error.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_42.png)

  ![Screenshot 2025-04-11 185612](https://github.com/user-attachments/assets/2ee7a411-03ae-44bc-8b3f-6f072f71a6a6)


> **💡 Why is there an error?**  
> Don't worry, this is expected! We haven't given CloudFront permission to access our S3 bucket yet.
> 
> By default, S3 buckets are private. CloudFront needs explicit permission to access the files in your bucket.


![Screenshot 2025-04-11 185622](https://github.com/user-attachments/assets/a0c17b4e-6688-4212-b831-cbeb3ffde6dd)


- Great, at least we've visited our CloudFront distribution for the first time 😎

- We'll fix this error in the next step, by updating our CloudFront distributions's settings.
-------
## 🔑 Step #5

### Update your CloudFront settings

  

Let's grant CloudFront the necessary permissions to access our S3 bucket. We'll update our S3 bucket settings too after this!

  
  

**In this step, you're going to:**

-   Update your CloudFront origin's settings.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/architecture-5.0.png)

  



**Update your CloudFront settings**

-   Head back to your **CloudFront** console.
    
-   Select **Origins** in your distribution's menu bar.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_20.png)

  

-   In the **Origins** panel, select your origin titled **nextwork-three-tier S3 bucket**.

    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_21.png)

 ![Screenshot 2025-04-11 185832](https://github.com/user-attachments/assets/893fe15e-5a9f-4939-b642-5920d5e2285c) 

-   Select **Edit**.
    
-   Find the **Origin access** setting, which should have **Public** selected.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_22.png)

  

-   Can you tell what the **Origin access** setting means for your bucket?
    
![Screenshot 2025-04-11 190102](https://github.com/user-attachments/assets/b927a5b0-1e8a-47ea-a8e7-f233e37bfbb8)


> **💡 What does it mean for Origin access to be public?**  
> If Origin access is public, it means **anyone** can access the content directly from the **origin** i.e. your S3 bucket, not just via CloudFront. This can become a security risk if sensitive data is accessible.
> 
>   
> **💡 Since origin access is public, why is access still denied in my distribution?**  
> Setting the origin access to public **doesn't** automatically update the permissions of the objects in your S3 bucket - for security, the objects are private by default. You'll still need to go to your S3 bucket and set all your objects to **public** for everyone to access them.
> 
> So, even if origin access is public, CloudFront can't access your website's content until your objects' access settings are also set to public.



-   Change the setting from **Public** to **Origin access control settings (recommended).**
    

> **💡 Why are we changing this setting to origin access control?**  
> Normally, if you want to serve files publicly, those files must be **publicly accessible** on S3. This could potentially expose your S3 content to unwanted access or security threats.
> 
> An origin access control (OAC) is a special user for CloudFront that prevents this. An OAC lets you keep your S3 bucket and objects **not** publicly accessible, while still making sure they can be accessed through CloudFront.
> 
> **OAC** also gives you granular control over how CloudFront accesses the content. For example, you can add other authentication or security settings to make sure only legitimate users can access your content.



-   Under the new **Origin access control** heading, select **Create new OAC**.
    
-   Keep the default settings for your OAC.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_23.png)

  

> **💡 Extra for PROs: What does the signing behavior setting mean?**  
> Signing behavior deals with whether requests to the origin need to be signed (an authentication method). This is great for private content that requires authenticated access.
> 
> Before forwarding a request to the origin i.e. the S3 bucket storing the website files, CloudFront signs the request. This adds a digital signature that the S3 bucket will check for on every incoming request. If the signature is valid, it grants access to the requested object.

![Screenshot 2025-04-11 190159](https://github.com/user-attachments/assets/370c8981-9045-4d7b-be52-1607c3a60935)

-   Select **Create.**
    
-   A popup appears under the **Origin access control** you've just created.
    

> **💡 What does the popup say?**  
> The popup tells you that just creating an OAC isn't enough to give CloudFront access to your S3 bucket's objects.
> 
> You also need to change your S3 bucket settings!
> 
> Recap: The OAC's role is that it makes sure **only CloudFront** can access the files stored in the S3 bucket. For this restricted access to be effective, the S3 bucket's policy still needs to explicitly grant the OAC permission to the bucket's contents.


Sweet! We're almost done. You've just created an Origin Access Control (OAC), and now we'll need to update the settings on your S3 bucket's side.

------

  
## 🪣 Step #6

### Update your S3 bucket's settings

  

**In this step, you're going to:**

-   Update your S3 bucket's permission settings.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/architecture-6.0.png)

  



-   Still in your CloudFront distribution's settings page, select **Copy policy.**
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_24.png)

  

-   Next, select the shortcut under the popup message. It lets you go straight to your S3 bucket's **Permissions** tab.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_27.png)

  

-   Made it!

![Screenshot 2025-04-11 190325](https://github.com/user-attachments/assets/55812f75-d6cb-4e6b-b627-a9ab291b6aef)

    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_26.png)

  
![Screenshot 2025-04-11 190357](https://github.com/user-attachments/assets/7aa3bb51-b46b-4c57-8514-5d4a5e382fc0)

-   In your S3 bucket's **Permissions** page, scroll to the **Bucket policy** section.
    
-   Select **Edit**.
    
-   Paste the policy that you copied into the policy editor.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_28.png)

  
![Screenshot 2025-04-11 190603](https://github.com/user-attachments/assets/654399d6-3bc4-478a-9783-a5bc053e9be1)





-   Select **Save changes.**

![Screenshot 2025-04-11 190714](https://github.com/user-attachments/assets/b85a9c75-55af-448f-ab3d-aa78049ab505)
    
-   Head back to your CloudFront distribution's settings page.
    
-   Select **Save changes.**

![Screenshot 2025-04-11 190758](https://github.com/user-attachments/assets/6eb983d9-9028-4560-9000-4ac355447495)
    
-   Revisit your distribution's URL.
    
-   Refresh your tab.
    
-   What do you see now?
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_29.png)

  ![Screenshot 2025-04-11 190824](https://github.com/user-attachments/assets/fd16e699-d66c-4172-a596-b9eeed63139f)


Yay! Congrats on distributing your website over CloudFront.

> 🙋‍♀️ **I don't see a distributed site**  
> Oh no! If you're stuck, ## comments please

-----------------------

## 💎 Secret Mission

### Showcase Advanced Skills

  

Welcome to your 🤫 exclusive 🤫 secret mission!

Your mission, should you choose to accept it, is to compare using CloudFront vs S3 to serve your website.

  
  

**💎 In this secret mission, get ready to:**

-   Enable S3 static website hosting.
    
-   Compare S3 vs CloudFront based on the hosted website's URLs, permission settings and performance.
    
-   Showcase more advanced skills, like using developer tools to inspect a live site, in your **project documentation.** Stand out from the rest!
    

> 💎 **Congratulations** - Secret Mission unlocked!

  
  



**Enable S3 Static Website Hosting**

-   In the `S3` console, head back to your bucket.

![Screenshot 2025-04-11 191020](https://github.com/user-attachments/assets/06aec1b1-0571-4083-a4b0-0d8ae83fb843)
    
-   Select the **Properties** tab.

![Screenshot 2025-04-11 191032](https://github.com/user-attachments/assets/3ba4078c-3e09-4b84-b1c1-12679ddce48a)
    
-   Scroll down to the **Static website hosting** panel.
    
-   Select **Edit.**
    
-   Select **Enable** static website hosting.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_31.png)

![Screenshot 2025-04-11 191058](https://github.com/user-attachments/assets/ea9412be-478e-443b-ac31-2deda6134c89)  

-   For **Index document,** enter `index.html`
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_32.png)

  

-   Select **Save changes.**

![Screenshot 2025-04-11 191152](https://github.com/user-attachments/assets/502dbbeb-359d-41f7-900c-bde5e73f846f)
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_33.png)

![Screenshot 2025-04-11 191138](https://github.com/user-attachments/assets/815d7616-8b3d-4bf1-80d6-d6d36de61c48)  

-   Open the **Bucket website endpoint** URL.
![Screenshot 2025-04-11 191246](https://github.com/user-attachments/assets/36775919-7666-422b-8f13-fd07b5d18ad0)    

  
  

Uh oh, a **403 Forbidden** error this time!

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_34.png)

  
![Screenshot 2025-04-11 191255](https://github.com/user-attachments/assets/a6015910-e431-44ee-8133-6f86cb5dc8fc)


-   Keep the tab with the endpoint URL open.
    
-   Back in your S3 console, select the **Permissions** tab.
    
-   Scroll to the **Block public access (bucket settings)** section and select **Edit**.
    
-   Uncheck **Block _all_ public access.** We need our website files to be publicly accessible, so we'll disable this setting.
    

> **💡 Why uncheck "Block all public access"?**  
> Since we're hosting a static website with S3 this time, we want anyone to be able to access its files. We don't have CloudFront to distribute it for us!
> 
> By unchecking this option, we're allowing public read access to the objects in our bucket.

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_35.png)

  ![Screenshot 2025-04-11 191421](https://github.com/user-attachments/assets/8c6da8ca-6df3-4a7d-a49c-fc35f090f408)

-   Select **Save changes.**
    
-   Type `confirm` in the popup box, and select **Confirm**.

![Screenshot 2025-04-11 191454](https://github.com/user-attachments/assets/f0f09e42-6fb8-4bc5-a6cf-d24fe99b06ae)
    
-   Is your website hosted with S3 now?

![Screenshot 2025-04-11 191454](https://github.com/user-attachments/assets/f0f09e42-6fb8-4bc5-a6cf-d24fe99b06ae)
    
-   Refresh the tab with the S3 static website hosting URL open.
    
-   Ooops... we're still seeing a **403 Forbidden** error.
    

> **💡 Why do I still get this error?**  
> Unchecking **Block all public access** doesn't grant permission to access the objects. It simply **stops blocking** all public access attempts.
> 
> In other words, think of it as another security guard for your bucket's front door, but disabling it doesn't mean you've opened the door yet - it only means than you've sent the guard away, and you **can** open the door to traffic now.
> 
> You still need a bucket policy to explicitly **grant** permissions. When you set up a bucket policy that allows public read access, you're telling AWS to let **anyone** on the internet to read the files in the bucket.
> 
> ![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/block-all-access.png)
> 
>   



-   Back in the **S3** console, scroll to the **Bucket policy** section.


    
-   Select **Edit**.
    
-   In the bucket policy's editing window, add the following statement:
    



```json
{
    "Sid": "PublicReadGetObject",
    "Effect": "Allow",
    "Principal": "*",
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::nextwork-three-tier-[your-name]-[random-numbers]/*"
}

```

> 🙋‍♀️ **How do I add this statement to my JSON policy?**  
> Here's a hint!
> 
> ![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/unprocessed_image_36.png)


![Screenshot 2025-04-11 191739](https://github.com/user-attachments/assets/6e47eb7c-5f4f-491a-8173-69021a3bf6d5)

>   
> 
> Pssst.. notice how the screenshot added an extra comma `,` between the two Statements.
> 
> [Ask ## comments if you're stuck!

-   Check: did you replace the placeholder bucket name i.e. `three-tier-[your-name]-[random-numbers]`?
    
-   Select **Save changes**.
    
![Screenshot 2025-04-11 191805](https://github.com/user-attachments/assets/f871fc38-ed83-44e3-a9b6-c20bc478ecb7)
  
  

-   Refresh the S3 website endpoint URL.
    
-   You should see your website served directly from S3 now!
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_38.png)

  

![Screenshot 2025-04-11 191816](https://github.com/user-attachments/assets/404b6592-51da-44d5-b998-aa3c760311c7)

  
------
## 💎 Secret Mission 2

### Compare S3 vs. CloudFront Performance Times

  

This is truly for the PROs!

Are you ready for another level up?

Let's build our skills in investigating website performance and compare our two hosted sites along the way.

Note: you will need to complete the first secret mission before starting this one.

> 💎 **Congratulations** - second Secret Mission unlocked!

  
  

-   Head to your **CloudFront** hosted site.
    
-   Open your browser's developer tools, usually by pressing **F12** on the keyboard.
    

> **💡 What are my browser's developer tools?**  
> Browser developer tools are built into most modern web browsers (e.g. Safari, Google Chrome) and gives you options to inspect the HTML, CSS, and JavaScript of a webpage.
> 
> Developer tools are also used to debug errors and see a website's performance e.g. how fast content gets loaded.

-   Select **Network** from the menu bar of developer tools.
    

> **💡 What does the Network tab do?**  
> The **Network** tab in the browser's developer tools shows all requests that your browser's made to a server to load the website.
> 
> You get a list of files loaded, data sent and received, and detailed timing of each request.

-   Refresh your tab.
    
-   Notice the load times of the items in your **CloudFront** delivered website.
    

> **💡 What does load time mean?**  
> Load times mean how quickly content on your website loads.
> 
> The faster the load time, the quicker the user accesses your website content. This is a great way to improve the user experience and can contribute to your site having better search engine rankings!

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_41.png)

  
![Screenshot 2025-04-11 192539](https://github.com/user-attachments/assets/ed7e302d-0fe4-4e3f-94ef-8d5c2da51f2f)


-   Now revisit your S3 hosted site.
    
-   Again, let's open your browser's developer tools (by pressing **F12** on the keyboard).
    
-   Select **Network** from the menu bar of developer tools.
    
-   Refresh your tab.
    
-   Notice the load times of the items in your **S3** hosted website.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_40.png)

  ![Screenshot 2025-04-11 193312](https://github.com/user-attachments/assets/c566dfa9-05d9-4113-9f4d-ffeaef2adf8c)

> **💡 What's the difference?**  
> CloudFront should generally be faster, especially for users located far from your S3 bucket's region.
> 
>   
> **💡 Why would CloudFront be faster?**  
> CloudFront's CDN caches content closer to users globally, while S3 static website hosting serves files directly from a single region.
> 
> This means data travels a much shorter distance from an edge location to the end user.


-----
  

## Before you go

### Delete your resources

  

Now that we've completed the project, let's clean up our AWS resources to avoid incurring unnecessary charges.

  
  

**Resources to delete:**

-   The CloudFront distribution.
    
-   The S3 bucket.
    

> 💡 Make sure to delete the distribution **before** you delete the S3 bucket.
> 
> If you delete the S3 bucket first, your CloudFront distribution will point to a non-existent origin. This could cause some errors with deleting the distribution itself!
> 
>   
> 🙋‍♀️ **Uh oh, I've aready deleted the bucket first**  
> No worries! You can still resolve this by switching your distribution's origin access from OAC back to **Public**.
> 
> Ask ## comments if you're stuck!

  
  

**CloudFront Distribution**

-   In the `CloudFront` console, select your distribution.
    
-   Select **Disable.**
    
-   Wait for the distribution status to change to **Disabled.**
    
-   Select **Delete.**
    

> 🙋‍♀️ **The Delete button isn't working.**  
> If the **Delete** option isn't available, it means CloudFront is still propagating your distribution to edge locations.
> 
> Wait a few minutes, until a new timestamp appears under the **Last modified column**, then try deleting again.

  
  

**S3 Bucket**

-   In the `S3` console, select your bucket.
    
-   Select **Empty.** Confirm the deletion.
    
-   Select **Delete.** Confirm the deletion again.
    



----------



🎉 Mission Accomplished

### That's a wrap!

  

**You've learned how to:**

-   🪣 Create and manage S3 buckets.
    
-   ⬆️ Upload files to S3.
    
-   🌐 Set up a CloudFront distribution for lightning-fast content delivery.
    
-   🔑 Secure your S3 bucket using Origin Access Identities.
    
-   💎 Compare S3 static website hosting with CloudFront.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/architecture-complete.png)

  

Nice one - you've just set up the first tier of a 3-tier architecture!
----

content owner : **Nextwork**

