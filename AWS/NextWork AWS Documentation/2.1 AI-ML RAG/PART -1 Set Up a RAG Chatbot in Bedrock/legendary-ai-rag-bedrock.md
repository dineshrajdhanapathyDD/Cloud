<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up a RAG Chatbot in Bedrock

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-rag-bedrock)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---




# Set Up a RAG Chatbot in Bedrock

Build an AI chatbot that learns from your data with RAG and Amazon Bedrock!

## Summary

In this project, you'll learn how to build a chatbot that's an expert on _you_ - it can answer questions about who you are, what you do, and what you know!

This is made possible when we use a special AI technique called **RAG (Retrieval Augmented Generation)**, which is a way to train an AI chatbot on your personal documents. We'll learn how to do this on **Amazon Bedrock,** an AWS service that gives you access to AI models to bring into your applications.
applications

This is made possible when we use a special AI technique called **RAG (Retrieval Augmented Generation)**, which is a way to train an AI chatbot on your personal documents. We'll learn how to do this on **Amazon Bedrock,** an AWS service that gives you access to AI models to bring into your applications.

![This is what your finished chatbot can do!](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-6.15.png)

## What is RAG? 🤔

AI chatbots like ChatGPT are super smart, but they only know what they learned during training and what they can search online. They can't answer questions about you or your documents, unless you upload your files manually in each conversation (or unless you're a celebrity 👀).

That's where **RAG (Retrieval Augmented Generation)** comes in. RAG is an AI technique that lets you take an AI model's brain (i.e. their ability to turn data into a human-like response) and give it your own documents to train on. Now, your AI chatbot becomes an in-house expert on _your_ documents and information!

Companies often use RAG to create customer support chatbots, but you can also use RAG to create a personal research assistant or an advanced way to search your documents.

  

### Let's get ready to...

🚀 Build a powerful RAG chatbot from scratch in **Amazon Bedrock!**🧠 Create a **Knowledge Base** to hold your chatbot's information.☁️ Use Amazon **S3** and **OpenSearch** to manage your chatbot's data.🛠️ Test and refine your chatbot's performance..

----
👀 Step #0

### 

Before we start Step #1...

**Here's a quick overview of what we're building today:**

You're about to build a chatbot that's trained on your personal documents. When you send a message to your completed chatbot, three things will happen behind the scenes:

1.  The chatbot uses an **AI model** to understand your question and figure out what information it needs to answer it.
    
2.  The AI model sends a request for information it needs to your **Knowledge Base**, which is where you process and store your personal documents.
    
3.  The AI model transforms the raw data (e.g. paragraphs of text) from your Knowledge Base into a **proper response,** which gets sent back to you.
    

![A simple diagram of what we're building](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-0-annotated.png)

A simple diagram of what we're building

  

💡 **How in the world are we going to build this?**

-   We'll build a **Knowledge Base** in Amazon Bedrock in 📚 Steps #1-3.
    
-   We'll pick the best **AI models** for our chatbot in 🔑 Step #4.
    
-   We'll sync your documents from **S3** to the Knowledge Base in 🔁 Step #5.
    
-   Finally, Bedrock sets up a chatbot when we connect the Knowledge Base and AI model, which we'll test in 🤖 Step #6!
    

![Your complete solution will look like this](https://learn.nextwork.org/projects/static/ai-rag-bedrock/architecture-complete.png)

Your complete solution will look like this

  

-----

## 📚 Step #1


### Setting Up a Knowledge Base

To kick things off in Bedrock, let's create a **Knowledge Base** (also called a KBase) and set up an S3 bucket. A Knowledge Base acts like your chatbot's personal library, storing all the information it needs to answer questions.

  
  

**In this step, you're going to:**

-   Create a Knowledge Base in Amazon Bedrock.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/architecture-1.0.png)

  



  
  

**Sign in to AWS**

-   Log in to the AWS Management Console [as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    
-   Make sure you're in the **Ohio** (**us-east-2**) region.
    

> **💡 Why Ohio?**  
> Some features in Bedrock, like the AI models we'll use and API features for the secret mission (🤫) are only offered in certain regions.
> 
> Ohio (us-east-2) luckily offers all the features we need for this project. Other regions, from Sydney (ap-southeast-2) to Ireland (eu-west-1) do not offer all the features we'll use. This is because the data centres in those regions might not have the hardware required for advanced AI models, or because AWS chooses to roll out new features in certain regions first before making them available globally.

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.1.png)

  

-   In the search bar at the top of the console, type `Amazon Bedrock`
    
-   Select **Amazon Bedrock** from the dropdown list.
    

> 💡 **What is Amazon Bedrock?**  
> Think about Amazon Bedrock like an AI model marketplace - you can search for and use different models from top companies, like OpenAI, Anthropic, and Meta, in one place.
> 
> Developers usually need to sign up separately for each AI service, manage multiple API keys, handle different APIs, and set up their own servers to run these models. But with Bedrock, you can do all of this through one simple console - from testing AI models to using them in your apps for different tasks, like answering questions or analyzing text.
> 
> In Bedrock, you can also train AI models on your own information (this process is called RAG). This helps you create custom models that respond based on your specific data, and is how we'll create a chatbot in this project!

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.6.png)

  

  
  

