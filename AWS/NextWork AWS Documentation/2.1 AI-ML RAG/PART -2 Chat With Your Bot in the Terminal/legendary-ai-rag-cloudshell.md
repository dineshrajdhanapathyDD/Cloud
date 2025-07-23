<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Chat With Your Bot in the Terminal

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-rag-cloudshell)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---



# Chat With Your Bot in the Terminal

Build a RAG chatbot that gives you answers straight from the terminal!

## Summary

Welcome to part TWO of our RAG chatbot series!

In this project, you'll build a RAG chatbot that can answer questions about your documents - **over the terminal!** 🤖

Say goodbye to relying on the AWS Management Console - you'll learn how to chat with your chatbot over AWS Command Line Interface (CLI) commands. This is a big step towards learning how to integrate your chatbot into your own applications!

This project is great for building your skills towards roles like **Backend Developer** and **DevOps Engineer**, where you're working with tools over the command line.

### In this project, get ready to...

🧠 Set up your chatbot in **Amazon Bedrock.**☁️ Talk to your chatbot using commands in **AWS CloudShell.**💎 Manage your entire Bedrock **Knowledge Base** from the terminal.💎 Go beyond your chatbot - talk with **AI models** directly via the CloudShell terminal.

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/architecture-complete1.png)


----
👀 Step #0

### 

Before we start Step #1...

In our [first RAG chatbot project](https://link.nextwork.org/projects/ai-rag-bedrock?utm_source=project-app), you would've learnt how to set up a RAG chatbot in the AWS Management Console.

![A simple recap of how RAG chatbots work](https://learn.nextwork.org/projects/static/ai-rag-cli/rag-chatbot.png)

A simple recap of how RAG chatbots work

  

By the end of **this** project, you'll learn how to use that chatbot over the terminal!

Whether you're coding, debugging, or just need quick information from your documents, your RAG chatbot will be right there in your terminal, ready to answer questions instantly.

> 💡 **What's the point of chatting with our chatbot over the command line?**  
> While running commands might seem a little intimidating at first, many DevOps and Backend Engineers choose it over a web app or console!
> 
> Here's why:
> 
> -   Engineers can run commands much **faster** than clicking through a web app.
>     
> -   Engineers can script commands to **automate** repetitive tasks.
>     
> -   Engineers usually get **more control** over what they're doing when they're using a command.
>     
> 
>   
> You'll see this in action soon - interacting with Bedrock over the command line is faster and gives you more configuration options.

![What you can do in the terminal by the end of this project](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/new.9.png)

What you can do in the terminal by the end of this project

  

> 💡 P.S. You **don't** need to do our [first RAG chatbot project](https://link.nextwork.org/projects/ai-rag-bedrock?utm_source=project-app) to start this one, but we highly recommend it! You'd get to chat with your RAG chatbot in a visual interface, and build a much stronger understanding of how to set up a RAG chatbot in Bedrock.
> 
> We'll still explain how to set up your chatbot step-by-step in this project - we'll just move slightly faster, and talk with the chatbot over the terminal instead.

**🤔 How in the world are we going to build this?**

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/architecture-complete-grey.png)

  

**First, we'll set up our chatbot:**

-   In 🪣 Step #1.**S3**, we'll store the information we want our chatbot to know in
    
-   In 🧠 Step #2.**Knowledge Base**, we'll help our chatbot understand the information with a Bedrock
    
-   In 🤖 Step #3 in Bedrock that will help our chatbot communicate what it's learned.**AI models**, we'll pick
    

  
  

**Then, we'll chat with our chatbot over the terminal:**

-   In ☁️ Step #4, an AWS service that lets you run commands in your terminal.**AWS CloudShell**, we'll open up
    
-   In 🔍 Step #5, we'll run the commands to chat with our chatbot over the terminal.
    

---

## 🪣 Step #1

### Setting Up S3 and Data

Before we can create a RAG chatbot, we need to set up the information it needs to know! That's where Amazon S3 comes in - it's going to be the home for all the documents and information that your chatbot will learn from.

  
  

**In this step, you're going to:**

-   Create an S3 bucket to store your chatbot's training materials.
    
-   Upload documents that your chatbot will learn from.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/architecture-1.0.png)

  



  
  

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

-   Under **Object Ownership**, leave **ACLs disabled (recommended)** selected.
    

