<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Fetch Data with AWS Lambda

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-lambda)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---




# Fetch Data with AWS Lambda

Learn how to retrieve DynamoDB table data using AWS Lambda function!

Welcome to this project on **Fetching Data with AWS Lambda!** 🌟

Imagine building applications that can grow effortlessly to handle thousands or millions of users **without managing a single server.** That's the power of serverless computing!

This project is your introduction to serverless and you will learn how to use a serverless AWS Lambda function to retrieve data from a DynamoDB table.

This is perfect for roles such as **Backend Developers**, **Cloud Engineers**, and **Cloud Architects**-where it is a key responsibility to create **scalable** cloud solutions that handle large amounts of data efficiently.

### In this project, get ready to...

🗄️ Create a database table to store user data.🐑 Create a serverless function to retrieve user data.📝 Write tests to validate if your function can fetch data from DynamoDB.🔑 Secure your serverless function with proper permissions.💎 Secure your database with an inline policy

### Three-Tier Architecture

This is also the THIRD project of an awesome **three-tier architecture** series. You can do this project standalone, or as a part of this series.

Three-tier architecture splits applications into three essential layers: presentation, logic, and data.

In this project, you're diving into the **data tier,** which is all about how you store and manage the data relevant to your application.

We'll talk more about this architecture in later projects - for now, let's focus on Lambda and DynamoDB. Make sure to follow the rest of this series to build up a fully functional three-tier solution! 🚀

-   PART ONE (Presentation Tier): **Website Delivery with CloudFront**

-   PART TWO (Logic Tier): **APIs with Lambda + API Gateway**

-   PART FOUR (putting all three layers together): **Build a Three-Tier Web App**

-----
  
## 🗄️ Step #1

### Set up DynamoDB

  

In this step, we'll create a DynamoDB table to store some user data.

  
  

**In this step, you're going to:**

-   Create a DynamoDB table.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/architecture-1.0.png)

  


**Head to the DynamoDB console**

-   Log in to the AWS Management Console [as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    
-   Make sure you're in the AWS region closest to you.
    
-   Head to the `DynamoDB` console.

![Screenshot 2025-04-11 200653](https://github.com/user-attachments/assets/3d6276f6-8411-4401-9130-b3d1bf5b6086)
    

> **💡 What is DynamoDB?**  
> DynamoDB is one of AWS's database services. It stands out as a fast and flexible way to store data, which makes it a great choice for apps that need quick access to large volumes of data e.g. games.
> 
> If you enjoy using DynamoDB in this project, make sure to check out the **Load Data into DynamoDB** project!

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_36.png)

 
 ![Screenshot 2025-04-11 200756](https://github.com/user-attachments/assets/6e493dac-7c3b-45b8-bcaa-67b704886fd8) 

**Create the DynamoDB table**

-   Select **Create table**.
    
-   For **Table name**, enter `UserData`.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_37.png)

  

-   For **Partition key**, enter `userId`.
    

> **💡 What is a partition key?**  
> A partition key is the heart of how DynamoDB organizes data. Think of it as a label that you can use to group similar items. Under the hood, the partition key is how DynamoDB spreads out your data across different servers for quick access and efficient querying.
> 
> Every item in your table _must_ have a unique partition key.

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_38.png)

  

-   Select **String** as the data type for the partition key.
    
-   Leave the default settings for the rest of the options.
    
-   Select **Create table**.
    

![DynamoDB create table button.](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_1.png)

DynamoDB create table button.

  
 ![Screenshot 2025-04-11 200914](https://github.com/user-attachments/assets/cc3fc6e5-7ae0-49b9-a5b7-12dd6d2c4dc1)


![Screenshot 2025-04-11 201005](https://github.com/user-attachments/assets/d5e31791-0aca-4093-bded-cfdcdeb1cb48)

Great stuff! You've taken the first big step in this project and set up your DynamoDB table.

----

## ➕ Step #2

### Add a Table Item

  

Now that we have our DynamoDB table set up, let's add some sample data so we can see our Lambda function in action later.

  
  

**In this step, you're going to:**

-   Add a sample user to your `UserData` table.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/architecture-2.0.png)

  



**Add a table item**

-   Once the table status changes to **Active**, select your `UserData` table.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_1.png)

  

