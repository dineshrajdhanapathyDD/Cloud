<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Create an API for Your RAG Chatbot

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-rag-api)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---




# Create an API for Your RAG Chatbot

Build a RAG chatbot using Amazon Bedrock, and create an API that makes your chatbot accessible to any application!

## Summary

Welcome to part THREE of our RAG chatbot series! 🎉

In this project, you'll take your RAG chatbot to the next level by creating an API that lets **any** application use your chatbot. No more being limited to the AWS Console or terminal - if other applications like websites or mobile apps can use your chatbot's features via the API, they won't need to set up their own chatbot from scratch.

This project is most ideal for roles like **Backend Developer**, **Cloud Architect**, or **Machine Learning Engineer**, where you need to know how to deploy AI models as production-ready web services.

Creating an API is also the perfect next step after learning how to:

-   [Part 1: Create a RAG chatbot in Amazon Bedrock](https://link.nextwork.org/projects/ai-rag-bedrock?utm_source=project-app)
    
-   [Part 2: Manage your chatbot through AWS CloudShell](https://link.nextwork.org/projects/ai-rag-cloudshell?utm_source=project-app)
    
-   Note: You can follow along even if you haven't completed the first two projects yet! We'll walk through step by step how to build the chatbot and API from scratch.
    

  

### In this project, get ready to...

-   🪣 Store your chatbot's knowledge in **Amazon S3**.
    
-   🧠 Set up your chatbot's brain using **Amazon Bedrock** and AI models.
    
-   💻 Build a **web API** to interact with your chatbot.
    
-   🔒 **Secure and test** your API.

![](https://learn.nextwork.org/projects/static/ai-rag-api/architecture-complete.png)

----
## 👀 Step #0

### Before we start Step #1...

In this project, we're turning a RAG chatbot into an API!  
  

**Why do APIs matter?**

Think about popular AI tools like ChatGPT - they don't just work through a command line. They have beautiful web interfaces, mobile apps, and can even be integrated into other tools like Slack or Microsoft Teams.

How do they do this? Through APIs!

By creating an API for your chatbot, you'll open up endless possibilities for how others can interact with it. Want to build a sleek web interface? Add your chatbot to a mobile app? Or integrate it with your favorite messaging platform? With an API, all of this becomes possible.

  
  

**What is an API?**

An API, or Application Programming Interface, is a way for different software systems (like applications) to talk to each other.

In our case, while the AWS Management Console and CLI are great for manual interactions (i.e., you calling your chatbot directly), an API lets your chatbot be integrated into an app's code. Instead of manually typing commands into the console, your application can send requests to AWS Bedrock’s API endpoints, get responses, and process them automatically.

  
  

**How does an API work?**

An API works in 5 steps. Let's say you build a website that has your chatbot built in:

1.  When a user asks a question in the chat window, your website sends a request to the API.
    
2.  The API receives the request, and passes the request to your chatbot living in your AWS environment.
    
3.  Your chatbot processes the request and sends a response back to the API.
    
4.  The API receives the response, and sends the response back to the website.
    
5.  The website displays the response to the user.
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/api.png)

  


**🤔 How in the world are we going to build this?**

![](https://learn.nextwork.org/projects/static/ai-rag-api/annotated.png)

  

First, we'll set up our chatbot:

-   In 🧠 Step #1, we'll create a Knowledge Base in Bedrock and store our chatbot's information in S3.
    
-   In 🤖 Step #2 in Bedrock that will help our chatbot communicate what it's learned.**AI models**, we'll pick
    

  
  

Then, we'll learn how to use our chatbot from our local computer (i.e. without the AWS Management Console):

-   In 🏠 Step #3, an AWS service that lets you run commands in your terminal.**AWS CLI**, we'll set up your local terminal to use the
    
-   In 🔍 Step #4, we'll query our chatbot to make sure we can access Bedrock from your local terminal.
    

  
  

Finally, we'll build an API that makes your chatbot available to other applications:

-   In 🕸️ Step #5, we'll set up your local environment to create the API.
    
-   In ❓ Step #6, we'll run the API and watch your chatbot in action!

----
## 🧠 Step #1

### Creating the Knowledge Base

To set up a RAG chatbot, we need to set up the information it needs to know! That's where Amazon S3 comes in - it's going to be the home for all the documents and information that your chatbot will learn from.

  
  

**In this step, you're going to:**

-   Create an S3 bucket to store your chatbot's training materials.
    
-   Upload documents that your chatbot will learn from.
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/architecture-1.png)

  


  
  

**Create an S3 Bucket**

-   Log in to the AWS Management Console [as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    
-   Make sure you're in the **Ohio** (**us-east-2**) region.
    

> **💡 Why Ohio?**  
> Some features in Bedrock, like the AI models we'll use and API features for the secret mission (🤫) are only offered in certain regions.
> 
> Ohio (us-east-2) luckily offers all the features we need for this project. Other regions, from Sydney (ap-southeast-2) to Ireland (eu-west-1) do not offer all the features we'll use. This is because the data centres in those regions might not have the hardware required for advanced AI models, or because AWS chooses to roll out new features in certain regions first before making them available globally.

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.1.png)

  

-   Head to the `S3` console.
    
-   Select **Create bucket**.
    

> 💡 **What is Amazon S3?**  
> Amazon S3 (Simple Storage Service) is AWS's storage system. Think of it as a digital folder where you can store your documents, photos, videos, and other files. We'll use S3 to store the data that your chatbot will learn from.

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.7.png)

  

-   For **Bucket name**, enter a unique name like `nextwork-rag-documentation-<your-initials>`.
    

> 💡 **Extra for Experts: Why add your initials?**  
> S3 bucket names must be globally unique across all AWS accounts. Adding your initials helps ensure your bucket name won't conflict with other users' buckets.
> 
> Make sure your bucket name:
> 
> -   Only uses lowercase letters, numbers, dots (.), and hyphens (-)
>     
> -   Starts with a letter or number
>     
> -   Is between 3 and 63 characters long
>     

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-2.png)

  

-   Under **Object Ownership**, leave **ACLs disabled (recommended)** selected.
    

> 💡 **Extra for Experts: Why leave ACLs disabled?**  
> This makes managing permissions simpler. The bucket owner gets full control, which helps prevent accidental permission issues.

-   Under **Block Public Access settings**, make sure **Block all public access** is checked (default setting).
    

> 💡 **Extra for Experts: Why block public access?**  
> This keeps your data secure by ensuring only authorized users and services can access your bucket. Since your chatbot's training data doesn't need to be publicly accessible, this is the safest option.

-   Leave the default versioning and encryption settings.
    

> 💡 **Extra for Experts: Why use encryption?**  
> Encryption automatically encrypts your data when it's stored, adding extra security. If anyone tries to access your documents without the right permissions, they won't be able to read them.

-   Select **Create bucket**.
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-3.png)

  

**Upload Data to S3**

-   Click into your newly created bucket.
    
-   Select **Upload**.
    

> 💡 **Why are we uploading data to S3?**  
> This data will be the source of knowledge for your chatbot. Think of it as the reference material your AI will use to answer questions! The more relevant and well-organized your data is, the better your chatbot will perform.
> 
> In our case, we're about to upload a student's portfolio of NextWork project documentation. This will make our chatbot an expert on this student's project experience and the skills they've built!

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.1.png)

  

-   Download this ZIP file with 10 documents inside. You can use these 10 files to train your chatbot: [Download the ZIP file](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Turn%20Your%20Data%20into%20an%20AI%20Chatbot/nextwork-projects.zip)
    

> 🙋‍♀️ **I want to use from my own documents**  
> You definitely can! That's the beauty of RAG - you can upload anything you want your chatbot to know. Even if you start with our recommended documents, you can always challenge yourself to redo the project with your own!
> 
> If you want to use your own documents, we'd recommend uploading around 10 files to start with, so your chatbot has enough information to answer questions.

-   Head to your local computer's **Downloads** folder and unzip the file.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.4.png)

  

-   Click into the unzipped folder and confirm you see the 10 documents inside.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.9.png)

  