> 💡 **Extra for Experts: Why leave ACLs disabled?**  
> This makes managing permissions simpler. The bucket owner gets full control, which helps prevent accidental permission issues.

-   Under **Block Public Access settings**, make sure **Block all public access** is checked (default setting).
    

> 💡 **Extra for Experts: Why block public access?**  
> This keeps your data secure by ensuring only authorized users and services can access your bucket. Since your chatbot's training data doesn't need to be publicly accessible, this is the safest option.

-   Leave the default encryption settings.
    

> 💡 **Extra for Experts: Why use default encryption?**  
> This automatically encrypts your data when it's stored, adding extra security. If anyone tries to access your documents without the right permissions, they won't be able to read them.

-   Select **Create bucket**.
    

  
  

**Upload Data to S3**

-   Click into your newly created bucket.
    
-   Select **Upload**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.1.png)

  

-   Download this ZIP file with 10 documents inside. You can use these 10 files to build your Knowledge Base: [Download the ZIP file](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Turn%20Your%20Data%20into%20an%20AI%20Chatbot/nextwork-projects.zip)
    

> 🙋‍♀️ **I want to use my own documents for the Knowledge Base**  
> You definitely can! That's the beauty of RAG - you can upload anything you want your chatbot to know. Even if you start with our recommended documents, you can always challenge yourself to redo the project with your own!
> 
> If you want to use your own documents instead, we'd recommend uploading around 10 files to start with, so your chatbot has enough information to answer questions.

-   Head to your local computer's **Downloads** folder and unzip the file.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.4.png)

  

-   Click into the unzipped folder and confirm you see the 10 documents inside.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.9.png)

  

-   Head back to your S3 tab in your browser. You should be in an **Upload** page.
    

> 💡 **Why are we uploading data to S3?**  
> This data will be the source of knowledge for your chatbot. Think of it as the reference material your AI will use to answer questions! The more relevant and well-organized your data is, the better your chatbot will perform.
> 
> In our case, we're uploading a student's portfolio of NextWork project documentation. This will make our chatbot an expert on this student's project experience and the skills they've built!

-   Select **Add files**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-1.3.png)

  

-   select the 10 documents inside the unzipped folder.
    

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

Fantastic! Nice work setting up your S3 bucket - your chatbot is going to become an expert on the documents you've uploaded!

----

## 🧠 Step #2

### Creating the Knowledge Base

Great work setting up your S3 bucket! But having documents stored in S3 isn't enough - your chatbot needs a way to understand and process this information.

That's where your chatbot's knowledge management system, called the **Knowledge Base**, comes in. Let's create a Knowledge Base that helps your chatbot understand and process the documents you've uploaded.

  
  

**In this step, you're going to:**

-   Create a **Knowledge Base** in Bedrock.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/architecture-2.0.png)

  



  
  

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

-   Select **Create** in the Knowledge Bases section.
    
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
> -   The **Foundation Model Parser** uses AI models to scan other things that might be in the files (other than text), like images, tables, headers, and complex formatting. This would be an even better parser for our documents since they contain images. But, because this parser is more complex, it's slower to process and it comes with an additional cost.
>     
> 
>   
> **💡 What is chunking?**  
> **Chunking** breaks a large text into smaller, manageable paragraphs. AI models have a limit on the amount of text they can process at once, so chunking your documents helps the chatbot process information in your Knowledge Base efficiently.
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
>   
> 
> **Embeddings work the same way!** When you add new documents to your Knowledge Base:
> 
> 1.  The embeddings model reads each piece of text.
>     
> 2.  Creates a special "card" (actually a list of numbers) that captures what the text is about.
>     
> 3.  When someone asks a question, it creates another card (list of numbers) for their question.
>     
> 4.  Then matches the question's card with the most similar document cards.
>     
> 
>   
>   
> 
> This is why your chatbot can find relevant information even when the exact words don't match - it's matching the themes and meanings, just like how you could find cookbooks about "pasta" even if someone asks for "Italian food"!
> 
>   
> 💡 **Extra for Experts: Why use numbers instead of words?**  
> Computers are really good at comparing numbers quickly. By converting text into number patterns (that's what embeddings really are!), your chatbot can search through thousands of documents in milliseconds to find the most relevant information.
> 
>   
> 💡 **Extra for Experts: What's an embeddings model?**  
> An embeddings model is like a translator that's been trained to convert text into these number patterns consistently. Titan Text Embeddings v2 is Amazon's own embeddings model - it's fast, accurate, and works well with other AWS services, making it a great choice for processing your Knowledge Base documents.

**Configure the Vector Database**

-   For the **Vector store creation method**, select **Quick create a new vector store.**
    

> 💡 **Extra for Experts: Why choose Quick create?**  
> This option lets Bedrock automatically create a vector store while it creates the Knowledge Base too. You'd pick the other option if you were using a custom vector store you've already created before this.
> 
>   
> 💡 **Extra for Experts: What is a vector store?**  
> Recap: A vector store is a way to store and search for information in a way that understands the meaning of words, not just the words themselves.
> 
> In more technical terms, a vector store is a database that stores your documents' embeddings. It helps the AI find the most relevant information by matching the pattern of your question with similar patterns in your stored documents.

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.11.png)

  