**Create a Knowledge Base**

-   In the Amazon Bedrock console, find the left hand sidebar.
    
-   Under **Builder Tools,** click **Knowledge Bases**.
    

> 💡 **What is a Knowledge Base?**  
> A Knowledge Base is a collection of personal documents in Bedrock.
> 
> Bedrock has a handy feature that lets you connect your Knowledge Base with an AI model to **chat** with your documents, which is how we'll create our personal chatbot.

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.5.png)

  



-   Click **Create** in the top-right.
    
-   A dropdown will appear. Select **Knowledge Base with vector store**.
    

> 💡 **What is a Knowledge Base with vector store?**  
> Think of a **vector store** as an advanced way to search for information.
> 
> Here's how it works. If you decide to search "I want a book about **machine learning**":
> 
> -   A **traditional search** will find you books that have the words 'machine' and 'learning' inside it.
>     
> -   A **vector store** will find you books with the words 'machine' and 'learning' inside it, but **also** books about neural networks, deep learning, AI algorithms... books that don't necessarily say "machine learning", but talk about related concepts. This is because vector store understands the **meaning** behind your request, not just the specific words.
>     

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.4.png)

  

> 💡 **Extra for Experts: How are vector stores used in real life?**  
> Knowledge Bases with vector stores power:
> 
> -   **Customer Support chatbots** to help customers find the right resource or troubleshooting guides for complex issues, even if they're using different terminology in their search query.
>     
> -   **Research databases** to help researchers, like legal teams and doctors, find relevant examples of similar cases or medical conditions.
>     
> -   **Technical Documentation** to help developers find exact code examples instantly, especially when they're looking for a specific API or function.
>     

-   Under **Knowledge base name**, enter `nextwork-rag-documentation`.
    
-   Under **Description**, enter `This Knowledge base stores all documentation at NextWork.`
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.3.png)

  

-   Under **IAM permissions,** select **Create and use a new service role**.
    

> 💡 **Extra for Experts: What is a service role?**  
> A service role is a special type of permission setting that lets a service (in this case, Bedrock) access your resources. Bedrock is going to need to access your documents to store them in a Knowledge Base, so we'll create a service role for it.

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.2.png)

  

**Choose a Data Source**

-   Under **Choose data source,** select **Amazon S3**.
    

> 💡 **What is Amazon S3?**  
> Amazon S3 is a storage system. Think of it as a digital folder where you can store your documents, photos, videos, and other files.
> 
> We haven't set it up yet, but we'll be storing our documents in S3 bucket later in this step. You _can_ store your documents directly in Bedrock, but it's best practice to keep documents in a separate system like S3, so it's possible to manage your documents independently from your chatbot.
> 
>   
> 💡 **Extra for Experts: What are the other data source options?**
> 
> -   **Web Crawler**: Choose this if you want to store data that lives on a public website on the internet.
>     
> -   **Custom Data**: Best for storing data directly in Amazon Bedrock. This works well if you have a wide range of data types and formats that don't fit into the other options.
>     
> -   **Third party data sources**: Best for connecting Bedrock with data that lives privately inside another app, like Salesforce or Sharepoint.
>     

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.1.png)

  

