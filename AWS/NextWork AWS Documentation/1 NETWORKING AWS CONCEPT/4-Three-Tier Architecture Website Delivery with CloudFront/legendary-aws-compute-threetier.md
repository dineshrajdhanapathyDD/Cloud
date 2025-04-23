<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Three-Tier Web App

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-threetier)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---




# Build a Three-Tier Web App

Build a scalable web app with S3, CloudFront, Lambda, API Gateway, and DynamoDB.


## 30 second Summary

Welcome to this project on three-tier architecture! 🎉

**Three-tier** architecture is a way to organize web applications. It divides an app into three tiers to make your application easier to manage and scale.

Think of it like a layer cake: the top layer (the presentation tier) is what the user sees and interacts with, the middle layer (the logic tier) is the brains of your app that processes data, and the bottom layer (the data tier) stores data in a database.

This is not required, but we recommend learning about each tier separately before starting this project:

1.  **Presentation** Tier: [Website Delivery with CloudFront](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/1-Website%20Delivery%20with%20CloudFront)
    
2.  **Logic** Tier: [APIs with Lambda + API Gateway](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/2-APIs%20with%20Lambda%20%2B%20API%20Gateway)
    
3.  **Data** Tier: [Fetch Data with AWS Lambda](https://github.com/dineshrajdhanapathyDD/Cloud/tree/main/AWS/NextWork%20AWS%20Documentation/1%20NETWORKING%20AWS%20CONCEPT/3-Fetch%20Data%20with%20AWS%20Lambda)


### In this project, get ready to...


![](https://learn.nextwork.org/projects/static/aws-compute-threetier/architecture-complete.png)

🪣 Create a storage bucket for your website's files with **S3.**
🌎 Distribute your content globally with **CloudFront.**
⚙️ Build the brains of your application using serverless functions with **Lambda.**
🚪 Create an API to handle user requests with **API Gateway.**
💾 Store and retrieve user data with **DynamoDB.**
🔗 Connect all these services together seamlessly for your **three-tier architecture.**

![Screenshot 2025-04-23 161406](https://github.com/user-attachments/assets/126d82b5-fb8e-40d3-bd57-2241a6a92f42)

-----

## 🌐 Step #1

### Set Up the Presentation Tier

  
We'll start with the top layer, the presentation tier, which is responsible for displaying the website to our users.

 

**In this step, you're going to:**

-   Create an S3 bucket to store your website's files.
    
-   Upload a simple `index.html` file to your bucket.
    
-   Set up CloudFront to deliver your website's content globally.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/architecture-1.0.png)

  



**Create an S3 Bucket**

First, we need a place to store our website's files. This is where S3 comes in! S3 (Simple Storage Service) is like a massive, scalable hard drive in the cloud.

-   Log in to the AWS Management Console [as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    
-   Make sure you're in the AWS region closest to you.
    
-   Head to the `S3` console.
    
-   Click **Create bucket**.
    
-   Enter a unique **Bucket name,** like `nextwork-three-tier-[your-name]-[random-numbers]`.
    

> **💡 Why a unique bucket name?**  
> S3 bucket names must be globally unique because they form part of the website address if you enable static website hosting. If two buckets had the same name, there would be a conflict when trying to access the websites they host.

-   Make sure you've replaced `[your-name]` and `[random-numbers]` with your actual name and a random string of characters.
    
-   Leave all other settings as default.
    
-   Select **Create bucket.**
    
-   Click into your created bucket.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_1.png)

  

  ![Screenshot 2025-04-10 182213](https://github.com/user-attachments/assets/b6725d03-a31e-4d11-b7ce-8d11973439db)
  
![Screenshot 2025-04-10 182241](https://github.com/user-attachments/assets/5b725609-3273-4b2e-9ced-34aae347f7e5)

**Upload Website Files**

Now that we have our storage bucket set up, let's fill it with the actual content of our website.

-   Download the following website files (right click on each link, and select **Save link as...**): [index.html](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Website%20Delivery%20with%20CloudFront/index.html)[style.css](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Website%20Delivery%20with%20CloudFront/style.css)[script.js](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Website%20Delivery%20with%20CloudFront/script.js)
    

> **💡 What is index.html?**  
> index.html is the main file for a website. It's where you organise the text, pictures, and everything that makes up your webpage.
> 
>   
> **💡 What is style.css?**  
> style.css is where you write down the visual appearance of your website's HTML elements. It controls everything from font sizes and colors to layout designs, helping you keep a consistent style across your website.
> 
>   
> **💡 What is script.js?**  
> script.js is a JavaScript file that adds interaction to your website. It's where you would write the instructions for making things on your website move or change when you click a button or submit a form.

-   Head to the **Downloads** folder in your local computer. Let's see if you can find the files you've downloaded.
    
-   Open **index.html** in your browser.
    

> 🙋‍♀️ **How can I open index.html in my browser?**
> 
> 1.  Right click on index.html.
>     
> 2.  Select **Open With** > select your preferred browser.
>     

-   Do you see a simple web page?
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_2.png)

  

-   Nice work. If you see a web page, you're on your way to setting up your website's presentation!
    

> **💡 Am I setting up a static website?**  
> Not quite! Whether a site is **static** website or a **web app** depends on where the code is run:
> 
> -   **Static websites** don't need to communicate with any backend cloud resources, like databases, so code or logic is run on the client side i.e. the browser.
>     
> -   **Web apps**, on the other hand, execute code on the server side. For example, apps that use databases, APIs or Lambda functions in the backend.  
>     We'd be setting up a static website if we hosted this website right away without setting up our logic or data tiers. Since we're building a three-tier architecture today, there's going to be come code running on the server side (i.e. our Lambda function)!
>     

  
  

**Upload Your Website Files**

-   Head back to the S3 console.
    
-   Select **Upload**.
    
-   Select **Add files.**
    
   -   Select the three website files in your **Downloads** folder.
    
-   Select **Upload.**

 ![Screenshot 2025-04-10 194409](https://github.com/user-attachments/assets/7a929915-f130-47df-8048-d5fb500adfaf)   

-   Upload success!
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_3.png)

  
![Screenshot 2025-04-10 182351](https://github.com/user-attachments/assets/4b2d944d-eec2-4810-9750-81a19098f958)

**Create a CloudFront Distribution**

Now that our website files are uploaded, it's time to introduce **Amazon CloudFront**, our secret weapon for delivering it all over the world.

![Screenshot 2025-04-10 182446](https://github.com/user-attachments/assets/507e8241-a33d-45a4-b237-ad2e9eb47515)


-   Head to the `CloudFront` console.
    
![Screenshot 2025-04-10 182439](https://github.com/user-attachments/assets/05915045-a843-4602-b423-748ccfacb87e)


> **💡 What is Amazon CloudFront?**  
> Amazon CloudFront is a **Content Delivery Network (CDN),** which means it speeds up the distribution of your static and dynamic web content, such as .html, .css, .js, and image files.
> 
>   
> **💡 How does CloudFront speed up distributions?**  
> By using **caching!**
> 
> Caching is the process of storing copies of files in a **cache**, i.e. a temporary storage location, so that they can be accessed more quickly.
> 
> CloudFront has servers in many locations around the world. When a user requests content from your website, CloudFront checks if it has a copy of the content in a server near the user. If it does, it delivers the content from that server.
> 
> This is much faster than delivering the content from your origin server, which might be located in a different part of the world.

-   Select **Create a CloudFront distribution**.

![Screenshot 2025-04-10 182503](https://github.com/user-attachments/assets/c394ca38-da37-4328-a8a6-656297131c60)
    

> **💡 What is a CloudFront distribution?**  
> A CloudFront **distribution** is a set of instructions that tells CloudFront how to deliver your content.
> 
> It specifies where your website's files are stored (called the **origin**), how they should be cached, and other delivery settings like security standards.

-   Under **Origin domain,** select your S3 bucket from the dropdown list. Your S3 bucket's name should start with `nextwork-three-tier`
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_5.png)

  

-   For the origin's **Name**, enter `nextwork-three-tier S3 bucket`
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_6.png)

  

-   For **Origin accesss,** change the setting from **Public** to **Origin access control settings (recommended).**
    

![Screenshot 2025-04-10 182808](https://github.com/user-attachments/assets/775f7b8c-d720-4e0b-9d08-1367ac4b13a3)

> **💡 What is Origin Access Control (OAC)?**  
> An **origin access control (OAC)** is a special user for CloudFront. An OAC lets you keep your S3 bucket and objects private, while still making sure they can be accessed through CloudFront.
> 
> This adds an extra layer of security to your website. If we kept the **Origin access** to **Public**, it means you'd have to make your entire S3 bucket and the objects inside public for CloudFront to access it. This can be a security risk if sensitive data becomes accessible.

-   Under the new **Origin access control** heading, select **Create new OAC**.
    
-   Keep the default settings for your OAC.
    
![Screenshot 2025-04-10 182843](https://github.com/user-attachments/assets/ca2676f7-945a-4e8d-899e-6e9295b4c2d9)

> **💡 Extra for PROs: I spot a 'signing behavior' setting on the settings page... what does it mean?**  
>   
> 
> **Signing behavior** deals with whether requests to the origin need to be signed (an authentication method). This is great for private content that needs authenticated access.
> 
> Before forwarding a request to the origin i.e. the S3 bucket storing the website files, CloudFront signs the request. This adds a digital signature that the S3 bucket will check for on every incoming request. If the signature is valid, it grants access to the requested object.

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_23.png)

  

-   Select **Create.**
    
-   A popup appears under the **Origin access control** you've just created.

![Screenshot 2025-04-10 183001](https://github.com/user-attachments/assets/e6e4c12c-4e13-41e7-89e3-ef9784ca46ef)    

> **💡 What does the popup say?**  
> The popup tells you that just creating an OAC isn't enough to give CloudFront access to your S3 bucket's objects.
> 
> You also need to change your S3 bucket settings later! We'll finish creating the distribution first, and come back to it later in this step.

-   Under **Web Application Firewall (WAF)** panel, select **Do not enable security protections.**
    

> 💡 **What is Web Application Firewall (WAF)?**  
> AWS WAF is a **web application firewall**. A WAF protects your website from common threats. For example, a WAF could block traffic from IP addresses that are known for malicious behaviour.

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_16.png)

![Screenshot 2025-04-10 183116](https://github.com/user-attachments/assets/b0773fdf-0590-4c1f-9d3f-5bd943f61c3d)  

-   Under the **Settings** panel, for **Default root object,** enter `index.html`.
    

> 💡 **What is the default root object?**  
> The **default root object** is the file that CloudFront should serve when someone visits the root URL of your website.

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_14.png)

  
![Screenshot 2025-04-10 183234](https://github.com/user-attachments/assets/c2f7aeeb-1bba-4656-98ff-e24b190c0d61)

-   Leave all other settings as default.
    
-   Select **Create distribution.**
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_17.png)

![Screenshot 2025-04-10 183255](https://github.com/user-attachments/assets/1d8759a7-58fc-43a1-a1cc-6d4c320d1081)  

Phew! You've just set up a CloudFront distribution from scratch - nice work.

  
  

**Update your S3 bucket's settings**

Before we can wrap up this presentation tier, we're going to make sure we've updated the policy in our S3 bucket!

> 💡 **Recap:** The origin access control (OAC) you created makes sure **only CloudFront** can access the files stored in the S3 bucket.
> 
> But, your S3 bucket by default keeps your objects private to everyone (including the OAC).
> 
> You still need to update your S3 bucket to give the OAC permissions to your bucket's contents. Otherwise, CloudFront doesn't have access to your website files!

-   Select **Copy policy** on the banner that warns you about updating S3.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_16.png)

  

-   Next, select the shortcut in the banner. It lets you go straight to your S3 bucket's **Permissions** tab.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_15.png)


![Screenshot 2025-04-10 183450](https://github.com/user-attachments/assets/10635163-76d6-446d-a6ae-154fa2035dac)
  

-   Made it!
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_26.png)

  ![Screenshot 2025-04-10 183553](https://github.com/user-attachments/assets/a53bb2b2-715e-4577-9973-54657704b263)

-   In your S3 bucket's **Permissions** page, scroll to the **Bucket policy** section.
    
-   Select **Edit**.
    
-   Paste the policy that you copied into the policy editor.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_28.png)

  
![Screenshot 2025-04-10 183634](https://github.com/user-attachments/assets/a1424e0e-0e63-465c-8bc6-5ba88292fd88)

-   Select **Save changes.**
    

  ![Screenshot 2025-04-10 183727](https://github.com/user-attachments/assets/d73fbffe-f39d-478d-8b0c-c1461120acf9)
  

**Verify Your CloudFront Distribution**

Now, let's check if our website is live!

-   Head back into your CloudFront console.
    
-   Copy the distribution domain name. This is the URL that CloudFront will use to serve your website.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_18.png)

  

-   Paste the domain name into your web browser.
    

![](https://learn.nextwork.org/projects/static/aws-networks-cloudfront/processed_image_29.png)

  
![Screenshot 2025-04-10 183749](https://github.com/user-attachments/assets/1b001849-5757-4870-96c2-f974cc001484)

Yay! Congrats on distributing your website over CloudFront. This ticks off the presentation tier, which is all about the interface that your users and see and interact with.

------

## ⚙️ Step #2

Set Up the Logic Tier

Now that we have our presentation tier set up, let's move on to the **logic tier.**

This is where the magic happens! The logic tier is responsible for handling the brains of the application, such as fetching data from a database and performing calculations.

In this project, our logic will be a simple **Lambda function** that retrieves user data from a DynamoDB table. We need a way to expose that functionality to the outside world, so we'll use **API Gateway** to handle requests and route them to the right place.

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/architecture-2.0.png)
  

**In this step, you're going to:**

-   Create a Lambda function to fetch data from a DynamoDB table.
    
-   Write the code for your Lambda function.
    
-   Create an API Gateway REST API.
    
-   Create a resource and method to handle GET requests.
    
-   Deploy the API to make it accessible.
    
![](https://learn.nextwork.org/projects/static/aws-compute-api/architecture-complete.png)

**Create a Lambda Function**

Let's create a Lambda function. This function will fetch data from a database and return it to the user. This is a very common use case in web apps.

![](https://learn.nextwork.org/projects/static/aws-compute-api/architecture-1.0.png)

-   Head to the Lambda console.
    

> **💡 What is AWS Lambda?**  
> **AWS Lambda** is a service that lets you run code without needing to manage any computers/servers - Lambda will manage them for you.
> 
> Lambda runs your code only when you need it to (so you're not paying for any idle time).
> 
> It also scales automatically, from a few requests per day to thousands per second. All you need to do is supply your code in one of the languages that Lambda supports.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_1.png)


![Screenshot 2025-04-10 184606](https://github.com/user-attachments/assets/4f5a9e65-53a3-43b2-b488-3e24813742d7)


-   Click **Create function**.
    
-   Select **Author from scratch**.
    
-   For **Function name**, enter RetrieveUserData.
    
-   For **Runtime**, select a runtime using **Node.js**.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_5.png)    

> **💡 What does runtime mean?**  
> The **runtime** is like the environment where your code lives and runs.
> 
> While you write code in a programming language, the runtime provides the actual environment where that code runs. For example, Python code needs a Python runtime environment.

-   For **Architecture**, select **x86_64**.

![Screenshot 2025-04-10 184641](https://github.com/user-attachments/assets/0d08d64c-eafa-4fad-b7ba-fc1d6388400c)
    
-   Select **Create function**.
    
-   Success!
    
 ![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_3.png)

![Screenshot 2025-04-10 184714](https://github.com/user-attachments/assets/40c0bce4-ae68-4a53-ad2b-f80ef0de7a90)

> **💡 How do Lambda functions work?**  
> Lambda functions are triggered by events, such as an HTTP request or a change in an S3 bucket. When triggered, the Lambda service executes your code in the runtime environment you've picked.
> 
> You don't have to worry about managing servers or scaling your application; Lambda takes care of all of that for you (that's why it's called a serverless service).

  

**Write Lambda Function Code**

-   Scroll down to the **Code source** panel.
    
-   Copy and paste the following code into the code editor, replacing YOUR_REGION with your actual AWS region (e.g., 'us-west-2'):
    

```
// Import individual components from the DynamoDB client package
import { DynamoDBClient } from "@aws-sdk/client-dynamodb";
import { DynamoDBDocumentClient, GetCommand } from "@aws-sdk/lib-dynamodb";

const ddbClient = new DynamoDBClient({ region: 'YOUR_REGION' });
const ddb = DynamoDBDocumentClient.from(ddbClient);

async function handler(event) {
    const userId = event.queryStringParameters.userId;
    const params = {
        TableName: 'UserData',
        Key: { userId }
    };

    try {
        const command = new GetCommand(params);
        const { Item } = await ddb.send(command);
        if (Item) {
            return {
                statusCode: 200,
                body: JSON.stringify(Item),
                headers: {'Content-Type': 'application/json'}
            };
        } else {
            return {
                statusCode: 404,
                body: JSON.stringify({ message: "No user data found" }),
                headers: {'Content-Type': 'application/json'}
            };
        }
    } catch (err) {
        console.error("Unable to retrieve data:", err);
        return {
            statusCode: 500,
            body: JSON.stringify({ message: "Failed to retrieve user data" }),
            headers: {'Content-Type': 'application/json'}
        };
    }
}

export { handler };

```



> **💡 What does this code do?**  
> This code sets up a Lambda function that retrieves data from a DynamoDB table.
> 
> It looks for specific user data based on a userId and returns that data. If there's an error e.g. the userId doesn't exist in the database, it returns an error message.
> 
>   
> **💡 How do Lambda functions interact with other AWS services?**  
> Lambda functions can interact with other AWS services using the **AWS SDK.** The SDK gives you a set of libraries and tools for accessing various AWS services, such as DynamoDB, S3, and API Gateway.
> 
> In our case, we're using the DynamoDB functions within SDK to fetch data from our database.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_7.png)

-   Check: Make sure you've updated the placeholder region YOUR_REGION to your own region code.
    
![Screenshot 2025-04-10 185145](https://github.com/user-attachments/assets/1d4e7055-0625-49c2-bae4-a99dbf138eff)
  

**Deploy the function**

-   Select **Deploy**. This saves your code and makes the function ready to use.
    
-   Check for the Deployment successful in the bottom right corner of the console.
    
![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_8.png)
  
![Screenshot 2025-04-10 185248](https://github.com/user-attachments/assets/c2110a8a-f258-496d-9af2-7dd7503b68b6)

**Set up API Gateway**

![](https://learn.nextwork.org/projects/static/aws-compute-api/architecture-2.0.png)

Now that we have our Lambda function ready, we need a way to access it. This is where API Gateway comes in.

![Screenshot 2025-04-10 185341](https://github.com/user-attachments/assets/ab05ada9-16cb-4063-81a1-965d618ff428)

> **💡 What is an API?**  
> An **API**, or Application Programming Interface, is a way for different software systems to talk to each other. It's like a messenger that carries requests and responses between systems.
> 
> In this project, we're creating an API that carries requests from your user's browser to your Lambda function.

-   In the AWS Management Console, head to the API Gateway console.
    
![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_9.png)

![Screenshot 2025-04-10 185352](https://github.com/user-attachments/assets/b19d5039-eef7-479f-8a2b-dfa72d5b940a)

> **💡 What is Amazon API Gateway?**  
> Amazon API Gateway is an AWS service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale.
> 
> It manages incoming traffic, directing them to the correct services, and makes sure only authorized requests get through.
> 
>   
> **💡 What is the relationship between APIs and Lambda?**  
> **API Gateway** acts as the "front door" to our Lambda function. It receives requests and then forwards them to Lambda functions for processing.
> 
> **Lambda** processes the request, then sends the response through the API Gateway back to the user.

  

**Create a new API**

-   Scroll down the list of available API types.
    

> **💡 What are the different API types?**  
> API Gateway supports different types of APIs, like REST, HTTP, and WebSocket. Each type is suited for different use cases, whether it’s maintaining a standard web API (REST), providing real-time capabilities (WebSocket), or routing requests (HTTP).

-   Find **REST API**.

![Screenshot 2025-04-10 185436](https://github.com/user-attachments/assets/03766b06-93bf-4ed3-b14c-6a9d15489576)
    

> 💡 **What is a REST API?**  
> A **REST API** (Representational State Transfer) is type of API that uses HTTP methods to interact with resources (more on HTTP methods later in this step).
> 
> REST is popular because it's simple and can be used with virtually any programming language. We're using a REST API today to set up an API that connects the user with your Lambda function.

-   Select **Build**.
    

  

**Configure the API**

-   Under API details, select **New API.**
    
![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_11.png)

-   For **API name**, enter `UserRequestAPI`.
    
-   For **API endpoint type**, select **Regional**.
    
    ![Screenshot 2025-04-10 185452](https://github.com/user-attachments/assets/8360f807-76ea-476d-ad6e-aa474bbea382)

> **💡 What are endpoint types?**  
> **Endpoint types** define the scope of your API's availability. **Regional** endpoints are accessible within a specific AWS region, which is great for localized applications because it has low latency for clients in that region.
> 
>   
> **💡 What are the other endpoint types?**  
> Besides Regional, there are Edge-Optimized (for global applications) and Private (for internal networks) endpoints.
> 
> Each serves different needs depending on how and where you want your API accessed.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_12.png)

![Screenshot 2025-04-10 185532](https://github.com/user-attachments/assets/9e2601d0-db21-41eb-b1bc-6dd85a7bcc97)

-   Select **Create API**.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_13.png)    

![Screenshot 2025-04-10 185551](https://github.com/user-attachments/assets/5a6f19d1-6e53-4df6-807e-5b7e3028d199)

> **💡 What's in my API's page?**  
> Your API’s page in the AWS Console shows you a dashboard view of your API, including its methods, deployments, and settings. It's the central hub for managing and monitoring your API.

Nice work setting up that API! The API will be the front door to our Lambda function, letting users access the function via HTTP requests.

Next, we'll figure out how our app can be the bridge between our users and the API. In other words, how can users send requests? That's where API resources come in!

  

**Set up an API Resource**

![](https://learn.nextwork.org/projects/static/aws-compute-api/architecture-3.0.png)

-   Under **Resources**, select **Create resource**.
    

> **💡 What are API resources?**  
> **API resources** are endpoints that handle different parts of your API's functionalities.
> 
> For example, an API for a messaging app might have separate resources for retrieving messages and for retrieving user profiles.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_14.png)


-   For **Resource name**, enter users.
    

> **💡 What are resource path and resource name?**  
> A **resource path** is the URL path that gives you access to a resource, e.g. /messages and /users would take you to different resources, so you would access different functionalities in that API.
> 
> The **resource name** is used in the API Gateway to refer to that resource, helping you manage and reference it easily in the console.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_15.png)

![Screenshot 2025-04-10 185655](https://github.com/user-attachments/assets/00609d5f-dd29-4aae-b905-5adab17b7095)
-   Select **Create resource**.

![Screenshot 2025-04-10 185713](https://github.com/user-attachments/assets/4e778c06-5227-46aa-b427-50d36f041ad9)
    
-   Select the **/users** resource.
    
![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_16.png)

Woohooo! We're getting really close now. Great work creating the API resource.

To round off our API's setup, let's create an API **method**. Methods are things you can in a resource.

  

**Set up an API Method**

![](https://learn.nextwork.org/projects/static/aws-compute-api/architecture-4.0.png)
-   In the **Methods** panel, select **Create method**.
    

-   Select **GET** from the **Method type** dropdown.
    
  ![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_17.png)

> **💡 What are methods?**  
> **API methods** are actions you can do in a resource.
> 
> They are based on standard HTTP methods, which are different commands that let you interact with data over the internet. For example:
> 
> 1.  `GET` to retrieve,
>     
> 2.  `POST` to add,
>     
> 3.  `PUT` to update, and
>     
> 4.  `DELETE` to remove data.
>     

  ![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_18.png)

**Configure the method**

-   Select **Lambda Function** for the **Integration type**.
    

> **💡 What are integration types?**  
> **Integration types** are the backend services that can fulfill an API request. This setting determines how API Gateway passes the request data to the backend and processes the response.
> 
> By selecting a **Lambda function** as the integration type, API Gateway can directly call your AWS Lambda function each time someone uses an API endpoint:
> 
> 1.  When API Gateway gets a request, it sends it directly to your Lambda function.
>     
> 2.  Your Lambda function takes care of the request, processes it, and sends the result back to API Gateway.
>     
> 3.  API Gateway passes that response on to the user.
>     
![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_19.png)
-   Switch on **Lambda proxy integration**.
    

> **💡 Extra for PROs: What is a Lambda proxy integration?**  
> **Lambda proxy integration** is a setting that simplifies the connection between API Gateway and Lambda.
> 
> Normally, when the user interacts with the website, a request (e.g. a request for data from a database) goes straight to the API Gateway. This request contains multiple parts, like headers, query parameters, path parametres and more.
> 
> The API Gateway has the massive task of breaking down the request and reformat it in a way that the Lambda function can process. Once Lambda returns a response (e.g. retrieved data from the database), API Gateway needs to map the response back into a format expected by the client.
> 
> With Lambda proxy integration, API Gateway doesn't need to reformat the user's request. Instead, it passes the entire request—headers, query parameters, path parameters, and body directly to Lambda. The Lambda function itself will have to be capable of processing the request internally.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_20.png)

![Screenshot 2025-04-10 185741](https://github.com/user-attachments/assets/2959ec17-7585-42bc-afd1-28969e3d27a4)

-   For the **Lambda function**, make sure the default region selected is where you've created your function.
   
   ![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_21.png) 

![Screenshot 2025-04-10 190006](https://github.com/user-attachments/assets/55193f87-cde1-4ef7-8626-31bdd30cc0ab)

-   Select your `RetrieveUserData` function.
    

> **Why do I select a Lambda function?**  
> The Lambda function you select will be the function that gets triggered when that API method is called.
> 
> In this case, when the GET method for the `/users` resource is called, API Gateway will pass that request to the Lambda function you set up. When the function runs, Lambda will retrieve user data in a DynamoDB table.

-   Select **Create method**.
    
-   Method created!
    
![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_22.png)

![Screenshot 2025-04-10 190039](https://github.com/user-attachments/assets/d8bd462a-98b7-4163-a1e8-b0d6a4038c5e)

Method done = API setup DONE! 😮‍💨


> **💡 Let's recap: What are resources and methods in API Gateway?**  
> **Resources** represent the different parts of your API. In our case, the `/users` resource represents the collection of users.
> 
> **Methods** define the actions that can be performed on a resource. The `GET` method is used to retrieve data.

That's great, we'll just need to deploy our API and see it in action.

  

**Deploy the API**

-   Select **Deploy API**.
  ![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_23.png)  

-   For **Stage**, select **New stage**.
    

> **💡 What does stage mean in Lambda?**  
> In API Gateway, a **stage** is a snapshot of your API at a specific point in time.
> 
> API Gateway lets you deploy different versions of your API to different stages. This way, you can easily control who accesses what version of your API and when.
> 
> Usually, developers work on new features or changes in a **development** stage of the API, test new features in the **testing** stage, then deploy in in the **production** stage.

-   For **Stage name**, enter prod.
    

> **💡 Why is the stage called prod?**  
> Prod stands for production.
> 
> Production is the live environment where your API is fully working, and there is live traffic and real users using the API too.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_24.png)
-   Select **Deploy**.
    
![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_25.png)

![Screenshot 2025-04-10 190207](https://github.com/user-attachments/assets/dbd0d2bf-6a97-4c5f-b161-ea5837115e23)

-   Deployment success!
    
![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_27.png)
> **💡 What is on the 'prod' stage's page?**  
> This page shows you settings, metrics, and logs for your API when it’s in production.

![Screenshot 2025-04-10 190218](https://github.com/user-attachments/assets/102e84ff-215a-4f4d-9399-2e8ef7cf62e4)  

**Visit your API**

-   On the same page, find your prod stage's **Invoke URL.**
    

> **💡 What is the invoke URL?**  
> The invoke URL is the URL where your API can be used.
> 
> In real world scenarios, developers use the prod stage's invoke URL into their live application's code, so users are using the live/production version of the API.

-   Copy the **Invoke URL**.
    
![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_28.png)
-   Access the URL in a new tab on your browser.
    
    ![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_29.png)

![Screenshot 2025-04-10 190322](https://github.com/user-attachments/assets/891aa88f-f026-45f8-be82-b54693da72ba)


Dang it - you'll get an error because we haven't set up our DynamoDB table yet. That's okay! We're getting to that next 😉

----------------
  
## 💾 Step #3

### Set Up the Data Tier

We've got website files distributed through CloudFront, and a Lambda function that's ready to retrieve data.

Now, let's put our API to use. The **data tier** is where you store all the data that your application uses.

We'll use DynamoDB to store some user data.

![Screenshot 2025-04-10 190435](https://github.com/user-attachments/assets/65c633af-0fbb-4a15-a5c7-01041ffde7cd)

  

**In this step, you're going to:**

-   Create a DynamoDB table.
    
-   Add user data into your table.

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/architecture-3.0.png)    

**Create a DynamoDB Table**

DynamoDB is our NoSQL database. It's fast, flexible, and perfect for storing user data.

-   Head to the `DynamoDB` console.

![Screenshot 2025-04-10 190508](https://github.com/user-attachments/assets/04d8c869-a1cf-4506-a702-0f50c2dcb6db)
    

> **💡 What is DynamoDB?**  
> DynamoDB is one of AWS's database services. It stands out as a fast and flexible way to store data, which makes it a great choice for apps that need quick access to large volumes of data e.g. games.
> 
> If you enjoy using DynamoDB in this project, make sure to check out the [Load Data into DynamoDB](https://link.nextwork.org/projects/aws-databases-dynamodb?utm_source=project-app) project! - Make sure you're still in the same region as your Lambda function and S3 bucket.

-   Select **Create table**.
    
-   For **Table name**, enter `UserData`.
  ![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_38.png)  

-   For **Partition key**, enter `userId`.
    

> **💡 What is a partition key?**  
> A partition key is the heart of how DynamoDB organizes data. Think of it as a label that you can use to group similar items. Under the hood, the partition key is how DynamoDB spreads out your data across different servers for quick access and efficient querying.
> 
> Every item in your table _must_ have a unique partition key.
> 
![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_37.png)
-   Select **String** as the data type for the partition key.
    
-   Leave the default settings for the rest of the options.

![Screenshot 2025-04-10 190605](https://github.com/user-attachments/assets/a37dbbcc-a425-41ab-9f9b-383efe4fd629)
    
-   Select **Create table**.
    
![DynamoDB create table button.](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_1.png)
  

**Add a table item**

Now that we have our DynamoDB table set up, let's add some sample data so we can see our Lambda function in action later.

-   We'll wait until the table status changes to **Active**. While we wait...
    

-   Once the table status changes to **Active**, select your `UserData` table.
   
   ![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_1.png) 

![Screenshot 2025-04-10 190658](https://github.com/user-attachments/assets/c62e43bc-308f-4d51-93d9-73749a3bbb7a)

-   Select **Explore table items**.
    
![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_2.png)

![Screenshot 2025-04-10 190829](https://github.com/user-attachments/assets/762d97ce-d49d-494e-84e2-6d9275b1c0f5)

-   At the **Items returned** panel, select **Create item**.
    
![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_3.png)

![Screenshot 2025-04-10 190926](https://github.com/user-attachments/assets/77ebfc0a-578d-4393-b68e-b209a8cc8c5a)

-   Select **Switch to JSON view**.
    
![Screenshot 2025-04-10 190951](https://github.com/user-attachments/assets/7b7d50b3-a1fb-4b02-ad9c-2ee42f8f126c)

> **💡 Why is there a JSON view in DynamoDB?**  
> Under the hood, DynamoDB stores your data in JSON! By switching to JSON view, you can edit your data in a code format instead of filling out a form.
> 
> This is also a great way to save time - if you have data with lots of attributes, you wouldn't want to fill each of them out one by one for every item.

-   Switch off **View DynamoDB JSON**.
    
![Screenshot 2025-04-10 191005](https://github.com/user-attachments/assets/019a9365-91f8-49b5-8066-fd0cca911203)

> **💡 What is DynamoDB JSON?**  
> DynamoDB JSON is bit more specific than regular JSON. On top of storing the data's value, it also tells your database each data's **type** (e.g. a string or a number).
> 
> We won't be writing in DynamoDB JSON to stick with the simpler JSON format, so we can turn this off.

-   Paste the following JSON into the editor:
    

```
{
  "userId": "1",
  "name": "Test User",
  "email": "test@example.com"
}

```

![Screenshot 2025-04-10 191108](https://github.com/user-attachments/assets/a21543ab-985e-45e7-a677-95ed9a0e740e)


> **💡 What does this JSON code say?**  
> This JSON code defines a new item for our `UserData` table.
> 
> This item represents a user with...
> 
> -   A `userId` of **1**
>     
> -   A `name` of **Test User**, and
>     
> -   An `email` of **test@example.com**
>     
> 
>   
> Notice how we didn't have to add **name** or **email** as new attributes beforehand!
> 
> DynamoDB is **schemaless**, meaning you can add attributes as you need, and every item in your database can have a different set of attributes. This flexibility is one of the key benefits of using a NoSQL database like DynamoDB.

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_39.png)

![Screenshot 2025-04-10 191118](https://github.com/user-attachments/assets/d6148b34-894d-4d1b-a86f-9bf686808fdc)

-   Select **Create item**.
    
-   Verify that the item was created successfully. You should see it listed in the **Items returned** tab.
    
![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_40.png)
Phew! That's a piece of data in our DyanmoDB table now.

With the data tier ticked off, we're officially ready to merge the three layers!

![Screenshot 2025-04-10 191147](https://github.com/user-attachments/assets/8ff4f934-fec8-409d-b114-b82e4b497a4d)

Well, almost.

Don't forget to open up the gates between Lambda and DynamoDB - we still need to give Lambda the permission to read the items in your database table.

  

**Grant DynamoDB access to Lambda**

-   Head back to your `Lambda` console.

![Screenshot 2025-04-10 191224](https://github.com/user-attachments/assets/953c581f-d59c-412d-85df-4d7468d711f3)
    
-   Switch to the **Configuration** tab in your Lambda function.
    
![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_18.png)

![Screenshot 2025-04-10 191248](https://github.com/user-attachments/assets/534eaccc-874e-4c0b-94f7-592a580590d5)

-   Select **Permissions**.
    

> **💡 What is in the Permissions tab?**  
> The Permissions tab shows the execution role linked with your Lambda function and the permissions given to that role. It's where you control what your function is allowed to access.

-   Select the execution role name (it will look something like `RetrieveUserData-role-xxxxxxxx)`.
    
![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_19.png)
-   This shortcut will take you to the IAM console, with your Lambda function readily open.
    
![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_20.png)
-   Select **Add permissions**.
    
![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_21.png)

![Screenshot 2025-04-10 191349](https://github.com/user-attachments/assets/84416066-c122-41fe-b7fd-1ff4f67804ab)

-   Select **Attach policies**.
    
![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_22.png)

![Screenshot 2025-04-10 191454](https://github.com/user-attachments/assets/d61639b7-866f-43e2-b56e-a66ae1c0a36e)

-   Type `DynamoDB` in the search bar.
    
-   Select **AmazonDynamoDBReadOnlyAccess** as the permission policy we'll use.
    

> **💡 Extra for PROs: What about "AmazonDynamoDBFullAccess"?**  
> AmazonDynamoDBFullAccess lets you do everything with DynamoDB, like creating, deleting, and managing tables. It also lets you read and write data.
> 
> But, if your Lambda function only needs to read data, you don't need this level of access. Granting this permission when you don't need it can make your resources less secure. For example, if someone gets unauthorized access to your function, they could manipulate or delete crucial data by editing your function, which could disrupt your service or lead to data loss.
> 
![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_23.png)

![Screenshot 2025-04-10 191536](https://github.com/user-attachments/assets/b11acc38-f0a3-4cbd-b542-25acacb2ac28)

-   Select **Add permissions**.
    

  ![Screenshot 2025-04-10 191552](https://github.com/user-attachments/assets/3291f981-feec-4425-9f9e-b12267c719f7)

Yay! Permissions added. This means your Lambda function should be able to read DynamoDB table items.

With the data tier officially ticked off, _now_ we're officially ready to merge the three layers!

-----

🔄 Step #4

### Integrate the Tiers

  

We've built all three tiers of our application!

Now, it's time to connect them. We'll update our `index.html` file to make a request to our API Gateway endpoint and display the returned data.

  
  

**In this step, you're going to:**

-   Update your `script.js` file with JavaScript code to make an API request.
    
-   Verify that the data is displayed on your website.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/architecture-4.0.png)

  



  
  

**Verify API Functionality**

Let's test our API:

-   Head back into your `API Gateway` console.
    
-   Copy your prod stage API's **Invoke URL**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_9.png)

![Screenshot 2025-04-10 195523](https://github.com/user-attachments/assets/7526f278-9bab-463c-88bc-dee2e68955b7)
  

-   Append `/users?userId=1` to the end of the URL you've copied.  

![Screenshot 2025-04-10 191945](https://github.com/user-attachments/assets/65fa612a-2f7e-48cc-ac22-360ac5b3fd98)
   
-   Run the edited URL in your web browser.
    
-   You can see your table's data getting returned by the API.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_6.png)

  
![Screenshot 2025-04-10 191957](https://github.com/user-attachments/assets/7f61dc95-46f0-4e44-8bad-057912be9a66)
  
  

That's the logic and data tier's integration verified ✅



**Verify the distributed website**

Now let's check our distributed website on CloudFront.

-   Find your distributed site's URL in the CloudFront console again.
    
-   Open the URL in your browser.
    
-   Try entering `1` in the userId field and selecting **Get User Data**.
    
-   Do you see data returned to you?
    

  
  

OOo not yet...

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_19.png)

  
![Screenshot 2025-04-10 192235](https://github.com/user-attachments/assets/244cd8fe-fdf4-4a32-8d59-f76f4597baca)


Let's investigate what's happened.

  
  

**Update the connection between the presentation and logic tiers**

Where do you think your website is connected to your Lambda function?

-   You can troubleshoot frontend errors using your browser's developer tools.
    
-   Open your browser's developer tools, usually by pressing **F12** on the keyboard.
    

> **💡 What are my browser's developer tools?**  
> Browser developer tools are built into most modern web browsers (e.g. Safari, Google Chrome) and gives you options to inspect the HTML, CSS, and JavaScript of a webpage.
> 
> Developer tools are also used to debug errors and see a website's performance e.g. how fast content gets loaded.

-   Select the **Console** tab.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_8.png)

  

-   Refresh your page.
    
-   Aha! There's an error... it's referencing a URL `https://[YOUR-PROD-API-URL]/users?userId=1`
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_17.png)

![Screenshot 2025-04-10 194845](https://github.com/user-attachments/assets/94568a44-c67a-4d9b-ba8c-c4a969574b5c)  

> **💡 Where is this URL?**  
> Read the entire error message - notice that it actually references where you can find this URL:
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-threetier/unprocessed_image_18.png)

![Screenshot 2025-04-10 194900](https://github.com/user-attachments/assets/79082287-1912-478e-b972-8480534f16d6)


> 
> That's right, this URL is in line 9 of our `script.js` file.

-   Open your local computer's **Downloads** folder.
    
-   Open **script.js** in a code/text editor.
    
-   Aha, there's a line that directly references `[YOUR-PROD-API-URL]`
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_12.png)

  ![Screenshot 2025-04-10 195507](https://github.com/user-attachments/assets/6254495b-81ab-4c78-bdbe-af537a3b6673)



-   Looks like we've found our missing piece. We still need to update a placeholder that's inside script.js.
    
-   Head back into your **API Gateway** console.

![Screenshot 2025-04-10 195523](https://github.com/user-attachments/assets/7526f278-9bab-463c-88bc-dee2e68955b7)

    
-   Select **Stages** from the left hand sidebar. If you can't find it, make sure you've selected **UserRequestAPI** from the console homepage.
    
-   Copy your prod stage API's **Invoke URL**.
    
-   Paste this in **script.js**, making sure you're replacing `[YOUR-PROD-API-URL]` in the script.
    
-   Save your changes.
    

  
  

**Upload the Updated script.js**

-   Head back to the `S3` console.
    
-   Select **Upload**.
    
-   Select **Add files.**
    
-   Select the updated `script.js` in your **Downloads** folder.
    
-   Select **Upload.**
    
-   Upload success!
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_7.png)

  
![Screenshot 2025-04-10 195734](https://github.com/user-attachments/assets/c4d7d367-6c94-4d55-874a-649cb50b2f86)

Niceeeeee, that's your script.js all updated. High five! 🙌

----

## 🔌Step #5

### Validate a Fully Functioning Web App

  

It's time to validate our web app one more time - can we search for items in the application now?  
  

**In this step, you're going to:**

-   Test your CloudFront site again.
    
-   Resolve an error on the browser side (yup, one last error coming through)!
    
**Create invalidation**

![Screenshot 2025-04-10 200834](https://github.com/user-attachments/assets/eeaffe6d-fb07-4b83-a87c-86ac88b16ab4)

![Screenshot 2025-04-10 200848](https://github.com/user-attachments/assets/1f910d57-36a4-4153-9799-ffc100a0696c)

![Screenshot 2025-04-10 201204](https://github.com/user-attachments/assets/a83ba3cf-bf3d-4a47-bf4d-814c8753f452)


**Verify Your CloudFront Site**

-   Access your website through the CloudFront URL again.
    
-   Can you see your data now?
    
  

Dang it, it's still a no!

-   Use the **Console** developer tool to investigte your error this time.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_1.png)

  ![Screenshot 2025-04-10 201242](https://github.com/user-attachments/assets/22888b7f-273f-48d4-a87c-0cb05bca21f1)

> **💡 What is the error this time?**
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-threetier/unprocessed_image_2.png)

![Screenshot 2025-04-10 201728](https://github.com/user-attachments/assets/2455de03-12f4-46d1-8966-3ff5486022a6)

> The **CORS (Cross-Origin Resource Sharing)** error you're encountering happens because your API Gateway is not configured to allow requests from your CloudFront URL.
> 
> API Gateway is only allowing requests directly from its **Invoke URL**!
> 
> To resolve this, you'll need to enable CORS on your API Gateway so that it can accept requests from the domain where your frontend is hosted.
> 
>   
> **💡 What is CORS?**  
> **CORS (Cross-Origin Resource Sharing)** is like a security bouncer for your browser. It decides whether your frontend (like your CloudFront-hosted site) is allowed to talk to a backend server (like API Gateway).
> 
> By default, browsers are super cautious—they don’t let one website access resources from another domain (e.g. your frontend trying to call your API Gateway) unless the backend explicitly says it's okay.
> 
> In this case, because CORS isn’t configured in API Gateway, the browser freaks out and blocks the request from CloudFront, giving you those annoying CORS errors.
> 
> So, we need to enable CORS on your API Gateway. This is like handing the browser a VIP list that says, "Yep, the CloudFront URL is trusted—let it through."





  
  

**Configure CORS on API Gateway**

-   Head back to the **Amazon API Gateway** console in your AWS account.
    
-   Navigate to the **Resources** tab.
    
-   Select the **/users** resource.
    
-   Select **Enable CORS**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_10.png)

  ![Screenshot 2025-04-10 201935](https://github.com/user-attachments/assets/bf1300c7-98cb-445d-9b46-7cf832ee18bb)

-   In the CORS configuration, check both **GET** and **OPTIONS** under **Access-Control-Allow-Methods**.
    

> **💡 What is OPTIONS?**  
> OPTIONS is another method that browsers use to do a pre-check of your CORS settings.

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_11.png)

  

-   Enter your **CloudFront distribution domain name** as the **Access-Control-Allow-Origin** value. This will allow requests from your CloudFront domain to your API.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_3.png)

![Screenshot 2025-04-10 202134](https://github.com/user-attachments/assets/4573ef53-dcdc-40f7-a701-b3b307500bef)  

-   Select **Save**.
    

![Screenshot 2025-04-10 202205](https://github.com/user-attachments/assets/aa8df700-1b19-4ef5-9b3e-92453c2287c8)

  
  

**Deploy Your API**

After enabling CORS, you must redeploy your API for the changes to take effect:

-   Select **Deploy API.**
    
-   Choose your deployment stage i.e. **prod**.
    
![Screenshot 2025-04-10 202357](https://github.com/user-attachments/assets/5fa071e8-06e3-41c8-8a40-17b8f1b423aa)


-   Click **Deploy** to update the stage.
    
![Screenshot 2025-04-10 202408](https://github.com/user-attachments/assets/789aeb85-403c-45e8-80a0-05b6a7740a72)

  
  

**Add CORS Headers in Your Lambda Function**

> **💡 What are we doing in our Lambda function?**  
> You're using Lambda Proxy Integration for your GET method (this was st up in Step #2)!
> 
> When proxy integration is enabled, API Gateway simply forwards the request to your Lambda function and expects the Lambda to return the full HTTP response, including the CORS headers.

This means the CORS headers must be added directly in your Lambda function response, not within API Gateway.

-   Update your Lambda function code to include the **Access-Control-Allow-Origin** header in the response:
    



```javascript
// Import individual components from the DynamoDB client package
import { DynamoDBClient } from "@aws-sdk/client-dynamodb";
import { DynamoDBDocumentClient, GetCommand } from "@aws-sdk/lib-dynamodb";

const ddbClient = new DynamoDBClient({ region: 'YOUR_REGION' });
const ddb = DynamoDBDocumentClient.from(ddbClient);

async function handler(event) {
    const userId = event.queryStringParameters.userId;
    const params = {
        TableName: 'UserData',
        Key: { userId }
    };

    try {
        const command = new GetCommand(params);
        const { Item } = await ddb.send(command);

        if (Item) {
            return {
                statusCode: 200,
                headers: {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*' // Allow CORS for all origins, replace '*' with specific domain in production
                },
                body: JSON.stringify(Item)
            };
        } else {
            return {
                statusCode: 404,
                headers: {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                body: JSON.stringify({ message: "No user data found" })
            };
        }
    } catch (err) {
        console.error("Unable to retrieve data:", err);
        return {
            statusCode: 500,
            headers: {
                'Content-Type': 'application/json',
                'Access-Control-Allow-Origin': '*'
            },
            body: JSON.stringify({ message: "Failed to retrieve user data" })
        };
    }
}

export { handler };

```

-   Check: Have you updated `YOUR_REGION` to your region's code?
    
-   For security best practice, replace `*` with your CloudFront domain name. Keeping `Access-Control-Allow-Origin` means you're allowing everyone to use your API, but we should restrict access to just your CloudFront distribution.
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_4.png)

![Screenshot 2025-04-10 203322](https://github.com/user-attachments/assets/f7ac7b06-ace4-449c-8171-ad208ab27466)  

-   Select **Deploy** to deploy your updated function.
    



  
  

**The Final Test...**

-   Let's do one more refresh of our CloudFront domain name.
    
-   WOAHH, you should now see the data fetched from DynamoDB displayed on your website!
    

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/processed_image_5.png)

![Screenshot 2025-04-10 205235](https://github.com/user-attachments/assets/4e4d25ab-f590-437e-b933-560afe422bed)  

What a win!

------
## 🗑️ Before you go

### Delete your resources

  

Now that you've successfully built and tested your three-tier web application, it's time to clean up your AWS resources.

This will help us avoid incurring unnecessary costs.

  
  

**Resources to delete:**

🌎 The **CloudFront** distribution (do this first!)

🪣 The **S3** bucket.

⚙️ The **Lambda** function.

🚪 The **API**.

💾 The **DynamoDB** table.

> 💡 Make sure to delete the distribution **before** you delete the S3 bucket.
> 
> If you delete the S3 bucket first, your CloudFront distribution will point to a non-existent origin. This could cause some errors with deleting the distribution itself!

  
  

**Delete the CloudFront Distribution**

-   In the `CloudFront` console, select your distribution.
    
-   Select **Disable.**
    
-   Wait for the distribution status to change to **Disabled.**
    
-   Select **Delete.**

![Screenshot 2025-04-10 210913](https://github.com/user-attachments/assets/69b9170a-ddfb-4484-999d-21b2d53a4c6c)
    

> 🙋‍♀️ **The Delete button isn't working.**  
> If the **Delete** option isn't available, it means CloudFront is still propagating your distribution to edge locations.
> 
> Wait a few minutes, until a new timestamp appears under the **Last modified column**, then try deleting again.

  
  

**Delete the S3 Bucket**

-   In the `S3` console, select your bucket.
    
-   Select **Empty.** Confirm the deletion.

![Screenshot 2025-04-10 211029](https://github.com/user-attachments/assets/9de7382a-88eb-4d7a-9df4-541b9a43386f)

    
-   Select **Delete.** Confirm the deletion again.
    
![Screenshot 2025-04-10 211103](https://github.com/user-attachments/assets/39662ec0-c0ac-48e1-be76-d12603dbfb99)
  
  

**Delete the API**

-   Navigate to the API Gateway service in the AWS Management Console.
    
-   Select your API (`UserRequestAPI`).
    
-   Select **Actions** and select **Delete API**.
    
-   Confirm the deletion.
    

  ![Screenshot 2025-04-10 210640](https://github.com/user-attachments/assets/3ac1f407-b2c7-4eb2-8395-4459b100f594)
  

**Delete the Lambda function**

-   Navigate to the Lambda service in the AWS Management Console.
    
-   Select your function (`RetrieveUserData`).
    
-   Select **Actions** and select **Delete**.
    
-   Confirm the deletion.
    
![Screenshot 2025-04-10 205610](https://github.com/user-attachments/assets/53f673a6-be59-45de-a6d3-1caf0a6146b1)
  
  

**Delete the DynamoDB table**

-   Head to the `DynamoDB` service.
    
-   From the left hand navigation bar, select **Tables**.
    
-   Select the `UserData` table.
    
-   Select **Delete**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_48.png)

  ![Screenshot 2025-04-10 210809](https://github.com/user-attachments/assets/f60f0126-bd70-4c5b-aa29-da0b567423a6)


> **💡 What are these warnings about?**
> 
> -   **Delete all CloudWatch alarms:** Keep this **checked ✅** Deleting any CloudWatch alarms associated with this table will save you from unnecessary charges.
>     
> -   **Create an on-demand backup:** Keep this **unchecked** ❌ You can create a backup of your table to save for the long term, so you restore your data to its exact state before deleting it. Additional charges apply for on-demand backup and restore, so we won't use this option.
>     

-   Type `confirm` to confirm the deletion.
    
-   Select **Delete**.

----
## 🎉 Mission Accomplished

### That's a wrap!

  

You just built a three-tier web application on AWS. That's a huge accomplishment!

Give yourself a pat on the back (or a high five to your computer screen).

  
  

![](https://learn.nextwork.org/projects/static/aws-compute-threetier/architecture-complete.png)

  

You've just learned how to:

-   ☁️ Store website files with **S3.**
    
-   🌎 Deliver content globally with **CloudFront**.
    
-   🧠 Write serverless code with **Lambda**.
    
-   🚪 Create and manage APIs with API **Gateway**.
    
-   💾 Store and retrieve data with **DynamoDB**.
    
-   🔗 Connect all these services together to build a fully functional three-tier web application.

----


content owner : **Nextwork**