-   Under the **Vector store** section, select **Amazon OpenSearch Serverless**.
    

> 💡 **Extra for Experts: What is Amazon OpenSearch Serverless?**  
> **Amazon OpenSearch Serverless** is a fully managed search and analytics engine. It helps you search, analyze, and visualize large amounts of data quickly.
> 
> In this case, we're using Amazon OpenSearch Serverless as our vector store. Once your documents are chunked and embedded, Bedrock will store the embeddings in OpenSearch.
> 
> Then, when you query your Knowledge Base, Bedrock will go into the OpenSearch vector store to grab the most relevant chunks of text to answer your question.

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.12.png)

  

-   Click **Next** to review your Knowledge Base setup.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-2.13.png)

  

  
  

**Review and Create Knowledge Base**

Let's check your Knowledge Base setup:

Knowledge Base name: `nextwork-rag-documentation`

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



> 🚨 **Important: Make sure to delete your Knowledge Base and OpenSearch vector store**  
> Creating a Knowledge Base costs money. The costs are minimal (< $0.10) if you're only running it for a few hours, so it's a good idea to delete your Knowledge Base and OpenSearch vector store **today!** Make sure to 🗑️ delete both resources.
> 
>   
> **🙋‍♀️ My Knowledge Base creation failed**  
> If your Knowledge Base creation fails, it's usually because your Knowledge Base's IAM role doesn't have proper permissions to access S3.
> 
> Double-check these settings and try again. If you're still having trouble, make sure your IAM user has the `AmazonBedrockFullAccess` policy attached.
> 
> If you're still stuck, [ask the NextWork community!](https://community.nextwork.org/c/i-have-a-question/?topics=7611)

Woop woop! Nice work setting up that Knowledge Base.

As a recap, when you ask your RAG chatbot a question, it works by retrieving relevant chunks of text from your Knowledge Base. Then, it uses an AI model to generate a response.

![A simple recap of how RAG chatbots work](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/kb-flow.png)

A simple recap of how RAG chatbots work

  

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

---
## 🤖 Step #3

### Choose an AI Model

While we're waiting for our Knowledge Base to get ready, let's get access to the AI models available in Amazon Bedrock.

These models will be the brains behind our chatbot - they'll convert your Knowledge Base's results into human-like text responses. Otherwise, your chatbot would just respond with chunks of text from your documents (i.e. the raw search results), which isn't the best experience for anyone using the chatbot!

  
  

**In this step, you're going to:**

-   Select an **AI model** for your chatbot.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/architecture-3.0.png)

  


**Navigate to the Model Access Page**

-   In the left hand navigation menu, scroll down to the **Bedrock configurations** section.
    
-   In a new tab, open **Model access**.
    

  
  

-   We're about to request access to two AI models:
    

**Titan Text Embeddings V2**

**Llama 3.3 70B Instruct**

  
  

-   Check - do you already have access to both models?
    
-   If you've done our [first RAG chatbot project](https://link.nextwork.org/projects/ai-rag-bedrock?utm_source=project_app), you would've requested access to these models before. You'll see green `access granted` labels next to both models if you already have access!
    

