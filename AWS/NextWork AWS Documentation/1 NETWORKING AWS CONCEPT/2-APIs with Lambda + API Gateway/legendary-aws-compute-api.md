<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# APIs with Lambda + API Gateway

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-api)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com




## APIs with Lambda + API Gateway


In this project, you'll learn to build an API without having to manage traditional servers. Say hello to AWS Lambda and Amazon API Gateway!

This project is most ideal for roles like **Backend Developer**, **Cloud Architect**, or **Systems Engineer**, where it's important to understand how to set up serverless architecture and manage APIs.

  

### In this project, get ready to...

⚙️ Develop a serverless Lambda function.
🚪 Configure an API with API Gateway.
🔌 Connect Lambda with API Gateway.
💎 Write JSON documentation for your API.

![](https://learn.nextwork.org/projects/static/aws-compute-api/architecture-complete.png)

  

### Three-Tier Architecture

This is also the SECOND project of an awesome **three-tier architecture** series.

Three-tier architecture splits applications into three essential layers: presentation, logic, and data.

In this project, you're diving into the **logic tier,** which is all about your app's backend. This is where you write and run the code that translates user actions (e.g. button clicks) to application functionality (e.g. website searches or data processing).

We'll talk more about this architecture in later projects - for now, let's focus on Lambda and API Gateway. Make sure to follow the rest of this series to build up a fully functional three-tier solution! 🚀

-   PART ONE (Presentation Tier): **Website Delivery with CloudFront**
    
-   PART THREE (Data Tier): **Fetch Data with AWS Lambda**
    
-   PART FOUR (putting all three layers together): **Build a Three-Tier Web App**


-----

## 🐑 Step #1

### Create a Lambda Function

  

In this step, we'll create a Lambda function.

The function will fetch data from a database and return it to the user. This is a very common use case in web apps.

For example, when a user searches for a product in an online shop, the website's backend needs to query the product database, find the relevant product, and send its details back to the user's browser as swiftly as possible.

  
  

**In this step, you're going to:**

-   Create a new Lambda function.
    
-   Configure its settings.
    
-   Add some code to retrieve user data.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/architecture-1.0.png)

  



  
  

**Navigate to the Lambda service**

-   Log in to the AWS Management Console [as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    
-   Make sure you're in the AWS region closest to you.
    
-   Head to the `Lambda` console.

![Screenshot 2025-04-11 193802](https://github.com/user-attachments/assets/10273a17-dfec-49e8-aa33-21a850bdbbc1)
    

> **💡 What is AWS Lambda?**  
> **AWS Lambda** is a service that lets you run code without needing to manage any computers/servers - Lambda will manage them for you.
> 
> Lambda runs your code only when you need it to (so you're not paying for any idle time).
> 
> It also scales automatically, from a few requests per day to thousands per second - all you need to do is supply your code in one of the languages that Lambda supports.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_1.png)

  

![Screenshot 2025-04-11 193851](https://github.com/user-attachments/assets/8126aeab-9e3f-4f9c-a4df-09092356bdd9)
  
  

**Create a new Lambda function**

> **💡 What is a Lambda function?**  
> A Lambda **function** is a piece of code that you run in AWS Lambda.
> 
> You write Lambda functions to do things like process data, respond to events, or run automated tasks.

-   Select **Create a function**.
    
-   Select **Author from scratch**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_2.png)

  

  
  

**Configure the Lambda function**

-   For **Function name**, enter `RetrieveUserData`.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_4.png)

  

-   For **Runtime**, select a runtime using **Node.js**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_5.png)

  

> **💡 What does runtime mean?**  
> The **runtime** is like the environment where your code lives and runs.
> 
> While you write code in a programming language, the runtime provides the actual environment where that code runs. For example, Python code needs a Python runtime environment.
> 
> Selecting the right runtime for your AWS Lambda function makes sure it has everything (i.e. dependencies) needed to run efficiently.
> 
>   
> **💡 What is Node.js?**  
> **Node.js** is a popular **JavaScript** runtime environment.
> 
> Traditionally, JavaScript is used for scripts that run right in your web browser, handling tasks like animations and form validations. This browser-based setup means all the JavaScript action happens on your device after the web page loads.
> 
> But with Node.js, you can take JavaScript to the server side. Now, you're running scripts on a server before anything even reaches the browser.
> 
> This is a big deal because it lets developers use JavaScript for both frontend and backend tasks, which makes development much more efficient. You can use Node.js to build things like server-side apps, command-line tools, or even chat with databases using JavaScript.
> 
> In our case, we're using Node.js to create the backend for a web app.