-   Head back to your S3 tab in your browser. You should be in an **Upload** page.
    
-   Select **Add files**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.3.png)

  

-   Select the 10 documents inside the unzipped folder. Select **Open**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.8.png)

  

-   Select **Upload**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.5.png)

  

Great! Your files will take a few minutes to upload into your S3 bucket. In the meantime...

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.6.png)

  



> **🙋‍♀️ Error: Access Denied**  
> If you get an "Access Denied" error while uploading, it means your IAM user doesn't have the right permissions. Make sure your IAM user has the `AmazonS3FullAccess` policy attached.
> 
> To fix this:
> 
> 1.  Go to the IAM console
>     
> 2.  Find your user
>     
> 3.  Add the `AmazonS3FullAccess` policy
>     
> 4.  Try uploading again
>     

Great work setting up your S3 bucket! But having documents stored in S3 isn't enough - your chatbot needs a way to understand and process this information.

That's where your chatbot's knowledge management system, called the **Knowledge Base**, comes in. Let's create a Knowledge Base that helps your chatbot understand and process the documents you've uploaded.

  
  

**Navigate to Amazon Bedrock**

-   In a new tab, open the `Amazon Bedrock` console.
    

> 💡 **What is Amazon Bedrock?**  
> **Amazon Bedrock** is an AWS service that lets you use powerful AI models to build generative AI applications. In our case, we'll use it to build a RAG chatbot that can answer questions about our documents.

  
  

**Create a Knowledge Base**

-   In the Amazon Bedrock console, find the left hand sidebar.
    
-   Under **Builder Tools,** select **Knowledge Bases**.
    

> 💡 **What is a Knowledge Base?**  
> A **Knowledge Base** is a knowledge management system for your chatbot. When you ask your chatbot a question, the Knowledge Base is responsible for quickly finding the information that will answer your question.
> 
> Think of it like a skilled librarian who:
> 
> 1.  Reads and understands all the information your chatbot needs to know.
>     
> 2.  Organizes the information in a way that makes it easy to find.
>     
> 3.  Can quickly find relevant information when you ask your chatbot a question.
>     

-   Select **Create** in the **Knowledge Bases** section.
    
-   A dropdown will appear. Select **Knowledge Base with vector store**.
    

> 💡 **Extra for Experts: What is a vector store?**  
> A **vector store** is a special way of organizing information that understands **semantic concepts** i.e. the **meaning** of the words in the text.
> 
> For example, if you stored recipes inside your Knowledge Base, a regular search for "quick breakfast ideas" might only find recipes with the exact words you typed. But a vector store might also find "5-minute morning meals" because it understands they're related concepts!

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.1.png)

  

-   Under **Knowledge Base name**, enter `nextwork-rag-documentation`.
    
-   Under **Description**, enter `This Knowledge Base stores all documentation at NextWork.`
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.2.png)

  

-   Under **IAM permissions**, select **Create and use a new service role**.
    

> 💡 **Extra for Experts: What is a service role?**  
> A **service role** is like a permission slip that lets one AWS service (Bedrock) access another service (S3). By creating a new service role, we're giving Bedrock permission to read the documents we stored in S3.

-   Under **Choose data source**, select **Amazon S3**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.3.png)

  

-   Select **Next**.
    
-   Under **Data source name**, enter `s3-bucket-nextwork-rag-documentation`.
    
-   Make sure **This AWS account** is selected under **Data source location**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.5.png)

  

-   Select **Browse S3**.
    
    ![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.7.png)
    
      
    
-   Select your S3 bucket, which should start with `nextwork-rag-documentation-`.
    
-   Select **Choose**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.9.png)

  

-   Leave the default settings for **Parsing strategy** and **Chunking strategy**.
    

> 💡 **What is parsing?**  
> Parsing means the way data gets processed. There are two main types of parsers in Bedrock:
> 
> -   The **Default parser** extracts **only** text from common file types like PDFs, Word docs, and text files.
>     
> -   The **Foundation Model Parser** uses AI models to scan other things that might be in the files (other than text), like images, tables, headers, and complex formatting. This would be an even better parser for our documents, since our documents contain images. But, because this parser is more complex, it's slower to process and it comes with an additional cost.  
>       
>     
> 
> **💡 What is chunking?**  
> **Chunking** breaks a large text into smaller, manageable paragraphs. AI models have a limit on the amount of text they can process at once, so chunking your documents helps the chatbot process information in your Knowledge Base quickly.
> 
> By default, your documents will be chunked into 300 tokens, which is like 300 words or punctuation marks.

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.6.png)

  

-   Select **Next** to continue.
    
-   In the **Embeddings model** section, select **Select model**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.10.png)

  

-   Select **Titan Text Embeddings v2**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.9.png)

  

-   Select **Apply**.
    

> 💡 **Extra for Experts: What are embeddings?**  
> Imagine you're organizing a huge library of books. Instead of just organizing them by title, you create a special card for each book that lists all its important themes, topics, and writing style. For example:
> 
> -   A cookbook might have a card saying "cooking, Italian cuisine, pasta recipes, beginner-friendly, step-by-step instructions"
>     
> -   A mystery novel might have a card saying "crime solving, suspense, detective work, plot twists, dark atmosphere"  
>       
>     
> 
> **Embeddings is the process of creating that special "card" that captures what the text is about.** When you add new documents to your Knowledge Base:
> 
> 1.  The embeddings model reads each piece of text.
>     
> 2.  Creates a special "card" (which is actually a list of numbers) that captures what the text is about.
>     
> 3.  When someone asks a question, it creates another list of numbers i.e. makes embeddings out of the question.
>     
> 4.  Then matches the question's card with the other cards to find the closest embeddings i.e. the most similar documents.
>     
> 
>   
> This is why your chatbot can find relevant information even when the exact words don't match - it's matching the themes and meanings, just like how you could find cookbooks about "pasta" even if someone asks for "Italian food"!

**Configure the Vector Database**

-   For the **Vector store creation method**, select **Quick create a new vector store.**
    

> 💡 **Extra for Experts: Why choose Quick create?**  
> This option lets Bedrock automatically create a vector store as it creates the Knowledge Base too. You'd pick the other option if you were using a custom vector store you've already created before this.
> 
>   
> 💡 **Extra for Experts: What is a vector store?**  
> Recap: A vector store is a way to store and search for information in a way that understands the meaning of words, not just the words themselves.
> 
> In more technical terms, a vector store is a database that stores your documents' embeddings. It helps the AI find the most relevant information by matching the embeddings of your question with stored documents that share similar embeddings.

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.11.png)

  

-   Under the **Vector store** section, select **Amazon OpenSearch Serverless**.
    

> 💡 **Extra for Experts: What is Amazon OpenSearch Serverless?**  
> **Amazon OpenSearch Serverless** is a search and analytics engine, which means it helps you search, analyze, and visualize large amounts of data quickly.
> 
> In this case, we're using Amazon OpenSearch Serverless as our vector store. Once your documents are parsed, chunked and embedded, Bedrock will store the processed documents in OpenSearch.
> 
> Then, when you chat with your chatbot, Bedrock will go into the OpenSearch vector store to grab the most relevant chunks of text to answer your question.

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.12.png)

  

-   Click **Next** to review your Knowledge Base setup.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.13.png)

  

  
  

**Review and Create Knowledge Base**

Let's check your Knowledge Base setup:

Knowledge Base name: **nextwork-rag-documentation**

Data source type: **S3**

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.18.png)

  

Embeddings Model: **Titan Text Embeddings v2**

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.15.png)

  

Vector Store: **Quick create vector store** with **OpenSearch Serverless**

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.14.png)

  

-   Select **Create Knowledge Base**.
    

> 💡 **What happens now?**  
> Bedrock will set up your Knowledge Base, which can take up to 10 minutes.
> 
> Hang in there! The status of your Knowledge Base will change to **Available** once it's ready.
> 
> Lucky for us, we won't need to wait until the Knowledge Base is ready. Let's move on to the next step while it's being created.