-   Click **Next**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.7.png)

  

-   Under **Data source name,** replace the placeholder with something easier to recognize, like `s3-bucket-nextwork-rag-bedrock`.
    
-   Make sure **This AWS account** is selected under **Data source location.**
    
-   Select **Browse S3**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.8.png)

  

-   Aha - as you might notice, this is the step where we're supposed to connect our Knowledge Base to **S3.**
    



Nice work kicking off your Knowledge Base! As a recap, a Knowledge Base is like a personal collection of documents that your chatbot will use to answer questions.

We haven't put together the collection of documents our chatbot will use yet. It looks like we need to do that to finish setting up our Knowledge Base, so let's jump into storing our documents in the next step!

----
## 🪣 Step #2

### Store Your Documents in S3

We'll need to store your documents in S3, then connect S3 with your Knowledge Base. Luckily, Amazon S3 is a simple and easy-to-use storage system in AWS - let's set it up now!

  
  

**In this step, you're going to:**

-   Create an S3 bucket.
    
-   Upload documents to the S3 bucket. These documents will make up your chatbot's Knowledge Base.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/architecture-2.0.png)

  



  
  

**Create an S3 Bucket**

-   In a **new tab,** head to the `S3` console.
    
-   **🚨 Check:** Make sure you're using a new tab, so you don't cancel your progress with setting up the Knowledge Base.
    

> 🙋‍♀️ **Oops! I accidentally closed the Bedrock tab**  
> If you've accidentally closed the tab, or lost your progress with setting up the Knowledge Base, we can always do this set up again! You'll nail it in no time. Click here to start your Bedrock setup again.

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.13.png)

  

-   Check that you're in the same region as your Knowledge Base i.e **Ohio**.
    

> **💡 Why the same region?**  
> Bedrock is a region-specific service, which means your Knowledge Base can only access data in the same region.
> 
> In general, keeping your resources in the same region reduces latency (the time it takes for data to travel) and can lower costs too.

-   Select **Create bucket**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.12.png)

  

-   For **Bucket name**, enter a unique name like `nextwork-rag-bedrock-<your-initials>`.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.11.png)

  

-   Under **Object Ownership**, leave **ACLs disabled (recommended)** selected.
    

> 💡 **Extra for Experts: Why leave ACLs disabled?**  
> This makes managing permissions simpler. The bucket owner gets full control, which helps prevent accidental permission issues.

-   Scroll down to **Block Public Access settings**.
    
-   Make sure **Block all public access** is checked (default setting).
    

> 💡 **Extra for Experts: Why block all public access?**  
> This keeps your data safe by making sure only authorized users can access your bucket. You don't need to share your documents with anyone other than the Knowledge Base, so this is a good default setting.

-   Leave the default encryption settings.
    

> 💡 **Extra for Experts: Why use default encryption?**  
> This automatically scrambles your data when it's stored, adding extra security. If anyone tries to access your documents without the right permissions, they won't be able to read them.

-   Click **Create bucket**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.10.png)

  

  
  

**Upload Files to S3**

-   Select your newly created bucket.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.9.png)

  

-   Select **Upload**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.16.png)

  

-   Download this ZIP file with 10 documents inside. You can use these 10 files to build your Knowledge Base: [Download the ZIP file](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Turn%20Your%20Data%20into%20an%20AI%20Chatbot/nextwork-projects.zip)
    

> 🙋‍♀️ **I want to use my own documents for the Knowledge Base**  
> You definitely can! That's the beauty of RAG - you can upload anything you want your chatbot to know.
> 
> If you want to use your own documents instead, we'd recommend uploading around 10 files to start with, so your chatbot has enough information to answer questions.