-   For **Architecture**, select **x86_64**. This selects the type of processor the function will run on. Most use cases are fine with x86_64.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_6.png)

  

> **💡 What does architecture mean?**  
> **Architecture** refers to the type of hardware (specifically, the processor) that your AWS Lambda function uses. By selecting an architecture, you're making sure that your code runs efficiently and is optimized for the specific processor it will run on.
> 
> **x86_64** is a widely-used architecture in many computers and servers.
> 
>   
> **💡 Woah, did you just say hardware? I thought Lambda is serverless**  
> Even though AWS Lambda is serverless, which means you don't have to manage any servers or worry about the infrastructure, it still runs on physical servers behind the scenes.
> 
> Even though you're not directly handling the hardware, you still need to select an architecture that AWS manages for you.


![Screenshot 2025-04-11 193947](https://github.com/user-attachments/assets/f0b690a6-3ace-4ee9-8499-0b35631b4907)

-   Select **Create function**.
    
-   Success!
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_3.png)



![Screenshot 2025-04-11 194023](https://github.com/user-attachments/assets/fc2b937b-97b6-4014-af2c-21f8d36db5c5)

  

> **💡 What's in my Lambda function's page?**  
> The Lambda function's page in the console shows you everything about your function—its code, configuration settings like memory and timeout, and metrics on how it's performing.
> 
> We'll use it to add our function's code next.

  
  

**Add the code**

-   Scroll down to the **Code source** panel.
    
-   Copy and paste the following code into the code editor, replacing `YOUR_REGION` with your actual AWS region (e.g., 'us-west-2'):
    



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

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_7.png)

  
![Screenshot 2025-04-11 194209](https://github.com/user-attachments/assets/f21e7cd6-3026-49f9-a065-5de8837018db)

> **💡 What does this code do?**  
> This code sets up a Lambda function that retrieves data from a DynamoDB table.
> 
> It looks for specific user data based on a 'userId' and returns that data. If there's an error e.g. the userId doesn't exist in the database, it returns an error message.
> 
> Note: We haven't set up the DynamoDB table or userID yet - those will come in the next project!

-   Check: Make sure you've updated the placeholder region `YOUR_REGION` to your own region code.
    



  
  

**Deploy the function**

-   Select **Deploy**. This saves your code and makes the function ready to use.
    
-   Check for the Deployment successful in the bottom right corner of the console.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_8.png)

![Screenshot 2025-04-11 194233](https://github.com/user-attachments/assets/51fc9c25-37a1-44ec-bea1-c730b03ec319)
  

Great work! You've just set up a Lambda function.

-----
## 🚪 Step #2

### Set up API Gateway

  

Now that we have our Lambda function ready, we need a way to access it. This is where API Gateway comes in.

> **💡 What is an API?**  
> An **API**, or Application Programming Interface, is a way for different software systems to talk to each other. It's like a messenger that carries requests and responses between systems.
> 
> In this project, we're creating an API that carries requests from your user's browser to your Lambda function.

  
  

**In this step, you're going to:**

-   Create a new API in API Gateway.
    
-   Configure the API's settings.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/architecture-2.0.png)

  



  
  

**Navigate to API Gateway**

-   In the AWS Management Console, head to the `API Gateway` console.

![Screenshot 2025-04-11 194321](https://github.com/user-attachments/assets/33eae69d-7c35-4c80-bad6-f39721d917b6)
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_9.png)



![Screenshot 2025-04-11 194410](https://github.com/user-attachments/assets/3ab1645c-e6f4-4e31-85db-075ab8036dc4)
  

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
> 
>   
> **💡 Why do we need the API Gateway?**  
> Directly exposing Lambda functions to user requests isn't best practice, because Lambda doesn't have built in security or API management features.
> 
> API Gateway brings in authentication and authorization features, and advanced API management capabilities (e.g. request routing) that make your app more efficient.


  
  

**Create a new API**

-   Scroll down the list of available API types.
    

> **💡 What are the different API types?**  
> API Gateway supports different types of APIs, like REST, HTTP, and WebSocket. Each type is suited for different use cases, whether it’s maintaining a standard web API (REST), providing real-time capabilities (WebSocket), or routing requests (HTTP).

-   Find **REST API**.
    

> 💡 **What is a REST API?**  
> A **REST API** (Representational State Transfer) is type of API that uses HTTP methods to interact with resources (more on HTTP methods later in this step).
> 
> REST is popular because it's simple and can be used with virtually any programming language. We're using a REST API today to set up an API that connects the user with your Lambda function.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_10.png)

  
![Screenshot 2025-04-11 194421](https://github.com/user-attachments/assets/3ac787a1-f35d-445e-816d-8b6d23c8bcfa)

-   Select **Build**.
    

  
  

**Configure the API**

-   Under API details, select **New API.**
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_11.png)

  

-   For **API name**, enter `UserRequestAPI`.
    
-   For **API endpoint Type**, select **Regional**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_12.png)