-   Select **Explore table items**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_2.png)


![Screenshot 2025-04-11 201110](https://github.com/user-attachments/assets/c41e226d-21a5-4099-95b5-d99033b6fde0)
  

-   At the **Items returned** panel, select **Create item**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_3.png)



![Screenshot 2025-04-11 201120](https://github.com/user-attachments/assets/f8d1f94f-d595-4260-bbf0-dda843127651)


![Screenshot 2025-04-11 201138](https://github.com/user-attachments/assets/4095e2b6-1fd4-43ed-9073-aa37cf748cd7)
  

-   Select **Switch to JSON view**. 
    
![Screenshot 2025-04-11 201147](https://github.com/user-attachments/assets/c129fd5d-36cd-4668-9c65-daffd87dc8c5)

> **💡 Why is there a JSON view in DynamoDB?**  
> Under the hood, DynamoDB stores your data in JSON! By switching to JSON view, you can edit your data in a code format instead of filling out a form.
> 
> This is also a great way to save time - if you have data with lots of attributes, you wouldn't want to fill each of them out one by one for every item.

-   Toggle off **View DynamoDB JSON**.

![Screenshot 2025-04-11 201200](https://github.com/user-attachments/assets/de1ffd74-69d0-4738-9585-2aa3e205f89d)
    

> **💡 What is DynamoDB JSON?**  
> DynamoDB JSON is a special flavor of JSON used by DynamoDB that's a bit more specific. It tells your database exactly what type of data each piece is (e.g. a string or a number) on top of storing the data's values.
> 
> We won't be writing in DynamoDB JSON so we can stick with the simpler JSON format, so we can turn this off.

-   Paste the following JSON into the editor:
    
![Screenshot 2025-04-11 201219](https://github.com/user-attachments/assets/1ee13781-ac46-47c8-a2b8-a375b6f33388)



```json
{
  "userId": "1",
  "name": "Test User",
  "email": "test@example.com"
}

```

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
> Notice how we didn't have to add **name** or **email** as new attributes (i.e. table fields) beforehand!
> 
> DynamoDB is **schemaless**, meaning you can add attributes as you need, and every item in your database can have a different set of attributes. This flexibility is one of the key benefits of using a NoSQL database like DynamoDB.

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_39.png)

  
![Screenshot 2025-04-11 201242](https://github.com/user-attachments/assets/b8b38dbc-89cf-443d-940f-12091ecf9f11)


-   Select **Create item**.
    
-   Verify that the item was created successfully. You should see it listed in the **Items returned** tab.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_40.png)


![Screenshot 2025-04-11 201308](https://github.com/user-attachments/assets/41bcc9b7-5f92-450b-a68b-0f6e65e6392d)  

Phew! That's a piece of data in our DyanmoDB table now. Awesome to have some sample data we can use for the rest of this project.

-----

## 🐑 Step #3

### Create the Lambda Function

  

Time for Lambda to enter the picture!

Now that our DynamoDB table and data are set up, let's set up a function that can retrieve table items on demand.

  
  

**In this step, you're going to:**

-   Set up a Lambda function.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/architecture-3.0.png)

  



**Create the function**

-   Navigate to the `Lambda` service in the AWS Management Console.
    

> **💡 What is AWS Lambda?**  
> **AWS Lambda** is a service that lets you run code without needing to manage any computers/servers - Lambda will manage them for you.
> 
> Lambda runs your code only when you need it to (so you're not paying for any idle time).
> 
> It also scales automatically, from a few requests per day to thousands per second - all you need to do is supply your code in one of the languages that Lambda supports.

-   Select **Create function**.
    

> **💡 What is a Lambda function?**  
> A Lambda **function** is a piece of code that you run in AWS Lambda.
> 
> You write Lambda functions to do things like process data, respond to events, or run automated tasks.

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_5.png)

  



-   Select **Author from scratch**.
    

> **💡 There are other ways to create a Lambda function?**  
> Yup! We'll create ours from scratch (i.e. we're writing the function code ourselves), but Lambda functions can be created from blueprints, cloned from existing functions in your account, imported from a ZIP file, or deployed through a repository to jumpstart development.

-   For **Function name**, enter `RetrieveUserData`.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_6.png)

  

-   For **Runtime**, choose a **Node.js** runtime.
    

> **💡 What does runtime mean?**  
> The **runtime** is like the environment where your code lives and runs.
> 
> While you write code in a programming language, the runtime provides the actual environment where that code runs. For example, Python code needs a Python runtime environment.
> 
> Selecting the right runtime for your AWS Lambda function makes sure it has everything (i.e. dependencies) needed to run efficiently.
> 
>   
> **💡 Extra for PROs: What is Node.js?**  
> **Node.js** is a popular **JavaScript** runtime environment.
> 
> Traditionally, JavaScript is used for scripts that run right in your web browser, handling tasks like animations and form validations. This browser-based setup means all the JavaScript action happens on your device after the web page loads.
> 
> But with Node.js, you can take JavaScript to the server side. Now, you're running scripts on a server before anything even reaches the browser.
> 
> This is a big deal because it lets developers use JavaScript for both frontend and backend tasks, which makes development much more efficient. You can use Node.js to build things like server-side apps, command-line tools, or even chat with databases using JavaScript.
> 
> In our case, we're using Node.js to create the backend for a web app.

-   Expand the **Change default execution role** arrow.
    
-   Keep **Create a new role with basic Lambda permissions**.
    

> **💡 What's an execution role?**  
> An execution role is an IAM role for your Lambda function. It defines what the function is allowed to do, e.g. accessing other AWS services like DynamoDB.
> 
> By default, AWS creates a role for Lambda with basic permissions for writing logs to CloudWatch. That's why you could see an error message when you tested your Lambda function!
> 
>   
> **💡 Why do we need an execution role?**  
> Security! We don't want our Lambda function to have unlimited access to everything in our AWS account.
> 
> The execution role makes sure the function only has the permissions it needs to do its job, minimizing the potential for security vulnerabilities.



-   Note the message at the bottom that says "Lambda will create an execution role named RetrieveUserData-role-9w66kle5".
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_8.png)

  

-   Select **Create function**.
    

Easy as! Is your Lambda setup all done?

Well, although we've created a function, it's not going to do anything until we write its code. Let's do that next.

----

## 💻 Step #4

### Implement the Lambda Function Logic

  

Let's get coding! We'll write the code that retrieves user data from our DynamoDB table.

  
  

**In this step, you're going to:**

-   Add code to your Lambda function to retrieve data from DynamoDB.
    
-   Deploy the function.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/architecture-4.0.png)

  