-   Head to your local computer's **Downloads** folder and unzip the file.
    
-   Click into the unzipped folder and confirm you see the 10 documents inside.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.25.png)

  

-   Drag and drop your documents into S3's upload area, or select **Add files** to browse and select them.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.15.png)

  

-   Make sure you're uploading the individual documents, not the entire ZIP file!
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.24.png)

  

-   Select **Upload**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-1.14.png)

  

-   Wait for the file upload to finish. While we wait..
    



-   Confirm that all your files have uploaded. Phew!
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.6.png)

------  

## 🧠 Step #3

### Finish Setting Up Your Knowledge Base

Now that we have our S3 bucket set up, let's finish setting up the Knowledge Base in Bedrock.

  
  

**In this step, you're going to:**

-   Finish setting up the Knowledge Base in Bedrock.
    
-   Select the S3 bucket as your data source.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/architecture-3.0.png)

  



**Connect a Data Source to Your Knowledge Base**

-   Head back into your **Bedrock** tab, where you're setting up your Knowledge Base.
    
-   In the S3 bucket window, click on the **refresh** button.
    
-   Select your S3 bucket, which should start with `nextwork-rag-bedrock-`.
    
-   Select **Choose**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-2.10.png)

  

-   Leave the default settings for **Parsing strategy** and **Chunking strategy**.
    

> **💡 What is parsing?**  
> Parsing means the way data gets processed. There are two main types of parsers in Bedrock:
> 
> -   The **Default parser** automatically detects and extracts text from common file formats like PDFs, Word docs, and text files.
>     
> -   The **Foundation Model Parser** uses AI models to scan other things that might be in the files (other than text), like images, tables, headers, and complex formatting. This would be an even better parser for our documents since they contain images. But, because this parser is more complex, it's slower to process and it comes with an additional cost.
>     
> 
>   
> **💡 What is chunking?**  
> **Chunking** breaks a large text into smaller, manageable paragraphs. AI models have a limit on the amount of text they can process at once, so chunking your documents helps the chatbot process information in your Knowledge Base efficiently.
> 
> By default, your documents will be chunked into 300 tokens, which is like 300 words or punctuation marks.

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-2.8.png)

  



-   Select **Next** to continue.
    
-   In the **Embeddings model** section, select **Select mdoel**.
    
-   Select **Titan Text Embeddings v2**.
    
-   select **Apply**.
    

> 💡 **What are embeddings?**  
> Think of embeddings as a way to translate your documents into a special language that computers can understand better. When your knowledge base is created, the embedding model converts the documennts' text into unique patterns of numbers that capture the meaning of the content. Later, when someone asks a question, the same process happens to match their question with the most relevant parts of your stored documents.
> 
> 💡 **What's an embedding model?**  
> An embedding model is like a translator that's been trained to convert text into these number patterns consistently. Titan Text Embeddings v2 is Amazon's own embedding model - it's fast, accurate, and works well with other AWS services, making it a great choice for processing your Knowledge Base documents.

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-2.6.png)

  



**Configure the Vector Database**

-   For the **Vector store creation method**, select **Quick create a new vector store.**
    

> 💡 **Why choose Quick create?**  
> This option lets Bedrock automatically create a vector store as it created the Knowledge Base too. You'd pick the other option if you were using a custom vector store you've already created before this.
> 
>   
> 💡 **What is a vector store?**  
> Recap: A vector store is a way to store and search for information in a way that understands the meaning of words, not just the words themselves.
> 
> In more technical terms, a vector store is a database that stores your documents' embeddings. It helps the AI find the most relevant information by matching the pattern of your question with similar patterns in your stored documents.

-   Under the **Vector store** section, select **Amazon OpenSearch Serverless**.
    
-   👀 Tip: OpenSearch Serverless becomes really important in a later step of this project. We'd recommend taking a close look at the definition below!
    