![Screenshot 2025-04-11 194457](https://github.com/user-attachments/assets/39b17b88-25ff-44f0-b2f4-74fb067a41fd)  

> **💡 What are endpoint types?**  
> **Endpoint types** define the scope of your API's availability. **Regional** endpoints are accessible within a specific AWS region, which is great for localized applications because it has low latency for clients in that region.
> 
>   
> **💡 What are the other endpoint types?**  
> Besides Regional, there are Edge-Optimized (for global applications) and Private (for internal networks) endpoints.
> 
> Each serves different needs depending on how and where you want your API accessed.

-   Select **Create API**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_13.png)

  
 ![Screenshot 2025-04-11 194521](https://github.com/user-attachments/assets/ccbfaaab-f9fc-4735-b677-7c0561f0ef8e)

Nice work setting up that API! The API will be the front door to our Lambda function, letting users access the function via HTTP requests.



> **💡 What's in my API's page?**  
> Your API’s page in the AWS Console provides a dashboard view of your API, including its methods, deployments, and settings. It's the central hub for managing and monitoring your API.

So good, that's the API Gateway set up.

To start using the API, we need to figure out how we can make requests to the API Gateway...

-----

## 🧱 Step #3

### Set up an API Resource

  

In this step, we'll create an API resource.

Resources are like the different sections or pages of your API. They help organize how your API handles different requests.

  
  

**In this step, you're going to:**

-   Create a new resource in your API.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/architecture-3.0.png)

  



  
  

**Create a resource**

-   Under **Resources**, select **Create resource**.
    

> **💡 What are API resources?**  
> **API resources** are individual endpoints within your API that handle different parts of its functionality.
> 
> For example, an API for a messaging app might have separate resources for retrieving messages and for retrieving user profiles.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_14.png)

  



-   For **Resource name**, enter `users`.
    

> **💡 What are resource path and resource name?**  
> A **resource path** is the URL path used to access that resource, e.g. `/messages` for retrieving messages and `/users` for retrieving user profiles.
> 
> The **resource name** is used in the API Gateway to refer to that resource, helping you manage and reference it easily in the console.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_15.png)

  
![Screenshot 2025-04-11 194742](https://github.com/user-attachments/assets/c860f170-9992-4065-a0b0-f55e8d264e0a)


-   Select **Create resource**.
    



-   Select the **/users** resource.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_16.png)

![Screenshot 2025-04-11 194755](https://github.com/user-attachments/assets/571aa7f2-b1da-4d64-90ca-876594b13a56)  

Woohooo! We're getting really close now. Great work creating the API resource.

Since a resource can be used for many different kinds of actions, we'll need to define what each of those actions are.

-----
## 🛠️ Step #4

### Set up an API Method

  

To round off our API's setup, let's create an API method. Methods are things you can do with a resource.

For example, you can use a GET method to retrieve data, a POST method to create data, a PUT method to update data, and a DELETE method to delete data. The list goes on!

  
  

**In this step, you're going to:**

-   Create a GET method for the **users** resource.
    
-   Connect the GET method to your Lambda function.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/architecture-4.0.png)

  



  
  

**Create a method**

-   In the **Methods** panel, select **Create method**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_17.png)

  

-   Select **GET** from the **Method type** dropdown.
    

> **💡 What are methods?**  
> **API methods** define the actions you can perform on a resource.
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

  

-   For the **Lambda function**, make sure the default region selected is where you've created your function.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_21.png)

  

-   Select your `RetrieveUserData` function.
    

> **Why do I select a Lambda function?**  
> The Lambda function you select will be the function that gets triggered when that API method is called.
> 
> In this case, when the GET method for the `/users` resource is called, API Gateway will pass that request to the Lambda function you set up. When the function runs, Lambda will retrieve user data in a DynamoDB table.