**Add the code**

-   In the Lambda code editor, replace the existing code with the following:
    



```javascript
import { DynamoDBClient } from "@aws-sdk/client-dynamodb";
import { DynamoDBDocumentClient, GetCommand } from "@aws-sdk/lib-dynamodb";

const ddbClient = new DynamoDBClient({ region: 'YOUR-REGION' }); // Make sure to replace this with your actual AWS region
const ddb = DynamoDBDocumentClient.from(ddbClient);

async function handler(event) {
const userId = String(event.userId);  // Make sure to extract userId from the event
const params = {
        TableName: 'UserData',
        Key: { userId }
    };

    try {
        const command = new GetCommand(params);
        const data = await ddb.send(command);  // Log the raw response from DynamoDB
        console.log("DynamoDB Response:", JSON.stringify(data));
        const { Item } = data;
        if (Item) {
            console.log("User data retrieved:", Item);
            return Item;
        } else {
            console.log("No user data found for userId:", userId);
            return null;
        }
    } catch (err) {
        console.error("Unable to retrieve data:", err);
        return err;
    }
}

export { handler };

```

> **💡 What's this code doing?**  
> The first half of the code uses the **AWS SDK** for JavaScript to interact with DynamoDB.
> 
> It takes a `userId` as input, grabs the corresponding data from the `UserData` table, and returns it to you.
> 
> The second half of the code (i.e. beginning with `try {`) handles potential errors during the database operation, so you get a tailored error message that tells you what went wrong.
> 
>   
> **💡 What is AWS SDK?**  
> The **AWS Software Development Kit (SDK)** is a set of tools that let developers build apps that interact with AWS.
> 
> Think of it like a library of pre-written code that lets you use AWS services without having to write all the code yourself. It gives you functions and classes that simplify common tasks, like creating an S3 bucket or launching an EC2 instance.
> 
> There's a different SDK for different programming languages or platforms, and JavaScript is one of them! Your code uses the AWS SDK to use pre-written functions for communicating with DynamoDB and getting data from a table. Without the SDK, you'd have to manually write the code to interact with AWS, which would be much more complex and error-prone.