> 💡 **What is Amazon OpenSearch Serverless?**  
> **Amazon OpenSearch Serverless** is a fully managed search and analytics engine. It helps you search, analyze, and visualize large amounts of data quickly.
> 
> In this case, we're using Amazon OpenSearch Serverless as our vector store. Once your documents are chunked and embedded, Bedrock will store the embeddings in OpenSearch.
> 
> Then, when you query your Knowledge Base, Bedrock will go into the OpenSearch vector store to grab the most relevant chunks of text to answer your question.



![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-2.5.png)

  

-   Click **Next** to review your Knowledge Base setup.
    

  
  

**Review and Create Knowledge Base**

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-2.4.png)

  

Let's check your Knowledge Base setup:

**Knowledge Base Name:** Confirm the Knowledge Base name is what you entered i.e. `nextwork-rag-documentation`.

**Data Source:** Confirm that your S3 bucket is selected i.e. `s3-bucket-nextwork-rag-bedrock`.

**Embeddings Model:** Confirm **Titan Text Embeddings v2** is chosen.

**Vector Store:** Confirm **Quick create a new vector store** is selected.

  
  



-   Select **Create Knowledge Base**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-2.1.png)

  

> 💡 **What happens now?**  
> Bedrock will set up your knowledge base, which can take up to 10 minutes.
> 
> Hang in there! In the background, AWS is prearing the vector database, which includes chunking your documents and embedding them. The status of your Knowledge Base will change to **Available** once it's ready.
> 
> Lucky for us, we won't need to wait until the Knowledge Base is ready. Let's move on to the next step while it's being created.

![You might see this loading state for 10+ minutes, so we'll move on to the next step while your Knowledge Base is getting ready!](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-2.9.png)

You might see this loading state for 10+ minutes, so we'll move on to the next step while your Knowledge Base is getting ready!

----
## 🔑 Step #4

### Get Access to AI Models

While we're waiting for our Knowledge Base to get ready, let's get access to the AI models available in Amazon Bedrock.

These models will be the brains behind our chatbot - they'll convert your Knowledge Base's results into human-like text responses. Otherwise, your chatbot would just respond with chunks of text from your documents (i.e. the raw search results), which isn't the best experience for anyone using the chatbot!

  
  

**In this step, you're going to:**

-   Explore different AI models in Bedrock.
    
-   Get access to 3 models for this project.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/architecture-4.0.png)

  



  
  

**Navigate to the Model Access Page**

-   In the left navigation pane, scroll down to **Bedrock configurations** and open **Model access** in a new tab.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-3.7.png)

  

> 💡 **What is a model?**  
> A model is a pre-trained AI model that can you can use to generate text. Popular AI chatbots today, like ChatGPT and Claude, use these models behind the scenes to generate text responses.
> 
>   
> 💡 **Why do we need AI models anyway?**  
> You can think of vector search as a searching function for your Knowledge Base, but the AI models are what translates the search results into a chat message that answers your questions.
> 
> Without your AI model, your chatbot would only respond with relevant chunks of text from your documents, which isn't the best experience for anyone using the chatbot!


  
  

**Modify Model Access**

-   You will see a list of available models in Bedrock!
    
-   Select **Enable specific models**.
    

> 💡 **Why do we need to enable specific models?**  
> In order to use AI models in Bedrock, you need to explicitly **request** access from AWS first. This is because:
> 
> -   Some models are expensive to use, so AWS is double checking that you're consciously opting-in to using them.
>     
> -   AWS needs to make sure they have enough capacity i.e. servers in your region to support the model you want to use.
>     
> -   Some models have different rules and conditions that you need to review and accept before you can start using them. For example, Anthropic models need you to fill out a form that tells them what you're going to use the model for.
>     

  
  

**Select the Models to Request Access**

-   In the list of Base Models, use the search bar or scroll down to find the models you need.
    