> 🚨 **Important: By the end of TODAY, remember to delete your Knowledge Base and OpenSearch vector store**  
>   
> 
> Creating a Knowledge Base costs money. It costs about $0.10 per hour, so it's a good idea to delete your **Knowledge Base** _and_ **OpenSearch vector store** today! Make sure to 🗑️ delete both resources.
> 
>   
> **🙋‍♀️ My Knowledge Base creation failed**  
> If your Knowledge Base creation fails, scroll to the top of your console and check for the error message, which should be in a red banner.
> 
> A failed Knowledge Base creation is usually because your Knowledge Base's IAM role doesn't have proper permissions to access S3. Double-check these settings and try again. Make sure your IAM user has the `AmazonBedrockFullAccess` policy attached.
> 
> If you're still stuck, [ask the NextWork community!](https://community.nextwork.org/c/i-have-a-question/?topics=7611)

Woop woop! Nice work setting up that Knowledge Base.

As a recap, when you ask your RAG chatbot a question, it works by retrieving relevant chunks of text from your Knowledge Base. Then, it uses an AI model to generate a response.

![A simple recap of how RAG chatbots work](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/kb-flow.png)

A simple recap of how RAG chatbots work


-----

## 🤖 Step #2

### Choose an AI Model

While we're waiting for our Knowledge Base to get ready, let's get access to the AI models available in Amazon Bedrock.

These models will be the **brains** behind our chatbot - they'll convert your Knowledge Base's results into human-like text responses. Otherwise, your chatbot would just respond with raw search results from your Knowledge Base, which looks like random chunks of text taken straight from your documents. Yikes!

  
  

**In this step, you're going to:**

-   Select an **AI model** for your chatbot.
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/architecture-2.png)

  



**Navigate to the Model Access Page**

-   Still in your **Bedrock console**, open the left hand navigation menu.
    
-   Scroll down to the **Bedrock configurations** section, at the bottom of the menu.
    
-   In a new tab, open **Model access**.
    

  
  

-   We're about to request access to two AI models.
    
-   Check - do you already have access to both models? You'll see green ✅ **Access granted** labels next to both models if you already have access.  
      
    

`Titan Text Embeddings V2`

`Llama 3.3 70B Instruct`

![You'll see green `access granted` labels next to both models if you already have access.](https://learn.nextwork.org/projects/static/ai-rag-cli/step-3.4.png)

You'll see green `access granted` labels next to both models if you already have access.

  

I already have accessI need to request model access

-   Nice! This means the models are already enabled and ready to use.
    

> 💡 **Extra for Experts: What are we using these models for?**
> 
> -   **The Titan Text Embeddings V2** model converts text data into embeddings. Your Knowledge Base needs this model to process your documents and understand the meaning of the words inside them.
>     
> -   The **Llama 3.3 70B Instruct** model turns raw data into human-like text responses. When you ask your chatbot a question, the model is what translates the Knowledge Base's results into a chat message.
>     
> 
>   
> 💡 **Extra for Experts: Why are we using Llama 3.3 70B Instruct?**  
> We're going with this model because it has the perfect balance of performance and cost:
> 
> -   It's one of the most powerful open-source models available in Bedrock.
>     
> -   It's 2-3 times more affordable than other options like Claude or GPT-4 (we'll spend less than USD $0.50 to complete this project).
>     
> -   It's great at following instructions (that's what the "Instruct" part means!)
>     

Sweet! Now that model access is sorted, let's double check that your Knowledge Base has finished creating.

  
  

**Sync Your Knowledge Base**

-   Head back to the tab where you're creating your **Knowledge Base**.
    

> 🙋‍♀️ **Ooops, I've closed the Knowledge Base tab!**  
> If you've closed the Knowledge Base tab, you can open it again by going to the `Bedrock` console in a new tab and selecting **Knowledge Bases** from the left hand menu.
> 
> If your Knowledge Base is created, select your Knowledge Base from the list. If your Knowledge Base is not created, select **Create Knowledge Base** and follow the steps in Step #2!

-   You should see a green confirmation banner if the Knowledge Base is done creating. If not, wait a few minutes until it's ready!
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-4.5.png)

  

-   Find the **Data sources** section on your Knowledge Base's page.
    
-   Check the checkbox next to your data source, which should start with `s3-bucket-nextwork-rag-bedrock`.
    
-   Select **Sync** to sync your data for the first time. You'll need to do this to load your S3 documents into the Knowledge Base.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-3.2.png)

  

-   Great! Your Knowledge Base will start syncing your S3 bucket's data.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-3.3.png)

  

> **🙋‍♀️ My synchronization failed**  
> If the synchronization fails, double-check that your Knowledge Base has access to your S3 bucket. Make sure the Knowledge Base's IAM permissions include `AmazonS3ReadOnlyAccess`
> 

> 
>   
> 💡 **Extra for Experts: What happens when we synchronize data?**  
> When you synchronize data, your Knowledge Base will:
> 
> -   Read the documents from S3.
>     
> -   Process the documents to understand the meaning of the words inside them.
>     
> -   Store the processed information in the OpenSearch vector database.
>     

-   You should see a success banner like this when the sync is complete:
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-52.png)

  



Great job! You've selected an AI model and synced your data. This should mean you're ready to start conversing with your chatbot. Let's put it to the test... in your local terminal!



------

## 🏠 Step #3

### Run AWS Commands Locally

Let's learn how to talk to Bedrock using your local terminal! The **AWS Command Line Interface (CLI)** is a powerful tool that lets you manage your AWS services from your terminal.

> 💡 **Why run AWS commands locally?**  
> Running AWS commands locally means you can get answers from your chatbot directly from the terminal.
> 
> This is much faster access to your Knowledge Base than having to log into the AWS Management Console and visit the Bedrock console.
> 
> Since our goal for this project is to create an API for your chatbot, running the commands locally first will be the best way to test your chatbot before we set up the API.

  
  

**In this step, you're going to:**

-   Run a Bedrock command in your local terminal to chat with your Knowledge Base!
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/architecture-3.png)

  



> 🙋‍♀️ Heads up! This step is a bit of a 'choose your own adventure' experience, depending on whether you've already installed the AWS CLI and have access keys set up in your local terminal.
> 
> If you _do_ have CLI/access keys set up, don't hesitate to skip the questions/screenshots - the questions in this step are optional, so you can still create your personalized documentation without answering them!
> 
> If you _don't_ have CLI/access keys set up, no problem! We'll walk you through the process of setting them up, _and_ you'll get bonus pages on your documentation.

  
  

**Run Bedrock Commands**

Now, let's use AWS CLI commands to chat with our chatbot. This is where the magic happens!

-   You can choose to explore the AWS CLI documentation to find the command for this step, _or_ you can get the command straight from us.  
      
    

  ----------
  ### Explore the AWS CLI documentation

-   Head to the [AWS CLI documentation](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)
    
-   In the search bar, search for `Bedrock Knowledge Base`
    

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/new.14.png)

  

-   Wow! You might notice that there are a lot of search results.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/new.15.png)

  

-   ✋ **Pause**
    
-   If you'd like, you can explore and click through the different search results to find the right command for this step.
    
-   To narrow it down, remind yourself that you're looking for a command to **chat** with your chatbot.
    
-   For the chatbot to chat with you, it'll need to **retrieve** information from your Knowledge Base and **generate** a response.
    
-   Do any of the commands look like they'll help you do this?
    
-   Some of the commands might help you create, delete or update your Knowledge Base, but they wouldn't help you chat with your chatbot.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/new.16.png)

  

-   ✋ **Answer below**
    
-   Click into the **retrieve-and-generate** command from the search results.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/new.17.png)

  

-   Awesome, the **retrieve-and-generate** command queries a knowledge base and generates responses using an AI model. That's perfect!
    

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/new.18.png)

  

-   Read the documentation for how the command works, and see if you can put together the command for this step!
    
-   Tip: We'll make the prompt to our chatbot "What is NextWork?"
    
-   If you're stuck, you can always switch to the next tab to get the command straight from us!
  
  -----