-   Make sure you've replaced `YOUR-REGION` with your actual AWS region code (e.g., `us-east-1`).
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_9.png)

  

-   Select **Deploy**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_44.png)



![Screenshot 2025-04-11 202021](https://github.com/user-attachments/assets/ce3bcf06-28ba-44f1-a070-84b4e09955ba)
  

-   We'll wait until the deployment is successful...
    



-   Check: Is your deployment a success?
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_15.png)

  
![Screenshot 2025-04-11 202106](https://github.com/user-attachments/assets/38a9dd83-daec-4626-ab87-1632670b073c)


Great! You've just written and deployed the Lambda function's code. It should be working now, let's give it a test.

-----


## 🧪 Step #5

### Write a Lambda Function Test

  

Let's test our Lambda function to make sure it's working. Lucky for us, AWS Lambda comes with a handy testing feature we can use.

  
  

**In this step, you're going to:**

-   Create a test event for your Lambda function.
    
-   Run the test and observe the results.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/architecture-5.0.png)

  



**Create and run the test**

-   Still in your Lambda function, select the **Test** tab.
    

> **💡 What does the Test tab do?**  
> The Test tab is your playground for running your Lambda function.
> 
> In a function test, you can send fake events to your function to see how it would react.
> 
> In our case, we're writing tests that lets us see how our function would react if we made a data request.

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_10.png)

  

-   In the **Event JSON** panel, enter the following JSON:
    



```json
{
  "userId": "1"
}

```

> **💡 What will this test do?**  
> In this test, we're asking our Lambda function to search for an item in our DynamDB table. The item needs to have a userID of `1`  
> **💡 Why are we entering the test in JSON?**  
> By using JSON to input test data, we ensure it's in a format that’s easy for Lambda to understand and work with.

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_11.png)

  

-   Select **Test**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_12.png)

  

![Screenshot 2025-04-11 202308](https://github.com/user-attachments/assets/b7f5ffa5-fdc1-4f5d-8c31-3ed1eb9a4994)

-   Yay! Looks like we've got a successful test?
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_13.png)

  
![Screenshot 2025-04-11 202449](https://github.com/user-attachments/assets/80302897-7a7d-4f6a-a4e3-fc363793462f)

-   Expand the **Details** arrow for your successful test.
    
-   Nevermind, we have an error!
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_17.png)

  
  ![Screenshot 2025-04-11 202643](https://github.com/user-attachments/assets/5fd5acf1-1afc-43bd-8ccb-0ffbc393cff2)

> **🙋‍♀️ I don't see the same error**  
> Did you get an `ENOTFOUND` error instead?
> 
> ![](https://learn.nextwork.org/projects/static/aws-compute-lambda/UNFRAMED.png)
> 
> Check whether you've correctly replaced `YOUR-REGION` with your actual AWS region (e.g., `us-east-1`) in the function code.

-   Expand the full error message.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_42.png)

  



-   Can you tell why we've run into an error?
    

> **💡 Why did you get this error?**  
> Even though we created an execution role for our Lambda function, we haven't given it explicit permission to access our DynamoDB table. This means DynamoDB is currently blocking off our Lambda function from reading the table's items!
> 
> Because Lambda can't read any items, it has no choice but to tell us that its access was denied.
> 
>   
> **💡 Why did the test still show as a success, when your access was actually denied?**  
> The "success" message simply means the function itself could run (there are no errors with the code), it doesn't mean the function achieved what you want it to do!

-----

## 🔑 Step #6

### Grant DynamoDB Access to Lambda

  

Let's fix that permissions issue! We'll give our Lambda function the necessary permissions to read data from our DynamoDB table.

  
  

**In this step, you're going to:**

-   Grant your Lambda function read access to DynamoDB.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/architecture-6.0.png)

  