![You'll see green `access granted` labels next to both models if you already have access.](https://learn.nextwork.org/projects/static/ai-rag-cli/step-3.4.png)

You'll see green `access granted` labels next to both models if you already have access.

----
i already have access

-   Nice! This means the models are already enabled and ready to use.
    

> 💡 **Extra for Experts: What are we using these models for?**  
> 
> -   **The Titan Text Embeddings V2** model converts text data into numerical embeddings. Your Knowledge Base needs this model to process your documents and understand the meaning of the words inside them.
>     
> -   The **Llama 3.3 70B Instruct** model is used to turn raw data into human-like text responses. When you ask your chatbot a question, the model is what translates the Knowledge Base's results into a chat message.
>     
> 
>   
> 💡 **Extra for Experts: Why are we using Llama 3.3 70B Instruct?**  
> We're going with this model because:
> 
> -   It's one of the most powerful open-source models available in Bedrock
>     
> -   It's 2-3 times more affordable than other options like Claude or GPT-4
>     
> -   It's great at following instructions (that's what the "Instruct" part means!)
>     
> 
>   
> 
> While not _the_ most powerful model in Bedrock, it gives us a great balance of performance and cost for learning and development.

-   Select **Enable specific models**.
    

> 💡 **Why do we need to enable specific models?**  
> In order to use AI models in Bedrock, you need to explicitly **request** access from AWS first. This is because:
> 
> -   Some models are expensive to use, so AWS is double checking that you're consciously opting-in to using them.
>     
> -   AWS needs to make sure they have enough capacity i.e. servers in your region to support the model you want to use.
>     
> -   Some models have different rules and conditions that you need to review and accept before you can start using them.
>     

-   In the list of Base Models, use the search bar or scroll down to find the models you need.
    

> 💡 **Which models should I choose?**
> 
> -   **The Titan Text Embeddings V2** model converts text data into numerical embeddings. Your Knowledge Base needs this model to process your documents and understand the meaning of the words inside them.
>     
> -   The **Llama 3.3 70B Instruct** model is used to turn raw data into human-like text responses. When you ask your chatbot a question, the model is what translates the Knowledge Base's results into a chat message.
>     
> 
>   
> While not the most powerful model in Bedrock, it's open source and 2-3 times more affordable than other options.

-   Select the checkboxes next to:
    
    -   **Titan Text Embeddings V2**
        
    -   **Llama 3.3 70B Instruct**
        
-   Click **Next** to continue.
    
-   Time to review your selections! Make sure you have the right models:
    

**Titan Text Embeddings V2****Llama 3.3 70B Instruct**

  

-   On the Terms and Conditions page, review the pricing:
    