### Get the command

-   Try running the command below in your local terminal. This command will ask your chatbot to answer the question "What is NextWork?"
    



```bash
aws bedrock-agent-runtime retrieve-and-generate \
   --input '{"text": "What is NextWork?"}' \
   --retrieve-and-generate-configuration '{
       "knowledgeBaseConfiguration": {
           "knowledgeBaseId": "your_knowledge_base_id",
           "modelArn": "your_model_arn"
  },
  "type": "KNOWLEDGE_BASE"
}'

```

---


> **💡 Extra for Experts: What does this command do?**  
> This command uses the AWS CLI to send a request to Amazon Bedrock. Let's break it down:
> 
> -   `aws bedrock-agent-runtime retrieve-and-generate`: This is the specific AWS CLI command to interact with Bedrock's agent runtime for retrieval and generation tasks (like querying a Knowledge Base).
>     
> -   `--input '{"text": "What is NextWork?"}'`: This is the question we're asking the chatbot. You can change `"What is NextWork?"` to ask different questions later.
>     
> -   `--retrieve-and-generate-configuration`: This part configures how Bedrock should handle our request.
>     
> -   `"knowledgeBaseConfiguration"`: Specifies that we want to use a Knowledge Base.
>     
> -   `"knowledgeBaseId": "knowledge_base_id"`: A placeholder for your Knowledge Base ID. **We'll replace this placeholder soon.**
>     
> -   `"modelArn": "model_arn"`: A placeholder for the AI model's ARN (Amazon Resource Name). **We'll also replace this.**
>     
> -   `"type": "KNOWLEDGE_BASE"`: Confirms that we're using a Knowledge Base.
>     

-   What does your terminal say when you run the command? Let's handle any errors you might see:  

------
      
    
### Command not found
-   Hmmmm... your terminal might not like this command. Does the terminal output say `command not found: aws`?
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/command-not-found.png)

  

> **💡 What does this response in the terminal mean?**  
> This message means that your terminal doesn't understand AWS commands - when you ran the command, it's like you were talking to your terminal in a language it doesn't know.
> 
> To fix this, we need to install the **AWS CLI** locally, so your terminal can recognize and run those commands.

**Install the AWS CLI**

The instructions for installing AWS CLI are different depending on your computer's operating system, pick the one that works for you.  
  

MacOS/Linux  

-   In your terminal, run:
    


```bash
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /

```

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-5.8.png)

  

-   Your terminal will ask for your **password.** Enter your usual password for logging into your Mac and press **Enter** on your keyboard.
    
------
### Windows
-   Open **PowerShell** and run:
    

msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi

- ----
### linux 
-  Open your terminal and run:
    

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" unzip awscliv2.zip sudo ./aws/install

-----
-   That's it, your terminal will start downloading AWS CLI straight away! It might take ~30 seconds for the download to complete - time for a stretch.
    

  
  

**Verify Your Installation**

-   Once you've installed AWS CLI (or if you already had it), verify the installation by running:
    



```bash
aws --version

```

  
You should see a version number for AWS CLI, which confirms you've installed it perfectly. It might take 10-15 seconds for the terminal to show the version number for the first time - this is normal 🤙

> **🙋‍♀️ I don't see a version number**  
> Let's troubleshoot this together!
> 
> 1.  Make sure you've run `aws --version` without any typos or extra spaces.
>     
> 2.  [Check out the AWS CLI installation page for your OS](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html). Mac and Windows instructions offer a package you could install without needing the terminal.
>     


![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-5.7.png)

  



Nice work! You've just installed AWS CLI. Try running the command again in your terminal to see if it works now:



```bash
aws bedrock-agent-runtime retrieve-and-generate \
   --input '{"text": "What is NextWork?"}' \
   --retrieve-and-generate-configuration '{
       "knowledgeBaseConfiguration": {
           "knowledgeBaseId": "your_knowledge_base_id",
           "modelArn": "your_model_arn"
  },
  "type": "KNOWLEDGE_BASE"
}'

```

> **💡 Recap: What does this command do?**  
> This command uses the AWS CLI to send a request to Amazon Bedrock. In this case, we're asking the chatbot to answer the question "What is NextWork?"

-   Wait for the command to complete - it might take 10-15 seconds.
    
-   What does the terminal response tell you now?
    
-   If you see another error - that's okay! Head back to the top of these troubleshooting tabs to find the right solution for you.






------
### Credentials/region error

Command not foundCredentials/region errorValidationExceptionOther

-   Whoops! You might see an error that says either `Unable to locate credentials` or `You must specify a region.`
    

![Unable to locate credentials](https://learn.nextwork.org/projects/static/test_project_full/screenshot-79.png)

Unable to locate credentials

  

![You must specify a region](https://learn.nextwork.org/projects/static/ai-rag-api/region-error.png)

You must specify a region

  

> **💡 Why did I get this error?**  
> You're getting this error because you're running an AWS command **from your local terminal.** You're not inside the AWS Management Console, so you're technically 'logged out' of AWS. AWS wants to authenticate you before you can run any AWS commands.
> 
> The Management Console doesn't have a way to automatically pass your credentials to the CLI, so think of this as having to log in to AWS again.

That's okay - let's set up your credentials for AWS CLI now 😎

  
  

**Configure AWS CLI**

-   Run `aws configure` in your terminal to log in. It might take ~10 seconds to load the terminal response for this command!
    
-   The terminal is now asking for your **Access Key ID.**
    

> **💡 What is an access key?**  
> Think of an access key as the AWS CLI way of logging in.
> 
> The CLI and the Management Console aren't connected, so the CLI won't know if you've already authenticated yourself by logging into the console. It needs its own way to authenticate you, and accepting an access key is one of the fastest ways to do it.
> 
>   
> 💡 **Why do we need these credentials?**  
> These credentials will let your terminal securely connect to AWS and use services like Bedrock. Without credentials, AWS won't know that your terminal commands are coming from an authorized user.
> 
> In our case, we'll need to set up credentials to run the Bedrock commands that let us chat with our chatbot!

  
  

**Set Up AWS Access Keys**

-   From your browser, head back into the [AWS Management Console.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    
-   Head to the `IAM` console.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.13.png)

  

-   Select **Users** from the left hand navigation panel.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.12.png)

  

-   Select your **IAM Admin user**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.11.png)

  

-   Select the **Security credentials** tab.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.10.png)

  

-   In the **Access keys** section, select **Create access key**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.9.png)

  

-   Select **Command Line Interface (CLI)**. Note that the same access key can be used for _all_ of the use cases on this page. AWS is just making you pick one so that it can recommend some best practices for your use case.
    

> **💡 Extra for Experts: what are the other options about?**  
> Let's break 'em down!
> 
> -   Choose **Local code** if you're building an application in your local computer, and need the access key to connect your app with AWS services.
>     
> -   Choose **Application running on an AWS compute service** if you're building an application that's running on an AWS compute service like EC2 or Lambda, and need the access key to connect your app with AWS services.
>     
> -   Choose **Third-party service** if you're running an application from an external company (i.e. it wasn't built by yourself or AWS), but requires access to your AWS environment. For example, Crowdstrike is a third party security service that requires access to your AWS environment to protect them in real time!
>     
> -   Choose **Application running outside AWS** if you're running an application built by yourself but hosted on a physical server or another cloud platform, and you need to integrate it with AWS services.
>     

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.8.png)

  

-   Check the acknowledgement checkbox at the bottom of the page.
    

> **💡 Why is there an acknowledgement checkbox?**  
> AWS usually recommends using another service called **IAM Identity Center** instead of access keys for programmatic access (i.e. access over the terminal), because it's newer and more secure.
> 
> This is especially true for larger teams, where you might need to manage CLI access for multiple people. We won't need it for smaller projects like this one!

-   Select **Next**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.7.png)

  

-   For the **Description tag value**, enter a short name:
    



```text
nextwork-rag-bedrock-project

```

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.6.png)

  

-   Select **Create access key**.
    
-   **STAY ON THIS PAGE ✋**
    