**Grant DynamoDB access to Lambda**

-   Switch to the **Configuration** tab in your Lambda function.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_18.png)

  

-   Select **Permissions**.
    

> **💡 What is in the Permissions tab?**  
> The Permissions tab shows the execution role linked with your Lambda function and the permissions given to that role. It's where you control what your function is allowed to access.

-   Select the execution role name (it will look something like `RetrieveUserData-role-xxxxxxxx`).
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_19.png)

  
![Screenshot 2025-04-11 203445](https://github.com/user-attachments/assets/2e5918af-1fbc-4ce5-b2b9-baa14282ab3f)

-   This shortcut will take you to the IAM console, with your Lambda function readily open.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_20.png)



-   Select **Add permissions**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_21.png)


![Screenshot 2025-04-11 203544](https://github.com/user-attachments/assets/673f70bf-faad-4670-8ef5-df1dd3307287)  
  

-   Select **Attach policies**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_22.png)

  

-   Type `DynamoDB` in the search bar.
    

  
  

Ooo, we have four different permission policies that grants access to DynamoDB.

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_24.png)

  
![Screenshot 2025-04-11 203618](https://github.com/user-attachments/assets/e240ad70-f8c8-4265-97bc-c66b1fb4f92b)



-   To figure out which permission policy to apply, first it's best to head back to the error message.
    
-   What was the specific action that was denied?
    
-   Aha, it was **GetItem**!
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_43.png)

  

> **💡 Why are we reviewing the error message again?**  
> Reviewing the error message tells us exactly which permissions the Lambda function lacks.
> 
> To solve the access denied error, we can add a permission policy that give us the permissions we're lacking!



-   Head back to the policy set up page.
    
-   Expand the bottom two permission policies - can you spot the **GetItem** permission?
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_25.png)

![Screenshot 2025-04-11 204000](https://github.com/user-attachments/assets/82750a1a-887f-4edd-94d1-c9a01074292e)
  

> **💡 Nope... What do "AWSLambdaDynamoDBExecutionRole" and "AWSLambdaInvocation-DynamoDB" do?**
> 
> -   **AWSLambdaDynamoDBExecutionRole** gives your Lambda function the permissions to see a DynamoDB **stream** i.e. a live news feed of changes to your tables (like new, updated, or deleted items) in the last 24 hours.
>     
> -   **AWSLambdaInvocation-DynamoDB** is used to automatically trigger your Lambda functions in response to events captured in DynamoDB stream. You'd use this in apps where you need immediate action based on data changes—for example, if a user should get a notification when they add a new product to their in-app shopping cart.
>     



-   Now expand **AmazonDynamoDBReadOnlyAccess**.
    
-   Can you spot **GetItem** in the policy?
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_27.png)