> 💡 **How do I know which models to choose??**
> 
> -   **The Titan Text Embeddings V2** model converts text data into numerical embeddings. You might notice that we've actually come across this model when we set up our Knowledge Base's embedding settings. Your Knowledge Base wouldn't be able to use this model if we didn't request access to it!
>     
> -   The **Llama 3.1 8B Instruct** model is Meta's open source AI model. The **Instruct** version is optimized for handling conversational AI and instruction-following tasks.
>     
> -   The **Llama 3.3 70B** Instruct model is a larger and more capable version of the 8b version, useful for applications that need advanced reasoning and response generation. We'll use it to compare its responses against the 8B version.
>     
> 
>   
> Note: While Llama Instruct models are not the most powerful models in Bedrock, they are open source. It's 2-3 times more affordable to use Llama Instruct models compared to the others.

-   Select the checkboxes next to the following models:
    
    -   **Titan Text Embeddings V2**
        
    -   **Llama 3.1 8B Instruct**
        
    -   **Llama 3.3 70B Instruct**
        

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-3.4.png)

  

### ✍️ Explain the process of getting access to AI models in Bedrock

Start your answer with 'To get access to AI models in Bedrock, I had to... AWS needs explicit access because...'

Task Completed

-   Click **Next** to continue.
    
-   Time to review your selections! Make sure you have the right models:
    

**Titan Text Embeddings V2**

**Llama 3.1 8B Instruct**

**Llama 3.3 70B Instruct**

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-3.2.png)

  

**Accept the Terms and Submit**

-   The next page will show AWS' Terms and Conditions for using the models. This also tells us to acknowledge that we agree to the sellers' prices for the models.
    

> 💡 **How much will these models cost?**  
> Find the latest pricing information [here](https://aws.amazon.com/bedrock/pricing/).
> 
> The Titan Text Embeddings G1 - Text model costs $0.00002 per 1,000 tokens (i.e. for every ~800 words in the documents you upload).
> 
> The Llama **3.1 8B** Instruct model costs $0.00022 per 1,000 tokens (i.e. ~800 words in a conversation with your chatbot).
> 
> The Llama **3.3 70B** Instruct model costs $0.00072 per 1,000 tokens (i.e. ~800 words in a conversation with your chatbot).
> 
> It will cost you less than USD $0.01 to create and use your chatbot in this project.

-   If you agree, select **Submit**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-3.1.png)

  

-   Nice! A confirmation message will appear at the top of your console.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-3.8.png)

  

-   Once approved, the models will be available for you to use in your chatbot. Yay!!
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.7.png)

  
-----

## 🔄 Step #5

### Sync Your Knowledge Base

Woohooo! Knowledge Base, done ✅ AI models, done ✅

Surely that means we're ready to chat with our chatbot?!

Well, not yet. We still need to **synchronize** our data from S3 bucket to our Knowledge Base.

Creating the Knowledge Base simply sets up the **infrastructure** for your chatbot to use, but the data hasn't been loaded into the Knowledge Base yet. Let's see what synchronizing means in this step...

  
  

**In this step, you're going to:**

-   Sync your data from S3 to your Knowledge Base.
    



  
  

**Select a Model**

-   Head back to your **Bedrock** tab. Your Knowledge Base should be done creating now!
    
-   At the right hand side of your console, click **Select Model**.
    
-   Under **Model Providers**, choose **Meta** to see the Llama models you've requested access to.
    
-   Select **Llama 3.1 80B Instruct**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-4.4.png)

  

-   Click **Apply** to confirm your selection.
    
-   Try typing `Hello` in the chat input box.
    
-   Hmmm... you might notice that you can't enter anything into the box yet.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.8.png)

  

> 💡 **What's wrong?**  
> While you've created your Knowledge Base, you haven't **synced** the Knowledge Base with your data source. This means your Knowledge Base doesn't have any information inside, so you can't chat with your chatbot - it literally doesn't know anything yet 🤡
> 
>   
> **💡 But I've already picked the data source when I set up the Knowledge Base! Why do I have to sync?**  
>   
> 
> Creating the Knowledge Base sets up the **infrastructure** for your chatbot to use. In this case, Bedrock has created a Knowledge Base that's _connected_ to a data source (the S3 bucket) and a vector store (OpenSearch Serverless). But, the data hasn't actually moved from S3 into your Knowledge Base yet.



  
  