-   Well done! Your access key is created, and AWS has set you up with an **Access key** and **Secret access key.**
    

> 💡**What is the secret access key?**  
> The secret access key is like the password that pairs with your access key (your username). You need both to 'log in' to AWS over the CLI in your terminal.
> 
> **Secret** is a key word here - anyone who has it can access your AWS account, so make sure to keep this away from anyone else!

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.5.png)

  

-   🚨 **Select Download .csv file.** This is the ONLY time you can see your Secret Access Key. Downloading the .csv file is how you can keep these credentials! We'll make sure to delete everything at the end of this project.
    

**🙋‍♀️ Uh oh, I've already left this page**  
Ah, classic! Don't worry, you'll just need to delete the key you've set up and create another one. for help!deletion step Don't forget to stay on the page the second time round. If you're stuck while deleting your access key, you can jump to our



Access keys created - nice work!

Shall we try configure these credentials in your terminal? 🔑

  
  

**Configure the AWS CLI**

-   Copy your IAM user's **Access Key ID**
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.4.png)

  

-   Head back to your local terminal.
    
-   Are you ready to enter your **Access keys** details now?
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.14.png)

  

-   Paste the Access Key ID into your terminal, and press **Enter** on your keyboard.
    
-   Let's do the same for the **AWS Secret Access Key!**
    
-   Copy your IAM user's **Secret Access Key** and paste it in your terminal.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.2.png)

  

-   Enter your **AWS region code** i.e. `us-east-2` for Ohio, since that's the region where we've set up our Knowledge Base.
    
-   We don't have a default output format, so we can leave that empty. Press **Enter**.
    

> 💡 **Extra for Experts: What is a default output format?**  
> In just a second, you'll be running a few CLI commands in your local terminal. The **default output format** is how the CLI will display the results of your commands.
> 
> Options for your output format options are...
> 
> -   `json`, which is the default if you're not using another option.
>     
> -   `text` for plain text.
>     
> -   `table` for an formatted table.
>     
> -   `yaml`, which is a format for writing data in a way that is easy for people to read and write.
>     

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-6.3.png)

  



  
  

**Run Your Bedrock Command Again**

Awesome work! You've just set up your credentials over the CLI. This means you can now use Bedrock over your local terminal.

-   Try running the Bedrock command again in your terminal:
    


```bash
aws bedrock-agent-runtime retrieve-and-generate \
   --input '{"text": "What is NextWork?"}' \
   --retrieve-and-generate-configuration '{
       "knowledgeBaseConfiguration": {
           "knowledgeBaseId": "your_knowledge_base_id",
           "modelArn": "your_model_arn"
  },
  "type": "KNOWLEDGE_BASE"
}'

```

> **💡 Recap: What does this command do?**  
> This command uses the AWS CLI to send a request to Amazon Bedrock. In this case, we're asking the chatbot to answer the question "What is NextWork?"

-   Wait for the command to complete - it might take 10-15 seconds.
    
-   What does the terminal response tell you now?
    
-   If you see another error - that's okay! Head back to the top of these troubleshooting tabs to find the right solution for you.


------
### ValidationException

-   Ooooops! You might see a **ValidationException** error in your terminal.
    
-   This error tells us that you're missing the knowledge_base_id and model_arn placeholder values in your command.
    
-   Good news though! This response tells us that your AWS credentials are actually working, so you can **move on to the next step**.
    
-   Head straight to 🔍 Step #4: Finding Your Knowledge Base and Model IDs. Let's find the values we need to replace the placeholders in our command!
-----
## Other

-   If you've run into an **authentication** error (e.g., IncompleteSignatureException, UnrecognizedClientException, InvalidClientTokenId, or AccessDenied), this means you'll need to set up your CLI credentials in the terminal. Head to the Credentials or region error tab to learn how to do this!
    
    -   Special note: the **UnrecognizedClientException** error is a common one, it also triggers if your Secret Access Key has a special character like + or \. If this is the case, try copying the Secret Access Key from your .csv file, or create a new access key without special characters.
        

  

-   If your Knowledge Base responds with "Sorry, I am unable to assist you with this request", check whether you've **synced** your Knowledge Base. If your Knowledge Base is not synced with your source data in the S3 bucket, it doesn't have any data to retrieve from!

-----


## 🔍 Step #4

### Finding Your Knowledge Base and Model IDs

Now that we've tried running our first Bedrock command, let's find the values we need to make it work! We'll need to find your Knowledge Base ID and Model ARN.

  
  

**In this step, you're going to:**

-   Find your **Knowledge Base ID** and **Model ARN**
    
-   Update your Bedrock command with these values
    
-   Run your first successful chat with your Knowledge Base!
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/architecture-4.png)

  



  
  

**Edit the Retrieve-and-Generate Command**

-   To replace the placeholders, you'll need to edit the **retrieve-and-generate** command.
    
-   Copy the bash command below. This command asks your chatbot to answer the question "What is NextWork?"
    



```bash
aws bedrock-agent-runtime retrieve-and-generate \
   --input '{"text": "What is NextWork?"}' \
   --retrieve-and-generate-configuration '{
       "knowledgeBaseConfiguration": {
           "knowledgeBaseId": "your_knowledge_base_id",
           "modelArn": "your_model_arn"
  },
  "type": "KNOWLEDGE_BASE"
}'

```

-   Paste the command into a separate text editor. This can be **TextEdit** (MacOS), **Notepad** (Windows), or any other text editor you have on your computer.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.14.png)

  

Now that you have a text file to edit your command, let's search for the **Knowledge Base ID** and **Model ARN.**



  
  

**Find Your Knowledge Base ID**

-   In a new tab, open the `Bedrock` console again.
    
-   Select **Knowledge Bases** from the left hand menu.
    
-   Select your Knowledge Base.
    
-   Find the **Knowledge Base ID** from the overview panel.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.11.png)

  

-   Copy the **Knowledge Base ID**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.12.png)

  

-   Head to the text file where you saved the **retrieve-and-generate** command.
    
-   Paste the Knowledge Base ID into the command, replacing the `your_knowledge_base_id` placeholder.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.15.png)

  

  
  

**Find Your Model ARN**

Finding the model ARN is a bit more tricky - it's not information you can find over the Management Console! This is because model ARNs are usually handled in the background when you're using the Bedrock console.

You'll need to **run another command** in your local terminal to find the model ARN.  


----
### i want to find the command myself
-   Lucky for us, this time there's an existing user guide on finding the model ARN!
    
-   Search How to find the ModelARN of a Bedrock model
    ![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/new.19.png)

-   Aha! There's a search result on [getting information about Bedrock models.](https://docs.aws.amazon.com/bedrock/latest/userguide/models-get-info.html)
    
-   Click into the search result.
    
-   Do you think you can put together the command based on the guidance here?
    

-   Tip: Make sure you're looking at the **AWS CLI** instructions on the page!
    
-   The command to get the model ARN is aws bedrock get-foundation-model --model-identifier <your-model-id>
    
-   You'll need to replace <your-model-id> with the ID of your AI model!
    

-   In the CloudShell terminal, run the following command to find the ARN of your model.
    

aws bedrock get-foundation-model --model-identifier <your-model-id>

> 💡 **Damn it, the response is empty!**  
> That's okay! It's because you don't know your AI model's ID yet, which is <your-model-id> in the command above.
> 
> We'll need to find your AI model's ID first, and put it into this command. _Then_ we'll get the model's ARN.
> 
> Yup - it's an extra step - but it's a good way to practice your CLI skills! You've got this.

-   You can choose to explore the Bedrock console to find the model ID, _or_ you can get the completed command straight from us.
----
### give me the command
-   In the CloudShell terminal, run the following command to find the ARN of your model.
    

aws bedrock get-foundation-model --model-identifier <your-model-id>

> 💡 **Damn it, the response is empty!**  
> That's okay! It's because you don't know your AI model's ID yet, which is <your-model-id> in the command above.
> 
> We'll need to find your AI model's ID first, and put it into this command. _Then_ we'll get the model's ARN.
> 
> Yup - it's an extra step - but it's a good way to practice your CLI skills! You've got this.
----