![Screenshot 2025-04-11 204045](https://github.com/user-attachments/assets/6b4dff55-2b33-49d3-b51c-5b371bf380eb)
  

-   Yess, we can!
    
-   Select **AmazonDynamoDBReadOnlyAccess** as the permission policy we'll use.

![Screenshot 2025-04-11 204107](https://github.com/user-attachments/assets/b36b74b0-5af9-4bff-9aa7-6d24bb297b9c)
    

> **💡 What about "AmazonDynamoDBFullAccess"?**  
> AmazonDynamoDBFullAccess lets you do everything with DynamoDB, like creating, deleting, and managing tables. It also lets you read and write data.
> 
> But, if your Lambda function only needs to read data, you don't need this level of access. Granting this permission when you don't need it can make your resources less secure. For example, if someone gets unauthorized access to your function, they could manipulate or delete crucial data by editing your function, which could disrupt your service or lead to data loss.

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_23.png)

  



-   Select **Add permissions**.

![Screenshot 2025-04-11 204147](https://github.com/user-attachments/assets/e9b42c5c-db7f-4e45-ba74-2651098ac545)
    

Yay! Permissions added. This means your Lambda function should be able to read DynamoDB table items.

-----
## ✅ Step #7

### Re-test Your Lambda Function

  

Let's re-run our test and make sure our Lambda function now has the necessary permissions to access DynamoDB.

  
  

**In this step, you're going to:**

-   Re-run the Lambda function test.
    
-   Validate that your Lambda function now works!
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/architecture-7.0.png)

  



**Re-run the test**

-   Head back to the **Test** tab in your Lambda function.
    
-   Select **Test**.
    

![Screenshot 2025-04-11 204224](https://github.com/user-attachments/assets/8fad85f1-df3b-4d8b-9e44-a68fec951c13)
  
  

You should now see a successful test execution _without_ the `AccessDeniedException` error.

Yay! The response should show the user data we added in our DynamoDB table.

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_41.png)

![Screenshot 2025-04-11 204249](https://github.com/user-attachments/assets/dc14e164-2f13-4077-b7b3-691035b007de)  

> **💡 What are some uses cases of what I've built today?**  
> Lambda can be a **serverless backend** for web apps, grabbing data from DynamoDB when a user logs in or interacts with your app. For example...
> 
> 1.  Lambda can help customers find products, get product information or see their order history by fetching data from DynamoDB.
>     
> 2.  Lambda can help social media apps fetch user profiles or automatically retrieve all content (e.g. videos or images) linked with a profile.
>     
> 3.  Lambda can help news sites or blogs fetch articles based on user queries.
>     

----



## 💎 Secret Mission

### Tighten DynamoDB Security

  

Welcome to your 🤫 exclusive 🤫 secret mission!

Your mission, should you choose to accept it, is to update your Lambda function's permissions to better secure your database.

  
  

**💎 In this secret mission, get ready to:**

-   Update your Lambda function's permission policies.
    
-   Validate that your Lambda function still works.
    
-   Showcase your secret mission in your **project documentation.**
    

> 💎 **Congratulations** - Secret Mission unlocked!



-   Switch to the **Configuration** tab in your Lambda function.
    
-   Select **Permissions**.
    
-   Select the execution role name (it will look something like `RetrieveUserData-role-xxxxxxxx`). This will take you to the IAM console.
    
-   Select **AmazonDynamoDBReadOnlyAccess**.
    
-   Select **Remove**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_45.png)

  
![Screenshot 2025-04-11 204448](https://github.com/user-attachments/assets/0f25ffe5-6782-4d42-8474-2b1bb071fd7d)

-   Select **Remove** again at the popup.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_46.png)

  
  ![Screenshot 2025-04-11 204507](https://github.com/user-attachments/assets/877b70d0-7617-4500-b86e-e6c4cc3b6d48)


![Screenshot 2025-04-11 204517](https://github.com/user-attachments/assets/832f22f0-753c-44ee-8f68-6f2a43cd495d)

-   Select **Add permissions** and then **Create inline policy**.
    

> **💡 Why use an inline policy instead of a managed policy like AmazonDynamoDBReadOnlyAccess?**  
> While `AmazonDynamoDBReadOnlyAccess` grants read-only access to _all_ your DynamoDB tables, an inline policy allows for more granular control. In this case, we only want our Lambda function to access the `UserData` table, so an inline policy is more secure.
> 
> It's just like the reason why we gave our Lambda function ReadOnlyAccess instead of full access earlier in this project. We're now narrowing permissions even more - let's take out the unnecessary permissions that ReadOnlyAccess is still giving us.

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_28.png)

  
![Screenshot 2025-04-11 204537](https://github.com/user-attachments/assets/0ef75f32-a4c4-418b-82b6-f560d99b0fcc)



You can complete this part in either the **Visual** editor or in **JSON...** take your pick!

> **💡 What's the difference between using the visual editor vs JSON?**  
> The final policy you create is exactly the same, but the process looks different.
> 
> With the visual editor, you're using a more beginner friendly, guided interface that breaks up policy writing into checkboxes and dropdowns.
> 
> With JSON, you're writing the policy directly without guidance. It's more challenging, but is a more efficient solution if you're familiar with policy writing.

  
  

**OPTION A: Visual Editor**

-   Stay on this tab.
    
-   Under **Select a service**, enter `DynamoDB`
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_29.png)


![Screenshot 2025-04-11 204741](https://github.com/user-attachments/assets/09190105-7600-49c7-b78f-0311100510a4)  

-   Under the **Resources** tab, select **Specific**.
    
-   Select **Add ARNs**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_31.png)

  

Fill out the details for your DyanmoDB table's ARN.

-   Under **Resource region**, enter the region code where you deployed the table.
    
-   Under **Resource table name**, enter `UserData`
    
-   Select **Add ARNs.**
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_30.png)

  

-   Skip the steps in OPTION B and move on straight to **Create Your Policy.**
    

**OPTION B: JSON**

-   Choose the **JSON** tab.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_47.png)

  