**Sync Your Data Source**

-   On the right hand side of the page, select **Go to Data Sources**.
    
-   Check the check box next to your data source, which should start with `s3-bucket-nextwork-rag-bedrock`.
    
-   Click **Sync** to store your data for the first time.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-4.2.png)

  

> 💡 **What's happening when we sync?**  
> Syncing involves three key steps:
> 
> 1.  **Ingesting** - Bedrock will retrieve the data from the **data source** (S3).
>     
> 2.  **Processing** - Bedrock will chunk (i.e. split up into smaller pieces) and embed (i.e. convert into numbers) the data.
>     
> 3.  **Storing** - Bedrock will store the processed data in the **vector store** (OpenSearch Serverless).
>     

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.23.png)

  

The syncing process will take some time, depending on the size of the data you've uploaded. For example, if you've uploaded the 10 documents we've provided into your S3 bucket, syncing will take about 5 minutes.

In the meantime...

----

## 🤖 Step #6

### Chat With Your Chatbot

Now, let's test our chatbot - you'll see how it generates personalised responses about your data! 🏃‍♀️

  
  

**In this step, you're going to:**

-   Test your chatbot.
    
-   Troubleshoot some errors with your AI model.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/architecture-7.0.png)

  



**Sending Your First Question**

-   Wait until your data has synced.
    
-   Inside your Knowledge Base, find the **Test Knowledge Base** section on the right panel.
    
-   You should be able to sent a message now! If you see the text input still greyed out, you might need to select your AI model (Llama 3.1 8B Instruct) again.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-4.5.png)

  

-   Let's send the first one, like:
    



```text
Hello

```

-   Oops! You might get the following error:
    



```text
Invocation of model ID meta.llama3-1-8b-instruct-v1:0 with on-demand throughput isn't supported.

```

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.26.png)

  

> 🙋‍♀️ **I didn't get this error!**  
> Try sending a few more messages, and note whether your model responds with "Sorry, I am unable to assist you with this request." If that's the case, you're facing a similar issue!
> 
>   
> 💡 **What does this error mean?**  
> This happens because the AI model you're using, Llama 3.1 8B, doesn't support **on-demand inference!**
> 
> **Inference** is the process of using an AI model to generate responses. There are two ways to run inference in Bedrock:
> 
> -   **On-demand inference** - The model starts up and runs only when you need it. This is more cost-effective for occasional use, but can be slower to start up.
>     
> -   **Pre-provisioned inference** - The model is always running and ready to respond. This is more expensive but provides faster responses and consistent performance.
>     
> 
>   
> Older or more complex AI models (like Llama 3.1 8B) often need pre-provisioned inference because they need dedicated computing resources to run efficiently. Newer, or more advanced AI models (like Llama 3.3 70B) can handle on-demand inference because they're less resource-intensive to start up!

-   To fix this, select the pencil icon next to the model name.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.22.png)

  

-   Select **Llama 3.3 70B Instruct** and set it to **On-Demand inference**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-6.2.png)

  

-   Click **Apply**.
    
-   Let's try sending the same message again:
    



```text
Hello

```

-   Nice - should see the chatbot respond with a greeting!
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.21.png)

  



  
  

**Observe the Model's Response**

-   Now, let's try asking a question that's related to your data.
    



```text
What is NextWork?

```

-   If the model successfully processes the query, it should give you a summary of NextWork!
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.20.png)

  



  
  

**Ask An Out of Context Question**

-   Now, try asking a question that's not related to your data:
    



```text
How do you make a cup of tea?

```

-   Your model will likely tell you there's no relevant information in your data, or it might say "**Sorry, I am unable to assist you with this request**."
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.13.png)

  

-   This proves to you that your chatbot has no knowledge outside of your data. Now that's tea! 🍵
    


  
  

**Toggle Generate Responses**

-   Last, let's take a look at a setting at the top of the chat - switch **Generate Responses** to **Off**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.17.png)

  