![Screenshot 2025-04-11 195008](https://github.com/user-attachments/assets/066acf22-d6de-433c-9fb6-8caced3cf91c)



-   Select **Create method**.
    
-   Method created!
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_22.png)

  
  ![Screenshot 2025-04-11 195036](https://github.com/user-attachments/assets/6d3aae3d-694d-41eb-a57c-b9e3d440c745)

Method done = API setup DONE! 😮‍💨

That's great, we'll just need to deploy our API and see it in action.

-----
## 🚀 Step #5

### Deploy your API

  

Finally, let's deploy our API. Deploying makes our API accessible through a public endpoint, so we can actually start using it.

It's like publishing a website - once it's deployed, anyone can access it!

  
  

**In this step, you're going to:**

-   Deploy your API to a new stage.

  
  

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

-   For **Stage name**, enter `prod`.
    

> **💡 Why is the stage called prod?**  
> `Prod` stands for production.
> 
> Production is the live environment where your API is fully working, and there is live traffic and real users using the API too.

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_24.png)

  





-   Select **Deploy**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_25.png)

  
  ![Screenshot 2025-04-11 195119](https://github.com/user-attachments/assets/246c60e8-295f-4883-958f-71b58528fa8f)

-   Deployment success!
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_27.png)

  
  ![Screenshot 2025-04-11 195158](https://github.com/user-attachments/assets/c6a4c987-b12f-4c23-bfc4-fb9a1284e854)


> **💡 What is on the 'prod' stage's page?**  
> This page shows you settings, metrics, and logs for your API when it’s in production.

  
  

**Visit your API**

-   On the same page, find your prod stage's **Invoke URL.**
    

> **💡 What is the invoke URL?**  
> The invoke URL is the URL where your API can be used.
> 
> In real world scenarios, developers use the `prod` stage's invoke URL into their live application's code, so users are using the live/production version of the API.

-   Copy the **Invoke URL**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_28.png)

  

-   Access the URL in a new tab on your browser.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_29.png)

  
![Screenshot 2025-04-11 195234](https://github.com/user-attachments/assets/506f84eb-9bd7-4ba7-ace6-2c086a551ae0)

Dang it - you'll get an error because we haven't set up our DynamoDB table yet. That's okay!

The API set up is all done, which means you've still learnt how to create a serverless API (how cool is that). We'll get to creating the DynamoDB table and connecting that with this API in the next project.

-----

## 💎 Secret Mission

### Showcase Advanced Skills

  

Welcome to your 🤫 exclusive 🤫 secret mission!

Your mission, should you choose to accept it, is to write documentation for your API in API Gateway.  
  

**💎 In this secret mission, get ready to:**

-   Write documentation (in JSON!) for your API.
    
-   Publish and download your documentation.
    
-   Showcase more advanced skills with APIs in your **project documentation.** Stand out from the rest!
    

> 💎 **Congratulations** - Secret Mission unlocked!


**Navigate to the Documentation Section**

-   Return to the **API Gateway** console.
    
-   From the left hand sidebar, find the section dedicated to **API: UserRequestAPI**.
    
-   Select the **Documentation** tab.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_33.png)

  

> **💡 What is API documentation?**  
> API documentation is a detailed description of an API's functionality, including its endpoints (e.g. `/users`), methods (e.g. `GET`), parameters (e.g. `userId`), and responses (e.g. errors or success response).
> 
> Good documentation is crucial for developers to understand how to use the API correctly and efficiently.


  
  

**Create Documentation**

-   Select **Create documentation part.**
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_34.png)

  
  ![Screenshot 2025-04-11 200048](https://github.com/user-attachments/assets/1e8cfc94-3bb6-4070-afcc-0b3acbc413a6)

-   For **Documentation type,** select **API**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_36.png)

  

> **💡 What are the different documentation types?**  
> In API Gateway, you can select documentation types to decide the scope of your documentation, from high-level overviews to detailed descriptions of specific request and response structures.
> 
> You can write documentation of the API as a whole, or individual resources, methods, and models.

-   In the code window, enter the following JSON documentation:
    


```json
{
  "description": "The UserRequestAPI manages user data retrieval and manipulation. It supports operations to retrieve user details based on unique identifiers.",
  "baseURL": "https://yo8z6vf1ql.execute-api.us-east-2.amazonaws.com/"
}

```

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_31.png)

  
  ![Screenshot 2025-04-11 195646](https://github.com/user-attachments/assets/b423407f-9ef2-4d59-8a48-ca1d7af21cbf)

> **💡 What does this documentation say?**  
> This documentation gives a high-level overview of your API.
> 
> We're simply writing a description of the API and its base URL. Easy peasy!

-   Check: Have you replaced the placeholder `baseURL` with your API's URL?
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_42.png)

  

> **🙋‍♀️ How do I find my API's URL?**
> 
> 1.  In the API Gateway console's left hand navigation panel, select **API settings.**
>     
> 2.  Under the API details section, copy the **Default endpoint.**
>     
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-api/unprocessed_image_37.png)
> 
>   