> 💡 **How much will these models cost?**  
> Find the latest pricing information [here](https://aws.amazon.com/bedrock/pricing/).
> 
> The Titan Text Embeddings V2 model costs $0.00002 per 1,000 tokens (i.e. for every ~800 words in your documents).
> 
> The Llama 3.3 70B Instruct model costs $0.00072 per 1,000 tokens (i.e. ~800 words in chatbot conversations).
> 
> It will cost you less than USD $0.01 to complete this project.

-   If you agree to the terms, select **Submit**.
    
-   You'll see a confirmation message at the top of your console.
    

Now that model access is sorted, let's double check that your Knowledge Base has finished creating.

  
----
I already have access need to request model access

-   Select **Enable specific models**.
    

> 💡 **Why do we need to enable specific models?**  
> In order to use AI models in Bedrock, you need to explicitly **request** access from AWS first. This is because:
> 
> -   Some models are expensive to use, so AWS is double checking that you're consciously opting-in to using them.
>     
> -   AWS needs to make sure they have enough capacity i.e. servers in your region to support the model you want to use.
>     
> -   Some models have different rules and conditions that you need to review and accept before you can start using them.
>     

-   In the list of Base Models, use the search bar or scroll down to find the models you need.
    

> 💡 **Which models should I choose?**
> 
> -   **The Titan Text Embeddings V2** model converts text data into numerical embeddings. Your Knowledge Base needs this model to process your documents and understand the meaning of the words inside them.
>     
> -   The **Llama 3.3 70B Instruct** model is used to turn raw data into human-like text responses. When you ask your chatbot a question, the model is what translates the Knowledge Base's results into a chat message.
>     
> 
>   
> While not the most powerful model in Bedrock, it's open source and 2-3 times more affordable than other options.

-   Select the checkboxes next to:
    
    -   **Titan Text Embeddings V2**
        
    -   **Llama 3.3 70B Instruct**
        
-   Click **Next** to continue.
    
-   Time to review your selections! Make sure you have the right models:
    

**Titan Text Embeddings V2**

**Llama 3.3 70B Instruct**

  
  

-   On the Terms and Conditions page, review the pricing:
    

> 💡 **How much will these models cost?**  
> Find the latest pricing information [here](https://aws.amazon.com/bedrock/pricing/).
> 
> The Titan Text Embeddings V2 model costs $0.00002 per 1,000 tokens (i.e. for every ~800 words in your documents).
> 
> The Llama 3.3 70B Instruct model costs $0.00072 per 1,000 tokens (i.e. ~800 words in chatbot conversations).
> 
> It will cost you less than USD $0.01 to complete this project.

-   If you agree to the terms, select **Submit**.
    
-   You'll see a confirmation message at the top of your console.
    

Now that model access is sorted, let's double check that your Knowledge Base has finished creating.

  ------
  

**Sync Your Knowledge Base**

-   Head back to the tab where you're creating your **Knowledge Base**.
    

> 🙋‍♀️ **Ooops, I've closed the Knowledge Base tab!**  
> If you've closed the Knowledge Base tab, you can open it again by going to the `Bedrock` console in a new tab and selecting **Knowledge Bases** from the left hand menu.
> 
> If your Knowledge Base is created, select your Knowledge Base from the list. If your Knowledge Base is not created, select **Create Knowledge Base** and follow the steps in Step #2!

-   You should see a green confirmation banner if the Knowledge Base is done creating. If not, let's wait a few minutes until it's ready!
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-4.5.png)

  

-   Find the **Data sources** section on your Knowledge Base's page.
    
-   Check the check box next to your data source, which should start with `s3-bucket-nextwork-rag-bedrock`.
    
-   Select **Sync** to sync your data for the first time. You'll need to do this to load your S3 documents into the Knowledge Base.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-3.2.png)

  

-   Great! Your Knowledge Base will start syncing your S3 bucket's data.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-3.3.png)

  

> **🙋‍♀️ My synchronization failed**  
> If the synchronization fails, double-check that your Knowledge Base has access to your S3 bucket. Make sure the Knowledge Base's IAM permissions include `AmazonS3ReadOnlyAccess`
> 
(https://community.nextwork.org/c/i-have-a-question/?topics=7611)
> 
>   
> 💡 **Extra for Experts: What happens when we synchronize data?**  
> Synchronization is a process that loads your S3 documents into the Knowledge Base. During this process, your Knowledge Base will:
> 
> -   Read the documents from S3.
>     
> -   Process the documents to understand the meaning of the words inside them.
>     
> -   Store the processed information in the OpenSearch vector database.
>     

-   You should see a success banner like this when the sync is complete:
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.22.png)

  



Great job! You've selected an AI model and synced your data. This should mean you're ready to start conversing with your chatbot. Let's put it to the test... in CloudShell!


----
## ☁️ Step #4

### Running AWS Commands in CloudShell

Let's explore AWS CloudShell, a handy AWS service that lets you run terminal commands from the Management Console! We're going to use it to test a few commands to chat with our chatbot.

> 💡 **Recap: What's the point of chatting with our chatbot over the command line?**  
> While the command line might seem a little intimidating at first, many DevOps and Backend Engineers use it to interact with their tools!
> 
> Here's why:
> 
> -   Engineers can run commands much **faster** than clicking through a web app.
>     
> -   Engineers can script commands to **automate** repetitive tasks.
>     
> -   Engineers usually get **more control** over what they're doing when they're using a command.
>     
> 
>   
> You'll see this in action soon - interacting with Bedrock over the command line is faster and gives you more configuration options.

  
  

**In this step, you're going to:**

-   Run commands in AWS CloudShell to chat with your chatbot.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/architecture-4.0.png)

  


  
  

**Open AWS CloudShell**

-   In the AWS Management Console, select the **CloudShell** icon at the top navigation bar.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.19.png)

  

> 💡 **What is CloudShell?**  
> AWS CloudShell is a shell in your AWS Management Console, which means it's a space for you to run code. We're using CloudShell in this project because it already has AWS CLI pre-installed.
> 
>   
> 💡 **What is CLI?**  
> **AWS CLI (Command Line Interface)** is a software that lets you create, delete and update AWS resources with commands instead of clicking through your console (i.e. the visual interface we just used to set up our chatbot).
> 
> You usually have to install AWS CLI into your computer to use it, but CloudShell already has CLI installed for us (everyone say thank you CloudShell 🙏).
> 
> As you become more familiar with the CLI, you'll find that it becomes your go-to tool over the AWS Management Console. While the Console is fantastic for learning and having a visual guide, the CLI provides the speed and versatility that experienced users need for complex tasks and automations.