-   Try asking another question:
    


```text
What AWS services has the student worked on?

```

-   Oooo, the chatbot responds with chunks of text from your data source!
    

> 💡 **What does this mean?**  
> When the **Generate Responses** setting is off, your AI model is no longer translating the Knowledge Base's search results into a chat response. This is a great option if you just want to retrieve the processed data directly from your Knowledge Base, to analyze it further yourself.

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.16.png)

  

-   Now let's switch **Generate Responses** back to **On**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.15.png)

  

-   This tells Bedrock that we want an AI model to generate responses after all the data is retrieved. Let's select our AI model again!
    
-   Select **Select Model**.
    
-   Select **Meta**.
    
-   Select **Llama 3.3 70B Instruct**.
    
-   Click **Apply**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.14.png)

  

-   Try asking your chatbot the same question again:
    



```text
What AWS services has the student worked on?

```

-   Tada! Your chatbot goes back to responding with a detailed summary of the AWS services the student has worked on.
    

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-new.18.png)

  

### ✍️ What happens when you toggle Generate Responses on and off?

Start your answer with 'You can also turn off Generate Responses setting to'...

Task Completed

Well done on building your personalized chatbot! That was an awesome journey going from a zip file of documents to a fully functional chatbot.

With this, you've made an AWESOME start on what you can do with RAG in AI!

-----
🗑️ Before you go

### 

Delete your resources

Now that we've built and tested our chatbot, it's time to clean up the resources we created. This is important to avoid getting charged for unused resources.

  
  

**Resources to delete:**

Delete the **Knowledge Base** in Amazon Bedrock.

Delete the **S3 bucket.**

Delete the **vector store** in OpenSearch.

### Delete Knowledge Base

-   In your Bedrock console, head to **Knowledge Bases** from the left hand menu.
    
-   Select your Knowledge Base.
    
-   Select **Delete**.
    
![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-delete.7.png)
-   Type delete in the confirmation field.
    
-   Select **Delete**.

-   In your Bedrock console, head to **Knowledge Bases** from the left hand menu.
    
-   Select your Knowledge Base.
    
-   Select **Delete**.
    

-   Type delete in the confirmation field.
    
-   Select **Delete**.
    

-   Head to the S3 console.
    
-   Select **General purpose buckets** from the left hand menu.
    
-   Select your S3 bucket (nextwork-bedrock-rag).
    
-   Select **Empty**.
    

-   Type permanently delete in the confirmation field.
    
-   Select **Empty** to confirm emptying the bucket.
    
-   Once the bucket is empty, select it again and select **Delete**.
    
-   Type nextwork-bedrock-rag in the confirmation field.
    
-   Confirm the deletion.
    
### Delete S3 Bucket
-   Head to the S3 console.
    
-   Select **General purpose buckets** from the left hand menu.
    
-   Select your S3 bucket (nextwork-bedrock-rag).
    
-   Select **Empty**.
![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-delete.6.png)

-   Type permanently delete in the confirmation field.
    
-   Select **Empty** to confirm emptying the bucket.
    
-   Once the bucket is empty, select it again and select **Delete**.
    
-   Type nextwork-bedrock-rag in the confirmation field.
    
-   Confirm the deletion.


### Delete Vector store

-   Head to the OpenSearch console.
    
-   Select **Collections** from the left hand menu.
    
-   Select your vector store.
    
-   Select **Delete**.
    
    ![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/step-delete.2.png)

-   Type confirm in the confirmation field.
    
-   Select **Delete**.

-----
🎉 Mission Accomplished

### 

That's a wrap!

Nice work! 🤖 You've just built a powerful RAG chatbot using Amazon Bedrock.

![](https://learn.nextwork.org/projects/static/ai-rag-bedrock/architecture-complete.png)

  

**You've learned how to:**

-   Set up a Knowledge Base and AI modelin Bedrock.
    
-   Use S3 to store and manage your chatbot's data.
    
-   Test your RAG chatbot!
-----