You can choose to explore the Bedrock console to find the model ID, _or_ you can get the completed command straight from us.

----

---------
### I want to find the Model ID




-   In a new tab, open the `Bedrock` console again.
    
-   Select **Model catalog** from the left hand menu.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.4.png)

  

-   Welcome to the **Model Catalog!** This is where you can find all the models available in Bedrock, and find metadata about each model - like the Model ID.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.24.png)

  

-   Find the `Llama 3.3 70B Instruct` model.
    

> 💡 **Extra for Experts: Why are we using Llama 3.3 70B Instruct?**  
> We chose this model because:
> 
> -   It's one of the most powerful open-source models available in Bedrock
>     
> -   It's 2-3 times more affordable than other options like Claude or GPT-4
>     
> -   It's great at following instructions (that's what the "Instruct" part means!)
>     
> 
>   
> While not _the_ most powerful model in Bedrock, it gives us a great balance of performance and cost for learning and development.

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.25.png)

  

-   Click into the model's name.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.26.png)

  

-   Copy the **Model ID** from the details panel (it will look like `meta.llama3-3-70b-instruct-v1`).
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.5.png)

  

-   Head back to your **local terminal**.
    
-   Run the ModelARN command, this time replacing the `<your-model-id>` placeholder with the **Model ID** you copied earlier.
    

> 🙋‍♀️ **I need the ModelArn command again**  
> Here is the command:
> 
> 
> ```bash
> aws bedrock get-foundation-model --model-identifier <your-model-id>
> 
> ```

-   Press **Enter** on your keyboard to run the command!
    

> 🙋‍♀️ **I got a ValidationException error!**  
> That's okay! Your terminal might say `the provided model identifier is invalid.` This happens when you've configured CLI credentials in your terminal, but haven't configured it to a region with the Llama AI model you're using.
> 
> To fix this, run `aws configure` and make sure you set up your credentials for the `us-east-2` region.

-   You should see the terminal return the model ARN.
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/modelarn.png)

  

-   Copy the model ARN.
    
-   Head to the text file that you copied the retrieve-and-generate command to.
    
-   Paste the model ARN into the command, replacing the `your_model_arn` placeholder.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.16.png)

  

**Run the completed command**

-   Now, copy the completed Bedrock command from your text file.
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-78.png)

  

-   Run the command in your **local** terminal. If your terminal is still showing the ModelARN command, you can press `Ctrl+C` or `q` to stop it.
    
-   Wait for the command to complete. The first time you run it, it might take 10-15 seconds.
    

  
  

-   What was the response in the terminal?
    
-   Yayy!! You should see a response in your terminal!
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-7.1.png)

  



-   **🎉 Congratulations! You've just accessed Bedrock via the AWS CLI**
    
-   Press `q` on your keyboard to finish reading the response in your terminal.
    

> 💡 **Recap: Why is it important to use commands?**  
> Using commands is a really powerful way to interact with your chatbot. It's faster, more flexible, and gives you more control over your chatbot. You now have access to your chatbot from your local terminal!
> 
> Our end goal is to create an API for your chatbot. Running this command helps you test your programatic chatbot set up - your access keys, model ARN, and knowledge base ID are confirmed working now!
-----

## 🕸️ Step #5

### Set Up Your API

Now that we have our chatbot working through the CLI, let's make it even more powerful by making it accessible through an API!

Think about popular AI tools like ChatGPT - they don't just work through a command line. They have beautiful web interfaces, mobile apps, and can even be integrated into other tools like Slack or Microsoft Teams. How do they do this? Through APIs!

By creating an API for your chatbot, you'll open up endless possibilities for how others can interact with it. Want to build a sleek web interface? Add your chatbot to a mobile app? Or maybe integrate it with your favorite messaging platform? With an API, all of this becomes possible!

> 💡 **What is an API?**  
> Think of an API (Application Programming Interface) like a restaurant menu - it lists all the ways other applications can interact with your service. Just like how a menu tells customers what food they can order, an API tells other applications what requests they can make to your chatbot.

**In this step, you're going to:**

-   Set up a Python development environment
    
-   Create an API.
    
-   Connect your API to Amazon Bedrock
    
-   Test your chatbot through web requests
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/architecture-5.png)

  



Building an API from scratch can be complex - you need to handle web requests, manage connections to AWS, implement error handling, and more.

Luckily, we've prepared a starter API for you! We'll use a pre-built GitHub repository that has all the basic API code ready to go. Then, you'll customize it with your own Knowledge Base and AI model settings.

  
  

**Review the API Code**

Let's understand what's in our pre-built API's code before we run it!

-   Open the API's GitHub repository in your browser: [https://github.com/NatNextWork1/nextwork-rag-api](https://github.com/NatNextWork1/nextwork-rag-api).
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-101.png)

  

Notice that there are three separate files in the repository:

-   **main.py**, which is the main file for our API.
    
-   **requirements.txt**, which lists the dependencies for our project.
    
-   **secret_mission.py**, which (you guessed it) is a secret file that we'll use in this project's 💎 Secret Mission
    

> 💡 **What's does the code do?**  
> Our code creates an API that:
> 
> -   Creates a connection to Amazon Bedrock.
>     
> -   Sets up API endpoints that applications can call
>     
> -   Handles sending questions to your chatbot and returning responses.
>     
> 
>   
> 💡 **What is FastAPI?**  
> FastAPI is a modern web framework for building APIs with Python. It's:
> 
> -   **Fast**: One of the fastest Python frameworks available
>     
> -   **Easy to use**: Automatic API documentation
>     
> -   **Modern**: Built for modern Python features
>     
> -   **Production-ready**: Used by companies like Uber and Netflix
>     

-   Select the **main.py** file to open it in your browser.
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-105.png)

  

-   Welcome to your API's main file! This means this file defines how your API works.
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-106.png)

  

**📝 Understanding main.py** This Python file is structured into three main sections:  
  

1. Imports2. Environment Variables3. API Endpoints

**Environment variables:** These lines load environment variables, which are variables that you'll define in your local terminal:

-   `AWS_REGION`: The AWS region where your resources live (for us, it's us-east-2)
    
-   `KNOWLEDGE_BASE_ID`: The ID of your Bedrock Knowledge Base.
    
-   `MODEL_ARN`: Your AI model's ARN. You might remember grabbing this when we prepared our Bedrock command in #Step 4.
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-109.png)

  



**Clone the Repository**

-   Head back to the main page of the repository.
    
-   Select the **Code** button.
    
-   Copy the **HTTPS URL** of the repository.
    

> **💡 Why are we copying the HTTPS URL?**  
> In GitHub, the HTTPS URL is like an address for the repository. We'll use it to tell our local machine where to find the repository we want to clone.  
>   
> 
> **💡 What does cloning a repository mean?**  
> Cloning a repository means we're downloading a copy of the repository to our local machine. This lets us run the code on our own computer.

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-102.png)

  

-   In your local terminal, let's navigate to your Documents directory. This gets us ready to clone the repository in your Documents folder:

#### MacOS/Linux



```bash
cd ~/Documents

```

-   Run this command to clone the repository - don't forget to replace the [HTTPS-URL] placeholder with the URL you copied earlier:
    



```bash
git clone [HTTPS-URL]

```

> 🙋‍♀️ **Don't have Git installed?**  
> If you see an error that Git is `not available`, head to the [Git website](https://git-scm.com/downloads) to download and install Git for your operating system.

**Great start!** You've just downloaded your API's code.

  
  

**Navigate to the Project Directory**

-   After cloning the repository, navigate into the project directory by running:  
      
    

MacOS/Linux



```bash
cd nextwork-rag-api

```

-   Check that you're in the correct directory by running:
    



```bash
pwd

```

-   This command prints out your current directory. If the path ends with `nextwork-rag-api`, it means you're in the right place! If not, you can try navigating to your project directory by running `cd ~/Documents/nextwork-rag-api`
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-103.png)

  

-   Next, let's list the files in the directory to see the project structure:
    