-   Replace the existing JSON with the following:
    
![Screenshot 2025-04-11 204957](https://github.com/user-attachments/assets/08f0238e-4b78-4077-bd6d-46032f57e8cd)


```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "DynamoDBReadAccess",
            "Effect": "Allow",
            "Action": [
                "dynamodb:GetItem"
            ],
            "Resource": [
                "arn:aws:dynamodb:YOUR-REGION:YOUR-ACCOUNT-ID:table/UserData"
            ]
        }
    ]
}

```

-   Remember to replace `YOUR-REGION` with your AWS region and `YOUR-ACCOUNT-ID` with your AWS account ID.
    
-   You can find your account ID at the upper right corner of the AWS Management Console (select your IAM user's name).
    



**Create Your Policy**

-   Select **Next**.
    
-   For the **Policy name**, enter `DynamoDB_UserData_ReadAccess`
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_33.png)

  

![Screenshot 2025-04-11 205049](https://github.com/user-attachments/assets/20883213-65fb-4d13-a80a-d5adf29d69f1)


-   Select **Create policy**.
    



-   You should be able to see it in the **Permissions Policies** tab now.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_34.png)


![Screenshot 2025-04-11 205101](https://github.com/user-attachments/assets/8bdc35e7-539a-451b-b118-c986ad2772f6)  

-   Go back to your Lambda function's **Test** tab.
    
-   Select **Test** again.
    
-   You should be able to see the results for your DyanamoDB table's items again.
    
![Screenshot 2025-04-11 205146](https://github.com/user-attachments/assets/c13d981b-6e9b-4431-9a86-13eebde37f81)

Nice work! You've tightened the Lambda function's permission settings and still validated that the function works.



-------  

## 🗑️ Before you go

### Delete your resources

  

Time to clean up our AWS resources to avoid unnecessary costs.

  
  

**Resources to delete**

Your Lambda function.

Your DynamoDB table.

  
  

**🚨 Steps below**

  
  

**Delete the Lambda function**

-   Head to the `Lambda` service.
    
-   Select the `RetrieveUserData` function.
    
-   Select the **Actions** dropdown.
    
-   Select **Delete**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_50.png)

  

-   Type `confirm` to confirm the deletion.
    
-   Select **Delete**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_51.png)

  

  
  

**Delete the DynamoDB table**

-   Head to the `DynamoDB` service.
    
-   From the left hand navigation bar, select **Tables**.
    
-   Select the `UserData` table.
    
-   Select **Delete**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_48.png)

  

> **💡 What are these warnings about?**
> 
> -   **Delete all CloudWatch alarms:** Keep this **checked ✅** Deleting any CloudWatch alarms associated with this table will save you from unnecessary charges.
>     
> -   **Create an on-demand backup:** Keep this **unchecked** ❌ You can create a backup of your table to save for the long term, so you restore your data to its exact state before deleting it. Additional charges apply for on-demand backup and restore, so we won't use this option.
>     

-   Type `confirm` to confirm the deletion.
    
-   Select **Delete**.
    

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/processed_image_49.png)


-------

🎉 Mission Accomplished

### That's a wrap!

  

High five! You've built a Lambda function that retrieves data from a database – no servers required (how cool).

![](https://learn.nextwork.org/projects/static/aws-compute-lambda/architecture-complete.png)

  

You've just learned how to:

-   🗄️ Set up a DynamoDB database.
    
-   🐑 Create and configure an AWS Lambda function.
    
-   💻 Write code to interact with DynamoDB using the AWS SDK.
    
-   🧪 Test your Lambda function.
    
-   💎 Tighten permission settings for your Lambda function.

----

content owner : **Nextwork**
    