-   Wait about 30 seconds for your CloudShell environment to start up. In the meantime, double check that you're in the **Ohio region**!
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.23.png)

  

  
  

**Verify AWS CLI Access**

-   Let's make sure CloudShell is working by running a simple command:
    


```bash
aws --version

```

-   You should see output showing the AWS CLI version number. This confirms that CloudShell is working and you have access to AWS!
    

> 🙋‍♀️ **I don't get a version number**
> 
> -   If your terminal seems frozen, try pressing **Enter**.
>     
> -   If you get an error about credentials, wait a few more seconds for CloudShell to fully initialize.
>     
> -   If issues persist, try refreshing your tab or [asking the NextWork community](https://community.nextwork.org/c/i-have-a-question/?topics=7611) for help.
>     

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.1.png)

  


  
  

**Run Bedrock Commands**

Now, let's use AWS CLI commands to chat with our chatbot. This is where the magic happens!

-   You can choose to explore the AWS CLI documentation to find the command for this step, _or_ you can get the command straight from us.


----
Explore the AWS CLI documentation

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
----

### Get the command
-   Try running the following command in your CloudShell terminal. This command will ask your chatbot to answer the question "What is NextWork?"
    
```
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

## 🔍 Step #5

### Finding Your Knowledge Base and Model IDs

Now that we've tried running our first Bedrock command, let's find the values we need to make it work! We'll need to find your Knowledge Base ID and Model ARN.

  
  

**In this step, you're going to:**

-   Find your **Knowledge Base ID** and **Model ARN**
    
-   Update your Bedrock command with these values
    
-   Run your first successful chat with your Knowledge Base!
    

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/architecture-5.0.png)

  



  
  

**Edit the Retrieve-and-Generate Command**

-   To replace the placeholders, you'll need to edit the **retrieve-and-generate** command.
    
-   Copy the command that asks your chatbot to answer the question "What is NextWork?"
    



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

-   Paste the command into a separate text editor. This can be TextEdit (MacOS), Notepad (Windows), or any other text editor you have on your computer.
    

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

  

-   Head to the text file that you copied the retrieve-and-generate command to.
    
-   Paste the Knowledge Base ID into the command, replacing the `your_knowledge_base_id` placeholder.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.15.png)

  

  
  

**Find Your Model ARN**

Finding the model ARN is a bit more tricky - it's not information you can find over the Management Console! This is because model ARNs are usually handled in the background when you're using the Bedrock console.

You'll need to run another command in CloudShell to find the model ARN.

-----

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
-----
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


-----
### i want  to find the model ID
-   In a new tab, open the Bedrock console again.
![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.4.png)
    
-   Select **Model catalog** from the left hand menu.
    

-   Welcome to the **Model Catalog!** This is where you can find all the models available in Bedrock, and find metadata about each model - like the Model ID.
    ![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.24.png)

-   Find the Llama 3.3 70B Instruct model.
    

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
> 

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.25.png)
-   Click into the model's name.
    ![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.26.png)

-   Copy the **Model ID** from the details panel (it will look like meta.llama3-3-70b-instruct-v1).
    ![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.5.png)

-   Head back to the tab with your **CloudShell** terminal running.
    
-   Paste the **Model ID** into your ModelArn command, replacing the <your-model-id> placeholder.
    

> 🙋‍♀️ **I need the ModelArn command again**  
> Here is the command:
> 
`aws bedrock get-foundation-model --model-identifier <your-model-id>`

-   The model ID is meta.llama3-3-70b-instruct-v1:0
    
-   Here is the command with the model ID filled in:
    

aws bedrock get-foundation-model --model-identifier meta.llama3-3-70b-instruct-v1:0

-   Copy the command, and paste it into your CloudShell terminal.
 ----
 ### give me the mode ID
-   The model ID is meta.llama3-3-70b-instruct-v1:0
    
-   Here is the command with the model ID filled in:
    
`
aws bedrock get-foundation-model --model-identifier meta.llama3-3-70b-instruct-v1:0`

-   Copy the command, and paste it into your CloudShell terminal.
 ----   

-   Press **Enter** on your keyboard to run the command!
    
-   You should see the terminal return the model ARN.
    ![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.8.png)

-   Copy the model ARN.
    
-   Head to the text file that you copied the retrieve-and-generate command to.
    
-   Paste the model ARN into the command, replacing the your_model_arn placeholder.
- ![](https://learn.nextwork.org/projects/static/ai-rag-webapp/cloudshell2.png)


**Run the completed command**

-   Once you've replaced both placeholders, copy the completed command.
    
-   Paste the command in your CloudShell terminal. Let's see whether our chatbot can answer the question "What is NextWork?"
    
-   If your terminal seems stuck, try pressing q on your keyboard. This will force the terminal to start a new command line, which lets you paste a new retrieve-and-generate command!
    
-   Yay! You should get a response from Bedrock, right in the CloudShell terminal. Notice the explanation in the text field of the response.
    

> 🙋‍♀️ **I didn't get the correct response**  
> If your Knowledge Base responds with "Sorry, I am unable to assist you with this request", check whether you've **synced** your Knowledge Base. If your Knowledge Base is not synced with your source data in the S3 bucket, it doesn't have any data to retrieve from!
> 


![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.29.png)



-   Great job! You've just learnt how to use Bedrock over a CLI command. That's a major milestone 🥳
    

> 💡 **Recap: Why is it important to use commands?**  
> Using commands is a really powerful way to interact with your chatbot. It's faster, more flexible, and gives you more control over your chatbot.
> 
> We stayed in the CloudShell terminal to keep this project straightforward, but once you install the AWS CLI into your local computer, you can chat with your chatbot from your local terminal!
> 
> Using commands to interact with a tool is also a step towards learning how to **automate** tasks with code. If you want to integrate this chatbot into your own applications (what we're doing in the next project!), you'll also need to know how to use commands or interact with the tool via code!

-   As you scroll down the terminal response, you might notice that there is a **Retrieved Responses** section with lots of text!

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.18.png)


-   This section shows the raw text that was retrieved from your Knowledge Base. It's like your chatbot is showing you the original documents that it used to answer your question.
    

  

**Tidy up the terminal response**

While it's helpful that you get to see the raw information that's used to generate the response, it might get a bit messy in your terminal if you're running lots of commands.

-   Let's tidy up the terminal response by running this command in your terminal.
    
-   Don't forget to replace your_knowledge_base_id and your_model_arn again!
    

> 🙋‍♀️ **My terminal is stuck**  
> If your terminal is stuck, you can press Ctrl + C or q on your keyboard to stop the command that's currently running. It'll force the terminal to start a new command line, which lets you paste a new retrieve-and-generate command!



```
aws bedrock-agent-runtime retrieve-and-generate \
    --input '{"text": "What is NextWork?"}' \
    --retrieve-and-generate-configuration '{
        "knowledgeBaseConfiguration": {
            "knowledgeBaseId": "your_knowledge_base_id",
            "modelArn": "your_model_arn"
        },
        "type": "KNOWLEDGE_BASE"
    }' \
    --query 'output.text' \
    --output text
```


   
💡 **What's the difference with this command?**  
The --query parameter tells Bedrock to only return the output.text field in the response. This means the terminal response will only show the text of the response, not the raw information that's used to generate it.

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/new.2.png)


-----

## 🗑️ Before you go

### Delete your resources

Now that we've built and tested our chatbot over the terminal (that was so cool), it's time to clean up the resources we created. This is important to avoid getting charged for unused resources!

  
  

**Resources to delete:**

Delete the **Bedrock Knowledge Base**.

Delete the **S3 bucket**.

Delete the **OpenSearch vector store**. 



-----\
🎉 Mission Accomplished

### 

That's a wrap!

Nice work 🤖 You've just built a powerful RAG chatbot using Amazon Bedrock _and_ interacted with it over the command line!

![](https://learn.nextwork.org/projects/static/ai-rag-cloudshell/architecture-complete1.png)

  

**You've learned how to:**

-   Set up a **Knowledge Base** in Amazon Bedrock.
    
-   Use **AWS CloudShell** to run commands in the browser.
    
-   Use **AWS CLI** to access your RAG chatbot.
    
-   💎 Manage your Knowledge Base using the **AWS CLI**.
    
-   💎 Chat with **AI models** right from the terminal.

------