```bash
ls

```

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-104.png)

  

This confirms that we've correctly cloned three files into our project directory - `main.py`, `requirements.txt`, and `secret_mission.py`

**Create Your Virtual Environment**

-   Still in your terminal and project directory, let's create a new virtual environment:
    


```bash
python3 -m venv venv

```

> 💡 **Extra for Experts: What is a virtual environment?**  
> A **virtual environment** is a special folder on your computer that contains its own copy of:
> 
> -   Python itself (like Python 3.11).
>     
> -   Package managers (like pip or UV).
>     
> -   Any extra packages your project needs.
>     
> 
>   
> Think of it like a separate workspace for each of your coding projects. Just like how you might have different folders for different school subjects, each virtual environment is an isolated folder that keeps all the tools and packages for a specific project in one place.
> 
> The best part? Everything in this environment is separate and temporary. When you delete the environment folder, all the packages you installed are removed too, keeping your computer tidy.
> 
> Without a virtual environment, you might run into problems like:
> 
> -   Package version conflicts between projects
>     
> -   Difficulty tracking project dependencies
>     
> -   Messy Python installations on your computer
>     

-   What do you see in your terminal?  
      
    

Nothing...

-   Your terminal won't show anything straight away, but an empty response like this means your virtual environment has been created with no issues:
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/capture.png)

  

-   Activate your virtual environment:  
      
    

MacOS/Linux



```bash
source venv/bin/activate

```

> 🎯 **Nice work!** Your virtual environment is ready. You'll see `(venv)` at the start of your command prompt to show it's active.

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-111.png)

  

-   To verify that your virtual environment is activated, run:
    



```bash
echo $VIRTUAL_ENV

```

-   You should see the path to your virtual environment printed out. This confirms your virtual environment is active - if it wasn't active, this command would return nothing!
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-112.png)

  

  
  

-   Now let's try running the API:  
      
    



```bash
python3 -m uvicorn main:app --reload

```

> 💡 **What does this command do?**  
> This command starts up your API server! When you run this command, your API will be available for use at `http://127.0.0.1:8000` - your computer's local address.
> 
> In simpler terms, when you run this command, you're like saying "Python, please start a web server that will run my API code, and make sure to refresh it whenever I make changes."
> 
>   
> 💡 **Extra for Experts: Let's break down each part of the command:**
> 
> -   **python3:** This tells your computer "Hey, use Python version 3 to run something" - just like how you might use Microsoft Word to open a .docx file
>     
> -   **-m uvicorn:** This says "Use the uvicorn program", and Uvicorn is a web server that's responsible for passing requests from your browser to your API code.
>     
> -   **main:app:** This tells uvicorn where to find your API code. The `main` refers to your main.py file, and app refers to the `@app` sections inside that file
>     
> -   **--reload:** This is like an "auto-refresh" mode. Later on, when you make changes to your code, the server will automatically restart so you don't have to manually stop and start it.
>     

-   Uh oh! You might see an error like this:
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-113.png)

  

> **🙋‍♀️ What's this error?**  
> You might see an error like `ModuleNotFoundError: No module named uvicorn` if your virtual environment doesn't actually have Uvicorn installed yet!

  
  

**Install Requirements**

Other than Uvicorn, there are other packages that you'll need to run your API. These packages are all listed in the `requirements.txt` file in your project directory.

-   To see what packages are being installed, you can view the contents of the `requirements.txt` file:
    



```bash
cat requirements.txt

```

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-114.png)

  

> 💡 **What's in requirements.txt?**  
> This file lists all the Python packages our API needs:
> 
> -   `fastapi`: The web framework for building our API.
>     
> -   `uvicorn`: A server that actually runs your API and turns things you enter into your browser into API requests.
>     
> -   `boto3`: AWS SDK for Python, which helps us talk to Bedrock.
>     
> -   `python-dotenv`: Loads environment variables from a file.
>     
> 
>   
> 💡 **Extra for Experts: Why do we need a requirements.txt file?**  
> The `requirements.txt` file is a standard way to manage Python project dependencies:
> 
> -   Makes it easy to share projects with others.
>     
> -   The version numbers (like `==0.115.8`) make sure everyone is installing the same version of each package. This helps prevent unexpected issues that might come from using different versions.
>     

-   Install the required Python packages for the API by running:
    



```bash
pip3 install -r requirements.txt

```

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-115.png)

  

-   Now let's check that the packages are installed by listing the installed packages in your virtual environment:
    



```bash
pip3 list

```

-   You should see `fastapi`, `boto3`, `python-dotenv`, and `uvicorn` in the list.
    

> 💡 **Woah! Why am I seeing a lot of other packages?**  
> This is because we're installing all the packages listed in `requirements.txt` _and_ the dependencies of each package.
> 
> When you install Python packages, they often come with their own dependencies - other packages they need to work properly.
> 
> Think of it like buying a new computer - aside from the computer (the main package) itself, you might also need to get a charger (dependency) for it to work!
> 
> For example, `boto3`, one of our packages, requires `botocore`, `jmespath`, and `s3transfer` to actually connect to AWS.

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-117.png)

  



  
  

**Run the API**

-   Start running the API again by running:
    



```bash
python3 -m uvicorn main:app --reload

```

-   Yay, no more errors! You should see a message like `Uvicorn running on http://127.0.0.1:8000` in your terminal.
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-119.png)

  

Let's check out the API in action!

  
  

**Visit the Root Endpoint**

-   Open your web browser and go to the URL provided in the terminal output, usually [http://127.0.0.1:8000](http://127.0.0.1:8000/).
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-120.png)

  

-   You should see the message `{"message": "Welcome to your RAG chatbot API"}` in your browser. This confirms that your API is running correctly and the **root endpoint** is working.
    

> 💡 **Recap: What is the root endpoint?**  
> The root endpoint is the main page of your API. It's like the home page of a website - it's the first thing people see when they visit your API.
> 
> We created this endpoint by adding `@app.get("/")` to our `main.py` file.
> 
> ![](https://learn.nextwork.org/projects/static/ai-rag-api/screenshot-121.png)
> 
>   




-------
## ❓ Step #6

### Test the Query Endpoint

Now that our API is up and running, let's test the most important endpoint - the **query** endpoint!

This is where we'll see our chatbot API in action, taking questions from users and providing answers based on our Knowledge Base.

> 💡 **What is the `query` endpoint?**  
> This endpoint is defined in `main.py` using `@app.get("/bedrock/query")`.
> 
> ![](https://learn.nextwork.org/projects/static/ai-rag-api/screenshot-122.png)
> 
>   
> 
> It's designed to take a query text as input and send it to your Bedrock Knowledge Base. The `?text=What%20is%20NextWork` part of the URL is how we pass the question "What is NextWork?" to the API i.e. your chatbot.
> 
> P.S. `%20` is the URL-encoding for an empty space!

**In this step, you're going to:**

-   Ask your chatbot a question over the API (using the `query` endpoint)
    
-   Troubleshoot errors in your API setup.
    


**Visit the Query Endpoint**

-   Now, let's test the `query` endpoint in your API.
    
-   Update the URL in your browser to: [http://127.0.0.1:8000/bedrock/query?text=What%20is%20NextWork](http://127.0.0.1:8000/bedrock/query?text=What%20is%20NextWork). This asks your chatbot "What is NextWork?"
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-123.png)

  

-   Whoops!
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-125.png)

  

-   If you see an error message for `Invalid type for parameter` related to your `knowledgeBaseId` or `modelArn`, it means that your API isn't correctly configured with your Knowledge Base ID and Model ARN.
    

  
  

Let's investigate this now! Fixing this error is our final step before we can see our working API - you're sooooooo close 😮‍💨



  
  

**Troubleshoot the Error**

-   Let's visit [the main.py file in the API's GitHub repository](https://github.com/NatNextWork1/nextwork-rag-api/blob/main/main.py) to find out more about this ~mysterious~ error. Where is our API asking for our Knowledge Base ID and Model ARN?
    
-   Voila! We can see that our API is asking for our Knowledge Base ID and Model ARN between lines 11 and 14 of `main.py`
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-128.png)

  