![Screenshot 2025-04-11 195710](https://github.com/user-attachments/assets/494f272d-39c7-46f5-8eeb-d0c5a90ef2b1)


-   Select **Create docmentation part.**
    

  
  

**Publish Your Documentation**

> **💡 What does publishing my documentation do?**  
> Publishing your documentation lets you export your work in a special file type (either Swagger or OpenAPI). Then, you can use external tools like [Swagger UI](https://swagger.io/tools/swagger-ui/) or [ReDoc](https://redocly.com/redoc) can then use your OpenAPI documentation to generate beautiful, interactive web pages about your API.
> 
> This lets other developers explore your API directly through their browsers.

-   Select **Publish documentation**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_39.png)

  

-   Select the **prod** stage.
    

> **💡 Why do I select a stage when I publish documentation?**  
> Selecting a stage when publishing documentation makes sure that your documentation is consistent with the API version deployed to that stage.
> 
> This means you can write different versions of documentation across different stages of your API lifecycle, such as development, testing, and production.

-   Enter `1` as your **Version**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_40.png)

  
![Screenshot 2025-04-11 195737](https://github.com/user-attachments/assets/32c89dd9-fde5-4884-b59d-c1e512ae4c8f)


![Screenshot 2025-04-11 195744](https://github.com/user-attachments/assets/d975d779-849e-43e0-9b28-d9abaeac12cf)


-   Select **Publish**.
    



-   Select **Download documentation**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_32.png)

  

-   Keep the default specification type.
    

> **💡 What are the two API specification types?**
> 
> 1.  **Swagger** (aka Swagger 2.0) is a popular format for describing REST APIs. Swagger lets developers define an entire API, including available endpoints, operations on each endpoint, operation parameters, authentication methods, and contact information, in a format that both people and machines can understand.
>     
> 2.  **OpenAPI** is actually the latest version of Swagger (surprise)! Swagger was donated to the OpenAPI Initiative, so the latest specification (i.e. standard for writing documentation) has been renamed from Swagger 3.0 to OpenAPI 3.
>     

-   In the **Export API** popup, select **Export with API Gateway extensions.**
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_43.png)

  
  ![Screenshot 2025-04-11 195348](https://github.com/user-attachments/assets/07df26aa-d5a4-41d6-8593-c5d895a8ca03)

> **💡 Why are we exporting with extensions?**  
> Exporting with extensions lets you see additional API settings specific to API Gateway, like the documentation you've added in the API Gateway console.

-   Select **Export API.**
    
-   Open the downloaded documentation.
    
-   Scroll to the **x-amazon-apigateway-documentation** section near the bottom of the document.
    

![](https://learn.nextwork.org/projects/static/aws-compute-api/processed_image_41.png)

  
![Screenshot 2025-04-11 200138](https://github.com/user-attachments/assets/f2cd7bd2-f3b4-45e2-9fac-f40bfdffc728)


> **💡 What else is in this documentation? Why are they here?**  
> The other text in this file are documentation that API Gateway has automatically generated for you!
> 
> You can see metadata like your API's version and title, resources (`/users`), and methods (like `GET`) you can perform on these endpoints.
> 
> The main difference between the automatically generated documentation and the manually written part in your API is the level of customization and specificity in each section. In your written documentation, you can address specific questions, add insights, or guide the user through the API’s functionality in a more user-friendly way.



Nice work, you've just learnt how to write and publish your own API documentation!

--------  

## 🗑️ Before you go

### Delete your resources

  

Now that we've tested our API, it's time to clean up the resources we created. This is important to avoid incurring unnecessary costs. It's like tidying up your kitchen after cooking - you don't want to leave a mess behind.

  
  

**Resources to delete:**

Delete the API in API Gateway.

Delete the Lambda function.

  
  

**Delete the API**

-   Navigate to the API Gateway service in the AWS Management Console.
    
-   Select your API (`UserRequestAPI`).
    
-   Select **Actions** and select **Delete API**.
    
-   Confirm the deletion.
    

  
  

**Delete the Lambda function**

-   Navigate to the Lambda service in the AWS Management Console.
    
-   Select your function (`RetrieveUserData`).
    
-   Select **Actions** and select **Delete**.
    
-   Confirm the deletion.
    



----------





🎉 Mission Accomplished

### That's a wrap!

  

You've just built your first serverless API with Lambda and API Gateway!

**You learned how to:**

-   🐑 Create and configure a Lambda function.
    
-   🚪 Set up and configure an API in API Gateway.
    
-   🧱 Create resources and methods within your API.
    
-   🚀 Deploy your API to a live stage.

Nice one - you've just set up the Second tier of a 3-tier architecture!
----

content owner : **Nextwork**