> 💡 **How do we know that these commands are asking for my Knowledge Base ID and Model ARN?**  
>   
> 
> These lines are using the `os` package (one of the packages we installed earlier) to **import** your `KNOWLEDGE_BASE_ID` and `MODEL_ARN` from your computer.
> 
> For these lines to work, we need to set your `KNOWLEDGE_BASE_ID` and `MODEL_ARN` as **environment variables** on your computer.
> 
>   
> 💡 **What are environment variables?**  
> Think of environment variables as a secret configuration file.
> 
> Writing sensitive information (like your Knowledge Base's ID) directly in your code is a bad practice - imagine if you end up storing that code file publicly in a GitHub repository! Using environment variables are a better practice. You store the value of your `KNOWLEDGE_BASE_ID` and `MODEL_ARN` separately in an environment file.
> 
> Then, the `os` package can read these values from the environment file when your API runs.

-   Why does our API need to import these environment variables anyway? Let's scroll down `main.py` in the GitHub repository...
    
-   Aha! Do you see your API's `query` endpoint asking for your Knowledge Base ID and Model ARN?
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-126.png)

  

-   Just like the Bedrock command you ran earlier, your API needs to know your `KNOWLEDGE_BASE_ID` and `MODEL_ARN` to send requests to Bedrock.
    

![Recap: You needed to pass specific values for knowledge_base_id and model_arn in the CLI too](https://learn.nextwork.org/projects/static/test_project_full/screenshot-60.png)

Recap: You needed to pass specific values for knowledge_base_id and model_arn in the CLI too

  

-   To fix the error in our API, we need to set our `KNOWLEDGE_BASE_ID` and `MODEL_ARN` as environment variables.
    



  
  

**Add Environment Variables**

> 💡 **What are environment variables?**  
> Environment variables are like secret settings for your application. Think of them like a configuration file that your application reads when it starts up!
> 
> -   They keep sensitive information (like API keys) out of your code.
>     
> -   They make it easy to change settings without modifying code (for example, every NextWork student can use the same `main.py` file and configure it to use their own Knowledge Base and Model ARN using environment variables).
>     

-   First, stop the running API by pressing `Ctrl+C` in your terminal.
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-129.png)

  

-   Create a new `.env` file in your project directory:
    

> 💡 **What is the `.env` file?**  
> The `.env` file is a text file that contains environment variables for your application. It's used to store sensitive information like API keys and other configuration settings.

MacOS/Linux

-   Open your terminal and run:
    



```bash
touch .env
nano .env

```

> 💡 **What do these commands do?**
> 
> -   `touch .env` creates a new empty file called `.env`
>     
> -   `nano .env` opens the file in a text editor called nano
>     
> 
>   
> 💡 **What is nano?**  
> Nano is a simple text editor that lives in your terminal.
> 
> It's a popular choice for creating and editing text files, because you won't need to open a separate window or application to edit your files.

-   Copy the following template into your `.env` file - this is how we'll tell our API the environment values we want it to use:
    



```text
AWS_REGION=us-east-2
KNOWLEDGE_BASE_ID=<your_knowledge_base_id>
MODEL_ARN=<your_model_arn>

```

> 💡 **What are these environment variables?**
> 
> -   `AWS_REGION`: The AWS region where your resources live (for us, it's us-east-2)
>     
> -   `KNOWLEDGE_BASE_ID`: The ID of your Bedrock Knowledge Base
>     
> -   `MODEL_ARN`: The Amazon Resource Name of your AI model
>     

-   Replace the placeholders with your actual values:
    
    -   `<your_knowledge_base_id>`: Your Knowledge Base ID, which should be in your full command text file.
        
    -   `<your_model_arn>`: Your Model ARN, which should be in your full command text file.
        
-   Don't forget - you've already defined your knowledge_base_id and model_arn in your text file:
    
-   In your text file, copy the value for `knowledgeBaseId`
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-133.png)

  

-   Paste it into the `.env` file as `KNOWLEDGE_BASE_ID`.
    
-   In your text file, copy the value for `modelArn`
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-134.png)

  

-   Paste it into the `.env` file as `MODEL_ARN`.
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-136.png)

  

-   Save the file - the instructions for this depend on your operating system:  
      
    

MacOS/Linux

-   In nano:
    
    -   Press `Ctrl + X`
        
    -   Press `Y` to confirm.
        
    -   Press `Enter` to save.
        

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-130.png)

  

**Verify Environment Variables**

-   Check that your `.env` file was created correctly:
    



```bash
cat .env

```

> 🙋‍♀️ **I don't see my environment variables!**  
> If you don't see your environment variables:
> 
> 1.  Make sure you saved the `.env` file in the correct location (your project directory)
>     
> 2.  Check that the file name is exactly `.env` (including the dot)
>     
> 3.  Try creating the file again using a different text editor
>     

![](https://learn.nextwork.org/projects/static/ai-rag-api/nano.png)

  

  
  

**Run Your API Again**

-   Run the FastAPI server with your new environment variables:
    



```bash
python3 -m uvicorn main:app --reload

```

-   WOOO - you should see your API running again. We're so close to seeing your chatbot in action!
    

> 🙋‍♀️ **I got an error!**  
> If you see an error:
> 
> -   `ModuleNotFoundError`: Run `pip3 install -r requirements.txt` again.
>     
> -   `ImportError`: Make sure your virtual environment is activated.
>     
> -   `Connection refused`: Check that your AWS credentials are correct.
>     
> -   Make sure all environment variables in your `.env` file are set correctly!
>     
> 
>   
  
  

**Test Your API**

-   Visit the query endpoint in your browser again. As a reminder, this URL asks your chatbot "What is NextWork?": [http://127.0.0.1:8000/bedrock/query?text=What%20is%20NextWork](http://127.0.0.1:8000/bedrock/query?text=What%20is%20NextWork).
    

> 💡 **Recap: Understanding the URL**
> 
> -   `http://127.0.0.1:8000`: Your local server address
>     
> -   `/bedrock/query`: The endpoint for querying your chatbot
>     
> -   `?text=What%20is%20NextWork`: Your question (%20 represents a space)
>     

-   This time, you should see a successful response from your chatbot. Amaaaaazing!
    

> 🙋‍♀️ **Getting an error?**  
> If you see an error message, check that:
> 
> -   Your FastAPI server is still running in the terminal
>     
> -   Your `.env` file contains the correct credentials
>     
> -   Your Knowledge Base ID and Model ARN are correct
>     
> 
> Still having issues? Make sure your AWS credentials have permission to access Bedrock!

**🎉 you've built an API for your Bedrock RAG chatbot!**

You can now query your chatbot through web requests.

Once you learn how to make your API publicly accessible (we learn how to do this in the [APIs with Lambda + API Gateway project]() any application can chat with your Bedrock chatbot by sending requests to your API.

This opens up endless possibilities - you could build a chat interface, integrate it with Slack, or even create a mobile app that uses your chatbot. You've come a long way, great job!

--------

## 🗑️ Before you go

### Delete your resources

Now that we've built and tested our chatbot, it's time to clean up the resources we created. This is important to avoid getting charged for unused resources.

  
  

**Resources to delete:**

Delete the **Bedrock Knowledge Base**.

Delete the **S3 bucket**.

Delete the **IAM access key**.

Delete the **OpenSearch vector store**.


-----
  
🎉 Mission Accomplished

### 

That's a wrap!

Nice work! 🤖 You've just built a powerful RAG chatbot API using Amazon Bedrock.

![](https://learn.nextwork.org/projects/static/ai-rag-api/architecture-complete.png)

  

**You've learned how to:**

-   🚀 Set up an S3 bucket to store your documents.
    
-   🧠 Create and configure a Knowledge Base in Amazon Bedrock.
    
-   🔑 Request access to and use AI models in Bedrock.
    
-   💻 Access Bedrock using the AWS CLI.
    
-   🕸️ Build an API to query your chatbot.

------