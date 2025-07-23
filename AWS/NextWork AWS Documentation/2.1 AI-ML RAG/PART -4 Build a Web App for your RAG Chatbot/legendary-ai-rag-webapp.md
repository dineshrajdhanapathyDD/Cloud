<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Web App for your RAG Chatbot

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-rag-webapp)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---



# Build a Web App for your RAG Chatbot

Let's build a web app that makes it easy to connect and chat with your RAG chatbot!

## Summary

Welcome to part FOUR of this RAG chatbot series!

In this series' grand finale, we're building a **fully functional web app** where users can chat with your chatbot and get answers based on your documents.

Instead of running terminal commands or making API calls, a web app gives you a sleek, easy and beautiful way to use your chatbot. Just type your message in the chat box, hit enter, and your chatbot will respond!

This isn’t just about having a nice interface to look at - building a web app is also about making your chatbot accessible, scalable, and truly user-friendly.

This project is great for building your hands-on experience for roles like **Frontend Developer**, **Full Stack Developer**, or **Cloud Architect**, where you need to know how to build complete web applications that integrate AI capabilities.

This project also builds on the previous projects in our **RAG with Amazon Bedrock** series:

### In this project, get ready to...

-   🧠 Set up your chatbot using **Amazon Bedrock** and **S3.**
    
-   💻 Clone and customize a pre-built web app.
    
-   🔌 Connect the app's frontend to your chatbot via an API.
    
-   🚀 Run and test your web app.
    
-   💎 Design your own app frontend.
    
![](https://learn.nextwork.org/projects/static/ai-rag-webapp/architecture-complete.png)

-----
## 👀 Step #0

### Before we start Step #1...

We're about to build a web app with your very own **RAG chatbot** inside. Being a **RAG** chatbot means it can answer questions based on information in your personal documents, instead of just general knowledge.

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/comparison.png)

  

**How does a web app with a RAG chatbot work?**

A web app is often made up of three layers (and our web app is no different)!

-   Layer 1: The **data** is the information your app needs. For our RAG chatbot, this is the knowledge we're storing in Bedrock that our chatbot will use to answer questions.
    
-   Layer 2: The **backend** handles the processing and logic. For our RAG chatbot, this is the code that passes your users' messages to Amazon Bedrock (to generate a response behind the scenes) and passes back the response.
    
-   Layer 3: The **frontend** is what users see and interact with. For our RAG chatbot, this is the chat interface that lets users send a message.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/architecture-layers-annotated.png)

  

  
  

**🤔 How in the world are we going to build a web app with a RAG chatbot?**

1.  First, we'll set up the app's **data**:
    
    -   In 🧠 Step #1  
        , we'll use S3 to store our chatbot's information, and then connect S3 to a Knowledge Base in Bedrock.
        
2.  Then, we'll set up the app's **backend**:
    
    -   In 👯 Step #2, we'll clone a pre-built web app from GitHub. This web app already has an API built in, so you can use it with your chatbot.
        
    -   In 🚀 Step #3, we'll test run the API - this will help us make sure the API we cloned actually works.
        
    -   In ❓ Step #4  
        chatbot i.e. the Knowledge Base you set up in Step #1._your_, we'll customize the API to connect with
        
3.  Finally, we'll connect the app's **frontend** to the backend:
    
    -   Note: When we clone the code in Step #2, we also clone the code for the web app's frontend (the frontend and backend code live in the same repository).
        
    -   In 🕸️ Step #5, we'll use a modified API that connects with both your chatbot and the app's frontend, and use it to chat with your chatbot!
        

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/architecture-annotated.png)

-----

## 🧠 Step #1

### Creating the Knowledge Base

To set up a RAG chatbot, we need to set up the information it needs to know! That's where Amazon S3 comes in - it's going to be the home for all the documents and information that your chatbot will learn from.

  
  

**In this step, you're going to:**

-   Create an S3 bucket to store your chatbot's training materials.
    
-   Upload documents that your chatbot will learn from.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/architecture-1.png)

  


If you've done the [previous projects](https://learn.nextwork.org/projects/ai-rag-bedrock) in this series, the steps for setting up your Knowledge Base might be familiar! Challenge yourself to set up your chatbot's Knowledge Base by yourself, or if you'd like, you can follow step by step guidance:  
  

I'll try set up the Knowledge Base myself!Walk me through it step by step

Bravo! If you ever get stuck, you can always switch to the step by step guidance. Here are some tips for setting up your Knowledge Base:

  
  

**🔥 Hot Tip #1:** If you'd like, you can use these 10 files to train your chatbot: [Download the ZIP file](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Turn%20Your%20Data%20into%20an%20AI%20Chatbot/nextwork-projects.zip)

**🔥 Hot Tip #2:** When you're ready to create your Knowledge Base, make sure you're using these settings:  
  

Knowledge Base name: **nextwork-rag-documentation**

Data source type: **S3**

Embeddings Model: **Titan Text Embeddings v2**

Vector Store: **Quick create vector store** with **OpenSearch Serverless**

Woop woop! Nice work setting up that Knowledge Base. Your chatbot will use the information in your Knowledge Base to answer questions.



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


Now that we have our Bedrock Knowledge Base ready, that's our web app's **data** all set up ✅

----
## 👯 Step #2

### Cloning the Web App

Next up, let's jump into the web app's **frontend** and **backend**!

It can be quite complex to write the code for a web app that integrates with your Knowledge Base. You need to create a frontend, handle API requests, manage the connection to AWS, handle errors, style your pages with CSS, _and_ coordinate the data, frontend and backend to work together 🤯

Luckily, we've prepared some starter code for you! We'll use a pre-built web app that has all the essential components ready to go - from the frontend chat interface to the backend API code. To start using this app, we'll need to make a copy of the code so you can run it locally.

  
  

**In this step, you're going to:**

-   Copy the web app's code from **GitHub** to your local machine.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/architecture-2.png)

  



We'll use Git to **clone** code that already exists for the web app. Cloning = downloading a copy of the code to your local machine. Once you've cloned the repository, you can run the web app locally!

  
  

**Open the GitHub Repository**

-   Open the web app's GitHub repository in your browser: [https://github.com/NatNextWork1/nextwork-rag-webapp](https://github.com/NatNextWork1/nextwork-rag-webapp)
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-22.png)

  

This is where all the web app code lives. Notice that there are three separate files in the repository:

-   **main.py**, which contains code for an API that connects to the Amazon Bedrock chatbot. We're going to focus on this file first, and use it to test whether the API (i.e. the app's backend) works.
    
-   **web_app.py** is a version of main.py that has the API code _but also_ runs a frontend. Once we've tested the API by running main.py, we'll run web_app.py next to chat with your chatbot over a beautiful interface!
    
-   **requirements.txt** lists the dependencies (i.e. tools you'll need to install) to run main.py and web_app.py.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-23.png)

  

You might also spot two folders in the repository:

-   **static/** holds the files and images that style your frontend. In our case, we just have a `style.css` file inside this folder, which contains some basic styling (like font sizes or background colours) for the web app.
    
-   **templates/** holds the HTML files that make up the frontend. In our case, we have a `index.html` file, which is the only page in our web app.
    
-   Although we only have one file in each folder, it's always best practice to use folders to store frontend because it helps keep our code organized and easy to manage - imagine if we had multiple images and HTML files in our project!
    

> 👀 Curious about the code? We break it down in the 💎 Mini Secret Mission later in this project!

  
  

**Clone the Repository**

> **💡 What does cloning a repository mean?**  
> Cloning a repository means we're downloading a copy of the repository to our local machine. This lets us run the code on our own computer.

-   Open your computer's local terminal, which should be **Terminal** on macOS or **PowerShell** on Windows.
    
-   In your local terminal, let's navigate to your Documents directory. This gets us ready to clone the repository in your Documents folder:  
      
    

### MacOS/Linux


```bash
cd ~/Documents

```

-   Run this command to clone the repository - don't forget to replace the `[HTTPS-URL]` placeholder with the repository's URL:
    



```bash
git clone [HTTPS-URL]

```

-   To find the HTTPS URL, head back to your browser and the [repository's GitHub page.](https://github.com/NatNextWork1/nextwork-rag-webapp/tree/main)
    
-   Select the **Code** button.
    
-   Copy the **HTTPS URL** of the repository.
    

> **💡 Why are we copying the HTTPS URL?**  
> In GitHub, the HTTPS URL is like an address for the repository. We'll use it to tell our local machine where to find the repository we want to clone.

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-102.png)

  

> 🙋‍♀️ **Don't have Git installed?**  
> If you see an error that Git is `not available`, head to the [Git website](https://git-scm.com/downloads) to download and install Git for your operating system.

Off we go! This command will download all the files from the GitHub repository to a new folder with the same name as the repository.

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-17.png)

  

-   After cloning the repository, let's head into the project you've cloned by running:  
      
    

### MacOS/Linux


```bash
cd nextwork-rag-webapp

```

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-18.png)

  

-   Check that you're in the correct directory by running:
    



```bash
pwd

```

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-19.png)

  

-   This command prints out your current directory. If the path ends with `nextwork-rag-webapp`, it means you're in the right place!
    

> 🙋‍♀️ **My path is wrong!** If you don't see the right path when you run `pwd`, double check that you don't already have a folder with the same name in your Documents folder. Once you've confirmed that...
> 
> -   MacOS/Linux: You can try going into your project directory again by running `cd ~/Documents/nextwork-rag-webapp`.
>     
> -   Windows: You can try going into your project directory again by running `cd %USERPROFILE%\Documents\nextwork-rag-webapp`.
>     


**Ayyyy look at you go! You've just cloned the repository to your local machine.**

You now have all the project files ready to work with, well done. Let's set up a virtual environment to start running the web app.

  
  

**Create Your Virtual Environment**

-   Still in your terminal and project directory, let's create a new virtual environment:
    



```bash
python3 -m venv venv

```

> 💡 **What is a virtual environment?**  
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
> Think of it like a separate workspace for a specific coding project, like this web app. Just like how you might have different folders for different school subjects, each virtual environment keeps all the tools and packages for a specific project in one place.
> 
> The best part? Everything in this environment is **separate** and **temporary**. When you delete the environment folder, all the packages you installed are removed too, keeping your computer tidy.
> 
> Without a virtual environment, tracking the packages or libraries you've installed for a project can be tricky. It also be harder to run two different versions of the same tool, if two projects need different versions.
> 
>   
> 💡 **What are packages or libraries?**  
> Packages or libraries are pre-written code that you can use in your project. For example, if you're building a weather app, you could use a package that lets you make API requests to get the weather data.

-   What do you see in your terminal?  
      
    

Nothing...I ran into an error

-   Your terminal won't show anything straight away, but an empty response like this actually means your virtual environment has been created with no issues:
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/capture.png)

  

-   Activate your virtual environment:  
      
    

### MacOS/Linux



```bash
source venv/bin/activate

```

> 💡 **What does it mean to activate a virtual environment?**  
> When you **activate** a virtual environment, you're telling your computer to start using the virtual environment you created:
> 
> -   All the Python packages you install will only exist in this environment.
>     
> -   Your project won't interfere with other Python projects on your computer.
>     
> -   You'll see `(venv)` at the start of your command prompt to show your virtual environment is activated.
>     

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-21.png)

  



Good job! You've just cloned your RAG web app's code, and activated a virtual environment for running it. That means you're ready to start running your web app 😮‍💨👏

As a recap, the code you cloned contains two parts:

1.  The **frontend**: `index.html` and `style.css` work together to create a chat interface that lets users send a message.
    
2.  The **backend**: `main.py` and `web_app.py`are two **different** options for your web app's backend code (you only run one of them at a time). You can run either:
    
    -   `main.py`, which is a simple backend that connects to your Bedrock Knowledge Base (but doesn't display the frontend code), or
        
    -   `web_app.py`, which is an upgraded version of `main.py`. It connects your app to your Bedrock Knowledge Base _and_ runs the frontend code, so running this file will let you see a nice chat interface!
        




-----
## 🚀 Step #3

### Testing the Backend

Now that we have our virtual environment set up, it's time to put it to work - is it time to run the web app?!

Welllll, not exactly. It's best practice to test that the **different parts** of your web app are working properly first, **before** you run the entire web app. Don't forget that a web app has three parts:

1.  The **data** (i.e. the information your app uses, like your Bedrock Knowledge Base). We've set this up in 🧠 Step #1.
    
2.  The **backend** (i.e. the code that runs behind the scenes). We've just cloned the code for this part in 🚀 Step #2.
    
3.  The **frontend** (i.e. the interface you see in your browser). We've also just cloned the code for this part in 🚀 Step #2.
    

  
  

In this step, we'll focus on testing the **backend** part of the web app. Does it actually work, can you really run the backend code locally? Let's find out!

  
  

**In this step, you're going to:**

-   Test that your web app's backend code is working properly.
    
-   Run the backend code locally.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/architecture-3.png)

  



  
  

**Run the API**

-   Head back to your terminal.
    
-   Run the following command to start the API server:
    


```bash
python3 -m uvicorn main:app --reload

```

> 🙋‍♀️ **The command didn't work!**  
> If the command didn't work, try running it again with `python` instead of `python3`.

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-25.png)

  

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
> -   **-m uvicorn:** This says "Use the uvicorn program". We'll learn more about what this means in a second!
>     
> -   **main:app:** This tells uvicorn where to find your API code. The `main` refers to your main.py file, and app refers to the `@app` sections inside that file
>     
> -   **--reload:** This is like an "auto-refresh" mode. Later on, when you make changes to your code, the server will automatically restart so you don't have to manually stop and start it.
>     

-   Uh oh! You might see an error like this:
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-26.png)

  

> **🙋‍♀️ What's this error?**  
> You might see an error like `ModuleNotFoundError: No module named uvicorn` if your virtual environment doesn't actually have Uvicorn installed yet!
> 
> Uvicorn is a web server that runs your API and makes it accessible in your browser. When you start your API, Uvicorn listens for incoming requests (like when a user sends a message to your chatbot) and makes sure they reach your FastAPI code. Without Uvicorn, your API wouldn't actually run—it's the engine that keeps everything moving!

  
  

**Install Requirements**

Other than Uvicorn, there are other packages that you'll need to run your API. These packages are all listed in the `requirements.txt` file in your project directory.

-   To see what packages are being installed, you can view the contents of the `requirements.txt` file:
    



```bash
cat requirements.txt

```

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-1.png)

  

> 💡 **What's in requirements.txt?**  
> This file lists all the Python packages our API needs:
> 
> -   `fastapi`: The web framework for building our API.
>     
> -   `uvicorn`: Uvicorn is a web server that runs your API and makes it accessible in your browser. When you start your API, Uvicorn listens for incoming requests (like when a user sends a message to your chatbot) and makes sure they get passed to your API code. Without Uvicorn, your API wouldn't actually run—it's the engine that keeps everything moving!
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

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-2.png)

  

-   Now let's check that the packages are installed by listing the installed packages in your virtual environment:
    



```bash
pip3 list

```

-   You should see `fastapi`, `boto3`, `python-dotenv`, and `uvicorn` in the list.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-3.png)

  

> 💡 **Woah! Why am I seeing a lot of other packages?**  
> This is because we're installing all the packages listed in `requirements.txt` _and_ the dependencies of each package.
> 
> When you install Python packages, they often come with their own dependencies - other packages they need to work properly.
> 
> Think of it like buying a new computer - aside from the computer (the main package) itself, you might also need to get a charger (dependency) for it to work!
> 
> For example, `boto3`, one of our packages, requires `botocore`, `jmespath`, and `s3transfer` to actually connect to AWS.



  
  

**Run the API**

-   Start running the API again by running:
    



```bash
python3 -m uvicorn main:app --reload

```

-   Yay, no more errors! You should see a message like `Uvicorn running on http://127.0.0.1:8000` in your terminal.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-29.png)

  

Let's check out the API in action!

  
  

**Visit the Root Endpoint**

-   Open your web browser and go to the URL provided in the terminal output, usually [http://127.0.0.1:8000](http://127.0.0.1:8000/).
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-120.png)

  

-   You should see the message `{"message": "Welcome to your RAG chatbot API"}` in your browser. This confirms that your API is running - nice work!
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-30.png)

----
💎 Mini Secret Mission

### 

Breaking Down the API Code

You just saw your API's welcome message - pretty cool! You might be wondering... what's actually happening behind the scenes when you visit that endpoint?

Your mission, should you choose to accept it, is to 🕵️‍♀️ peek under the hood 🕵️‍♀️ of your web app and discover how that welcome message (and the rest of your API's functionality) actually works.

> 🙋‍♀️ **I've done the previous project in this series on APIs, should I still do this secret mission?**
> 
> Yes! We dive a little bit deeper into the API code in this secret mission, so it's a great way to level up your understanding of APIs.

**In this mini secret mission, you're going to:**

-   Break down your web app's backend code, which is in `main.py`.
    
-   Showcase your **advanced understanding** of the backend code and the API!
    

> 💎 **Secret Mission unlocked!**

Woooho! Well done choosing to do this secret mission (you legend). Let's crack open the code we just cloned, and uncover the secrets of how our app's API works.

> 💡 **Why should I care about understanding APIs?**  
> An API is a way for different apps to talk to each other. Visually, they look likes lines of code in your backend file, like `main.py`. But practically, it is APIs that...
> 
> -   Let your messaging apps send messages across the world.
>     
> -   Help your weather app know the temperature in your area.
>     
> -   Enable your banking app to safely transfer money.
>     
> 
>   
> Once you understand how APIs work, you'll start seeing them everywhere - and better yet, you'll know how to use them in your own projects like this one!
> 
> Plus, when an API error happens (and trust me, it will later in this project 😉), you'll know exactly where to look to fix it.

  
  

**Review the web app's code**

-   Head back to the web app's GitHub repository in your browser: [https://github.com/NatNextWork1/nextwork-rag-webapp](https://github.com/NatNextWork1/nextwork-rag-webapp)
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/github.png)

  

-   Open the `main.py` file.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-25.png)

  

> 💡 **What is `main.py`?**  
> `main.py` is a file that contains the code for our API. An API is like a bridge that lets different apps talk to each other. It's like having a translator that can understand and respond to requests in a language that both apps can understand.
> 
> In our case, the API will let our web app to talk to the Amazon Bedrock chatbot.
> 
> ![](https://learn.nextwork.org/projects/static/ai-rag-api/api.png)


----
### Import the tools we need

At the start of `main.py`, we're importing the tools we need for the API to work.

> 💡 **Why do we need imports?**  
> Think of it like this: Instead of coding everything from scratch, we're grabbing pre-built tools. It's like using pre-made components when building something - way faster than making every piece yourself.

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-2.png)

  

Here's what each import does:

-   `from fastapi import FastAPI` gets us **FastAPI** to build our API. Normally, you'd have to write a lot of code to handle things like receiving user input (e.g., when a user sends a chat message) and sending back responses. FastAPI takes care of that for you, making it much faster and easier to build APIs. That’s why it’s one of the most popular Python frameworks (companies like Uber and Netflix use FastAPI for their backend APIs too).  
      
    
-   `import boto3` gets us the **AWS SDK** for Python. The AWS SDK is like a library of pre-built tools that helps our code communicate with AWS services, such as storing files in S3 or accessing AI models in Bedrock, without needing to handle all the low-level details.  
      
    
-   `import os` lets us work with **environment variables.** Instead of storing sensitive info (like API keys) directly in our code, we can keep them separate and access them securely using os.  
      
    
-   `from dotenv import load_dotenv` helps us **load** the environment variables from a file. This means we can keep our environment variables in a separate `.env` file and easily access them in our code without hardcoding them. It's security best practice and easier to manage if your confidential information is in a separate file, so that you're less likely to accidentally expose it!
    



Nice! If you haven't finished exploring the code, jump back ⬆️ to the top of these tabs and pick the next section.

----

### Load the environment variables




After you import your tools, we set up our environment variables (lines 8-14):

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-5.png)

  

This code loads settings we need to connect to AWS:

-   `load_dotenv()`: Reads variables from an environment variable file. We haven't created this file yet, but we will soon to store our environment variables inside!
    
-   `AWS_REGION = os.getenv("AWS_REGION")`: Gets the AWS region from our environment variables. We do the same for `KNOWLEDGE_BASE_ID` and `MODEL_ARN`
    

> 💡 **What are these environment variables?**  
> We need three main variables:
> 
> -   `AWS_REGION`: The AWS region where your resources live (for us, it's us-east-2)
>     
> -   `KNOWLEDGE_BASE_ID`: The ID of your Bedrock Knowledge Base.
>     
> -   `MODEL_ARN`: The Bedrock AI model you want to use to generate chat responses.
>     
> 
>   
> 💡 **Why are we importing them? Why not just put these variables in the code?**  
> Putting these variables directly in the code is a security risk! If you accidentally push your code to GitHub with AWS credentials or Knowledge Base ID in it, _anyone_ could use them. Environment variables keep sensitive stuff separate from your code. Much safer.




----
### Create the FastAPI app


-   Continue scrolling down in `main.py` until you find the line `app = FastAPI()` (line 16).
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-6.png)

  

This line is where everything starts coming together!! 🔥

When we write `app = FastAPI()`, we're creating a **new FastAPI application** that will power our entire API.

Think of it as setting up a central command center - this `app` will handle every request that comes in, figure out what to do with it, and send back the right response.

> 💡 **What is FastAPI?**  
> FastAPI is a Python framework that makes it easy to build APIs. It’s called "fast" because it's optimized for performance and reduces the amount of code you need to write.
> 
> For example, when a user sends a message to your chatbot, FastAPI automatically:
> 
> -   Checks the data to make sure it's structured correctly (e.g., making sure required fields aren’t missing or empty).
>     
> -   Converts it into Python objects, so your code can process it easily in the next step.
>     

Next up, let's look at how we connect to Amazon Bedrock!

  
  

-   Look for the function definition `def get_bedrock_client():` in `main.py` (line 18).
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-8.png)

  

Think of this function like you're setting up a dedicated phone line between your API and Amazon Bedrock.

Once it's set up, your API can easily send requests to Bedrock and get responses back. Let's break down what each part does:

-   `bedrock_client = boto3.client(...)`: This line creates our connection to AWS.
    
-   `"bedrock-agent-runtime"`: This tells AWS exactly which service we want to talk to. The `bedrock-agent-runtime` service is specifically designed for working with Bedrock agents and knowledge bases - exactly what we need for our chatbot!
    
-   `region_name=AWS_REGION`: This tells AWS which AWS Region we want to connect to, using that `AWS_REGION` value we set up earlier as an environment variable.
    

> 💡 **So... am I using the AWS CLI to talk to Bedrock?**  
> Nope, you're not using the AWS CLI to talk to Bedrock. You're actually using the **AWS SDK** for Python (called boto3) to talk to Bedrock.
> 
>   
> 💡 **What's the difference between the AWS CLI and an SDK?**  
> Think of it this way: Use the CLI when you need to do something quickly yourself in the terminal, and use an SDK when you're building an application that needs to work with AWS.
> 
>   
> **AWS SDKs (Software Development Kits) are:**
> 
> -   Libraries you import into your code (like [boto3 for Python](https://aws.amazon.com/sdk-for-python/)). Other SDKs are available for different programming languages, like the AWS SDK for Java, JavaScript, or Go.
>     
> -   Used for **building applications** that need to work with AWS, because it lets your application make AWS calls.
>     
> -   In this project, our `main.py` uses `boto3` to call Bedrock whenever a user sends a chat message to our chatbot.
>     
> 
>   
> **AWS CLI (Command Line Interface) is:**
> 
> -   A tool you run directly in your terminal.
>     
> -   Used for quick, manual tasks and commands.
>     
> -   Great for testing or one-off operations.
>     
> 
> ![You might recall running a CLI command in the previous projects in this series!](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-9.png)
> 
> You might recall running a CLI command in the previous projects in this series!

----

### Set up what our API does

Import the tools we needLoad the environment variablesCreate the FastAPI appSet up what our API does

Let's explore how we tell our API what to do when a request comes in! In the next section of `main.py`, find the line that says `@app.get("/")` (line 22).

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-10.png)

  

-   `@app.get("/")` creates the root of your API. Let's break this down:
    
    -   `@app` tells Python "this is part of our API application"
        
    -   `.get` means "when someone visits this URL in their browser"
        
    -   `"/"` means "the main page" (like how facebook.com/ is Facebook's main page)
        
    -   When someone visits this URL, they'll see a welcome message: `{"message": "Welcome to your RAG chatbot API"}`
        

> 💡 **What are API routes?**  
> An API route is like a path to a specific part or function in your API.
> 
>   
> 💡 **Why do we need routes?**  
> Our web app is relatively simple because we're only setting up one connection between our web app and our chatbot. When a user sends a message, our API sends it to our chatbot and passes back a response.
> 
> But, imagine if we wanted to connect to **multiple** chatbots! We'd need **multiple** routes to connect to each chatbot. Or, imagine if we wanted to do more things with our chatbot, like send responses back using a different AI model or without using the Knowledge Base at all. We'd need **multiple** routes to do all of these things!
> 
> In our case, we have two routes:
> 
> -   `/` is the root route, which is like the default route for our API. If the user doesn't specify a route, our API will use this route.
>     
> -   `/bedrock/query`: This is a route that lets the user query our chatbot.
>     

-   `@app.get("/")`: This special **decorator** tells FastAPI "Hey, when someone comes to the root route (`/`), here's what we should do..." The lines right below this decorator then define the instructions for what to do when someone visits the root of our API.
    
-   `def read_root()`: This is the function that runs when someone arrives. It's like having a greeter at the door!
    
-   `return {"message": "Welcome to your RAG chatbot API!"}`: This sends back a friendly welcome message to whoever visited the root of our API.
    

  
  

**`/bedrock/query`**

Now for a super exciting part - let's look at how the API connects with our chatbot!

-   Find the line `@app.get("/bedrock/query")` (line 26) in your code.
    
-   This is the dedicated route where apps can send queries and get answers from our chatbot!
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-11.png)

  

> 💡 **Extra for Experts: I want to know more about the code!**  
> Let's break down the code, line by line:
> 
> -   `@app.get("/bedrock/query")`: This tells our API "hey, when someone visits the route ending in /`bedrock/query`, run the code below"
>     
> -   `async def bedrock_query(text: str)`: This creates a function that will handle the question someone asks.
>     
> -   `text: str`: This says "expect the user's question to come in as text". When someone asks a question like `/bedrock/query?text=What is AWS?`, the `text` part ("What is AWS?") is the user's question.
>     
> -   `bedrock = get_bedrock_client()`: Earlier in `main.py`, we created the `get_bedrock_client()` function that connects your web app to AWS (psst... it was in line 19!). This line runs that exact function to set up a connection to Bedrock.
>     
> -   `response = bedrock.retrieve_and_generate(...)`: This line:
>     
>     1.  Takes the user's question.
>         
>     2.  Searches through your Knowledge Base for relevant information.
>         
>     3.  Uses the AI model to write an answer.
>         
> 
> ![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-12.png)
> 
>   
> 
> -   `knowledgeBaseId=KNOWLEDGE_BASE_ID`: Tells Bedrock which Knowledge Base to search in (using that ID we saved in our environment variables)
>     
> -   `modelArn=MODEL_ARN`: Tells Bedrock which AI model to use for answering (also from our environment variables)
>     
>     ![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-13.png)
>     
>       
>     
> -   `retrievalConfiguration={...}`: Sets up how we want to search the Knowledge Base. We're using "vector search" here, which means it looks for information based on meaning, not just exact word matches
>     
> -   `generationConfiguration={...}`: Gives the AI model some guidelines about how to create its response
>     
> -   `promptConfiguration={...}`: This is like giving the AI model instructions about how to use the information it found to answer the question
>     
> -   `text=text`: This passes along the actual question the user asked
>     
> -   `modelInvocationConfiguration={...}`: Some technical settings for the AI model, like telling it to use the Claude model
>     
> -   `return {"response": response["output"]["text"]}`: Takes the AI's answer and sends it back to whoever asked the question
>     
>     ![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-14.png)
>

-------

Nice! If you haven't finished exploring the code, jump back ⬆️ to the top of these tabs and pick the next section.

-   Continue scrolling down in main.py until you find the line app = FastAPI() (line 16).
    

This line is where everything starts coming together!! 🔥

When we write app = FastAPI(), we're creating a **new FastAPI application** that will power our entire API.

Think of it as setting up a central command center - this app will handle every request that comes in, figure out what to do with it, and send back the right response.

> 💡 **What is FastAPI?**  
> FastAPI is a Python framework that makes it easy to build APIs. It’s called "fast" because it's optimized for performance and reduces the amount of code you need to write.
> 
> For example, when a user sends a message to your chatbot, FastAPI automatically:
> 
> -   Checks the data to make sure it's structured correctly (e.g., making sure required fields aren’t missing or empty).
>     
> -   Converts it into Python objects, so your code can process it easily in the next step.
>     

Next up, let's look at how we connect to Amazon Bedrock!

  

-   Look for the function definition def get_bedrock_client(): in main.py (line 18).
    

Think of this function like you're setting up a dedicated phone line between your API and Amazon Bedrock.

Once it's set up, your API can easily send requests to Bedrock and get responses back. Let's break down what each part does:

-   bedrock_client = boto3.client(...): This line creates our connection to AWS.
    
-   "bedrock-agent-runtime": This tells AWS exactly which service we want to talk to. The bedrock-agent-runtime service is specifically designed for working with Bedrock agents and knowledge bases - exactly what we need for our chatbot!
    
-   region_name=AWS_REGION: This tells AWS which AWS Region we want to connect to, using that AWS_REGION value we set up earlier as an environment variable.
    

> 💡 **So... am I using the AWS CLI to talk to Bedrock?**  
> Nope, you're not using the AWS CLI to talk to Bedrock. You're actually using the **AWS SDK** for Python (called boto3) to talk to Bedrock.
> 
>   
> 💡 **What's the difference between the AWS CLI and an SDK?**  
> Think of it this way: Use the CLI when you need to do something quickly yourself in the terminal, and use an SDK when you're building an application that needs to work with AWS.
> 
>   
> **AWS SDKs (Software Development Kits) are:**
> 
> -   Libraries you import into your code (like [boto3 for Python](https://aws.amazon.com/sdk-for-python/)). Other SDKs are available for different programming languages, like the AWS SDK for Java, JavaScript, or Go.
>     
> -   Used for **building applications** that need to work with AWS, because it lets your application make AWS calls.
>     
> -   In this project, our main.py uses boto3 to call Bedrock whenever a user sends a chat message to our chatbot.
>     
> 
>   
> **AWS CLI (Command Line Interface) is:**
> 
> -   A tool you run directly in your terminal.
>     
> -   Used for quick, manual tasks and commands.
>     
> -   Great for testing or one-off operations.
>     

Nice! If you haven't finished exploring the code, jump back ⬆️ to the top of these tabs and pick the next section.

Let's explore how we tell our API what to do when a request comes in! In the next section of main.py, find the line that says @app.get("/") (line 22).

-   @app.get("/") creates the root of your API. Let's break this down:
    
    -   @app tells Python "this is part of our API application"
        
    -   .get means "when someone visits this URL in their browser"
        
    -   "/" means "the main page" (like how facebook.com/ is Facebook's main page)
        
    -   When someone visits this URL, they'll see a welcome message: {"message": "Welcome to your RAG chatbot API"}
        

> 💡 **What are API routes?**  
> An API route is like a path to a specific part or function in your API.
> 
>   
> 💡 **Why do we need routes?**  
> Our web app is relatively simple because we're only setting up one connection between our web app and our chatbot. When a user sends a message, our API sends it to our chatbot and passes back a response.
> 
> But, imagine if we wanted to connect to **multiple** chatbots! We'd need **multiple** routes to connect to each chatbot. Or, imagine if we wanted to do more things with our chatbot, like send responses back using a different AI model or without using the Knowledge Base at all. We'd need **multiple** routes to do all of these things!
> 
> In our case, we have two routes:
> 
> -   / is the root route, which is like the default route for our API. If the user doesn't specify a route, our API will use this route.
>     
> -   /bedrock/query: This is a route that lets the user query our chatbot.
>     

-   @app.get("/"): This special **decorator** tells FastAPI "Hey, when someone comes to the root route (/), here's what we should do..." The lines right below this decorator then define the instructions for what to do when someone visits the root of our API.
    
-   def read_root(): This is the function that runs when someone arrives. It's like having a greeter at the door!
    
-   return {"message": "Welcome to your RAG chatbot API!"}: This sends back a friendly welcome message to whoever visited the root of our API.
    

  

**/bedrock/query**

Now for a super exciting part - let's look at how the API connects with our chatbot!

-   Find the line @app.get("/bedrock/query") (line 26) in your code.
    
-   This is the dedicated route where apps can send queries and get answers from our chatbot!
    

> 💡 **Extra for Experts: I want to know more about the code!**  
> Let's break down the code, line by line:
> 
> -   @app.get("/bedrock/query"): This tells our API "hey, when someone visits the route ending in /bedrock/query, run the code below"
>     
> -   async def bedrock_query(text: str): This creates a function that will handle the question someone asks.
>     
> -   text: str: This says "expect the user's question to come in as text". When someone asks a question like /bedrock/query?text=What is AWS?, the text part ("What is AWS?") is the user's question.
>     
> -   bedrock = get_bedrock_client(): Earlier in main.py, we created the get_bedrock_client() function that connects your web app to AWS (psst... it was in line 19!). This line runs that exact function to set up a connection to Bedrock.
>     
> -   response = bedrock.retrieve_and_generate(...): This line:
>     
>     1.  Takes the user's question.
>         
>     2.  Searches through your Knowledge Base for relevant information.
>         
>     3.  Uses the AI model to write an answer.
>         
> 
> -   knowledgeBaseId=KNOWLEDGE_BASE_ID: Tells Bedrock which Knowledge Base to search in (using that ID we saved in our environment variables)
>     
> -   modelArn=MODEL_ARN: Tells Bedrock which AI model to use for answering (also from our environment variables)
>     
> -   retrievalConfiguration={...}: Sets up how we want to search the Knowledge Base. We're using "vector search" here, which means it looks for information based on meaning, not just exact word matches
>     
> -   generationConfiguration={...}: Gives the AI model some guidelines about how to create its response
>     
> -   promptConfiguration={...}: This is like giving the AI model instructions about how to use the information it found to answer the question
>     
> -   text=text: This passes along the actual question the user asked
>     
> -   modelInvocationConfiguration={...}: Some technical settings for the AI model, like telling it to use the Claude model
>     
> -   return {"response": response["output"]["text"]}: Takes the AI's answer and sends it back to whoever asked the question
>     

Nice! If you haven't finished exploring the code, jump back ⬆️ to the top of these tabs and pick the next section.

  

**Well doneeeee!** You've just investigated the main.py file and how the API works behind the scenes - especially how it's set up to connect to Amazon Bedrock and handle queries 👏

Now that you know about this API inside out, you might notice that you've only run one of it's endpoints so far... we haven't actually used it to chat with our chatbot yet!

Let's do that in the next step.

-------

## ❓ Step #4

### Run the Query Endpoint

It's timeeeee 🥁 to test your API's most important endpoint - the **query** endpoint!

This is where we'll see our chatbot API in action, taking questions from users and providing answers based on our Knowledge Base.

> 💡 **What is the `query` endpoint?**  
> This endpoint is defined in `main.py` using `@app.get("/bedrock/query")`.
> 
> ![](https://learn.nextwork.org/projects/static/ai-rag-api/screenshot-122.png)
> 
>   

**In this step, you're going to:**

-   Ask your chatbot a question over the API (using the `query` endpoint)
    
-   Troubleshoot errors in your API setup.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/architecture-4.png)

  



**Visit the Query Endpoint**

-   Now, let's test the `query` endpoint in your API.
    
-   Update the URL in your browser to: [http://127.0.0.1:8000/bedrock/query?text=What%20is%20NextWork](http://127.0.0.1:8000/bedrock/query?text=What%20is%20NextWork). This asks your chatbot "What is NextWork?"
    
-   Whoops! You'll get an error.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-33.png)

  

Look like the steps for running the API has missed a few key things... your **challenge** now is to troubleshoot the issues and get the API running!

> 🙋‍♀️ **I don't want to troubleshoot on my own!**  
> If this is your first project in the entire RAG x Bedrock series, you're more than welcome to skip this troubleshooting challenge and move on to getting step-by-step guidance on how to get the API running successfully.

  
  

**Your troubleshooting challenge:**

If you've done the last few parts of this series, you would've already practiced all the troubleshooting steps you need to get the API running successfully.

Here is a list of things you can check to troubleshoot the issues and get the API running successfully.

Did you request access for the AI model you want to use in Bedrock?

Did you sync your Knowledge Base and S3 bucket?

Did you install the AWS CLI?

Did you configure the AWS CLI with access keys?

Are your access keys still valid? Run `aws sts get-caller-identity` to check.

Did you configure the AWS CLI with the correct region (i.e. us-east-2)?

Did you set environment variables i.e. `AWS_REGION`, `KNOWLEDGE_BASE_ID`, `MODEL_ARN`?

  
  

If you get stuck, no worries! Here are some detailed step-by-step guidance to troubleshoot common errors that might come up in this step.

> 🙋‍♀️ Heads up! This step is a bit of a 'choose your own adventure' experience. You will only come across certain questions/screenshots if you run into that error. You **don't** need to answer all the questions/take all the screenshots to complete this project!

----

### Parameter Failed Error

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-4.png)

  

-   If you see an error message for `Invalid type for parameter` related to your `knowledgeBaseId` or `modelArn`, it means that your API isn't correctly configured with your Knowledge Base ID and Model ARN.
    

  
  

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

  

-   Create a new `.env` file in your project directory.
    

> 💡 **What is the `.env` file?**  
> The `.env` file is a text file that contains environment variables for your application. It's used to store sensitive information like API keys and other configuration settings.

-   The instructions for creating the `.env` file depend on your operating system:  
      
    

MacOS/LinuxWindows

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
> -   `KNOWLEDGE_BASE_ID`: The ID of your Bedrock Knowledge Base.
>     
> -   `MODEL_ARN`: The Amazon Resource Name of your AI model.
>     
> 
>   
> 💡 **What am I using the AI model for?**  
> The AI model is responsible for creating the chat responses that respond to the user's questions. They're super important for our chatbot to work!
> 
> If this is your first time using Amazon Bedrock and Knowledge Bases, we'd highly recommend checking out Step #4 in our [beginner RAG chatbot with Bedrock project](https://link.nextwork.org/projects/ai-rag-bedrock?utm_source=project-app) to get a better understanding of how AI models work and how to use them in your chatbot.

-   To fix your error and get the API's `query` endpoint running, we'll need to replace these placeholders with your actual values:
    
    -   `<your_knowledge_base_id>`: Your Knowledge Base's ID.
        
    -   `<your_model_arn>`: Your AI Model's model ARN.
        

  
  

**Find Your Knowledge Base ID**  
  

Let me find it myselfWhere do I find the Knowledge Base ID?

-   In a new tab, open the `Bedrock` console again.
    
-   Select **Knowledge Bases** from the left hand menu.
    
-   Select your Knowledge Base.
    
-   Find the **Knowledge Base ID** from the overview panel.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.11.png)

  

-   Copy the **Knowledge Base ID**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.12.png)

  

-   Head to your `.env` file.
    
-   Paste the Knowledge Base ID into the `.env` file, replacing the `<your_knowledge_base_id>` placeholder.
    

![](https://learn.nextwork.org/projects/static/ai-rag-cli/step-4.15.png)

  

  
  

**Find Your Model ARN**

Finding the model ARN is a bit more tricky - it's not information you can find over the Management Console! This is because model ARNs are usually handled in the background when you're using the Bedrock console.

You'll need to **run another command** in CloudShell to find the model ARN.  
  

I want to find the command myselfGive me the command

-   In **AWS CloudShell,** run the following command to find the ARN of your model. No need to paste it in your text editor first!
    



```bash
aws bedrock get-foundation-model --model-identifier <your-model-id>

```

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/cloudshell1.png)

  

> 💡 **Damn it, I got an error!**  
> That's okay! It's because you don't know your AI model's ID yet, which is `<your-model-id>` in the command above.
> 
> We'll need to find your AI model's ID first, and replace the placeholder with that ID. _Then_ we'll get the model's ARN.
> 
> Yup - it's an extra step - but it's a good way to practice your CLI skills! You've got this.

-   You can choose to explore the Bedrock console to find the model ID, _or_ you can get the completed command straight from us.  
      
    

I want to find the Model IDGive me the Model ID

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

  

-   Head back to the tab with your **CloudShell** terminal running.
    
-   Paste the **Model ID** into your ModelArn command, replacing the `<your-model-id>` placeholder.
    

> 🙋‍♀️ **I need the ModelArn command again**  
> Here is the command:
> 
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

-   Copy the model ARN.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/cloudshell3.png)

  

-   Head back to the `.env` file.
    
-   Paste the model ARN into the `.env` file, replacing the `<your_model_arn>` placeholder.
    
-   Once you've replaced the placeholders for your Knowledge Base ID and model ARN, save the file! The instructions for this depend on your operating system:  
      
    

MacOS/LinuxWindows

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

  



  




------

### Unable to locate credentials

-   You might see an error that says `Unable to locate credentials`
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-5.png)

  

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

-------

### Unable to Assist with Request

Parameter Failed ErrorUnable to locate credentialsUnable to Assist with RequestOther Common Errors

-   You might see your chatbot return `Unable to assist with request`
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-7.png)

  

-   Well, the good news is that your AI model can return a response! This tells us that your app can access your AWS environment, which is already pretty darn impressive.
    
-   What's left is to make sure that once the web app is connected to your AWS environment, the AI models and Knowledge Base in Bedrock are also ready to use. Let's go investigate...
    

  
  

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
> If you're still stuck, [ask the NextWork community!](https://community.nextwork.org/c/i-have-a-question/?topics=7611)
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

-----

### Other Common Errors

Parameter Failed ErrorUnable to locate credentialsUnable to Assist with RequestOther Common Errors

Here are some other errors you might encounter and how to fix them:

  
  

**UnrecognizedClientException**

-   Let's check the rest of the error message - does it say your security token is invalid?
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/UnrecognizedClientException.png)

  

-   This usually means your access key credentials are incorrect!
    
-   To validate whether this is your error, try running `aws sts get-caller-identity` in your local terminal.
    
-   This command asks AWS "can you tell me which credentials I'm using right now?" It should return your credentials' matching IAM user and account ID if your credentials are working.
    
-   If you get the same error (`The security token included in the request is invalid.`), you'll need to create a new AWS access key. The credentials you're using right now are invalid!
    
-   Hot Tip: Check out how to create access key credentials in the Unable to locate credentials tab.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/InvalidClientTokenId.png)

  

**ValidationException**

-   This usually means there's a typo in your Model_ARN.
    
-   Double check the ARN in your `.env` file matches exactly with what's in your text file.
    
-   Run `aws configure` in your local terminal, and check that `aws-region: us-east-2` is set correctly.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-6.png)

  

**ResourceNotFoundException: Knowledge Base does not exist**

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-8.png)

  

-   This usually means you're in the wrong AWS region!
    
-   Make sure you're in `us-east-2` (Ohio) region.
    
-   Run `aws configure` in your local terminal, and check that `aws-region: us-east-2` is set correctly.

-----


**Re-run API and Test /bedrock/query Endpoint**

-   You need to **restart** the API server for the changes to take effect.
    
-   Then, run the uvicorn command again to restart the server:
    

python3 -m uvicorn main:app --reload

-   Once the server is restarted, go back to your web browser and refresh the /bedrock/query URL you used before (e.g., http://127.0.0.1:8000/bedrock/query?text=What%20is%20NextWork).
    

> 🙋‍♀️ **Damn it, I still got an error!**  
> That's okay! Errors are normal, and you're learning!
> 
> -   Go back to your terminal, where the uvicorn server is running.
>     
> -   Press **Ctrl+C** to stop the running server.
>     
> 
> Head back to the top of the troubleshooting steps and pick the troubleshooting option that fits the error you're seeing.
> 
> If you're still stuck, [ask the NextWork community!](https://community.nextwork.org/c/i-have-a-question/?topics=7611)

**🎉 Awesome!** You've run the API and got a response from your RAG chatbot.

You've learned how to set up environment variables, run an API, and troubleshoot common errors. That's _so_ cool, look at you go! Nothing can stop you now, ready to run the full web app?


-----

## 💎 Mini Secret Mission

### Breaking Down the Web App

Now that you've fully tested the **backend API** that connects your web app with your chatbot, we've got a bit more to explore... We're about to start running the full web app!

Your mini secret mission, should you choose to accept it, is to 🕵️‍♀️ investigate 🕵️‍♀️ the code that makes your web app _work_.

We'll dive deep into each component of the web app (frontend, backend and data layer) and see how they come together to create a functioning web app with a chatbot interface.

  
  

**In this step, you're going to:**

-   Understand the differences between running the API (`main.py`) vs. the full web app (`web_app.py`).
    
-   Learn how your web app's code handles chat interactions.
    
-   Showcase **advanced understanding** of your web app's components in your documentation!
    

> 💎 **Secret Mission unlocked!**



Let's start by recapping the key components that makes up a web app...

  
  

**1️⃣ Frontend (The User Interface)**

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/three-tier-1.png)

  

Our web app's **frontend** lives in two main places in your project directory:

-   `templates/index.html` - The structure of our web page
    
-   `static/style.css` - How our web page looks
    

> 💡 **What does the frontend do?**  
> The frontend is responsible for:
> 
> -   Showing the chat interface to users.
>     
> -   Capturing user messages.
>     
> -   Displaying the chatbot's responses.
>     
> -   Making everything look nice with CSS styling.
>     

  
  

**2️⃣ Backend (The Processing Layer)**

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/three-tier-2.png)

  

Our web app's **backend** lives in two Python files in your project directory:

-   `main.py` - The core API that talks to Amazon Bedrock
    
-   `web_app.py` - A version of main.py that connects a frontend to the API
    
-   You don't need both files for the backend to run. We run one file at a time to see the difference between running just the API vs. a web app that also has a frontend.
    

> 💡 **What does the backend do?**  
> The backend handles all the behind-the-scenes work:
> 
> -   Receives messages from the frontend.
>     
> -   Sends queries to Amazon Bedrock.
>     
> -   Gets responses from the AI model.
>     
> -   Sends responses back to the frontend.
>     

  
  

**3️⃣ Data Layer (The Knowledge Base)**

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/three-tier.png)

  

Your web app's **data layer** consists of:

-   Your S3 bucket - stores the original documents.
    
-   Your Knowledge Base - processes the documents.
    
-   Your OpenSearch data store - stores the processed documents.
    
-   The AI model - generates human-like chat responses to user's questions.
    

> 💡 **What does the data layer do?**  
> The data layer is your app's "brain":
> 
> -   Stores all your documents.
>     
> -   Processes documents to make them searchable.
>     
> -   Uses AI to understand questions and generate responses.
>     
> -   That's why your **Knowledge Base** is the star of the data layer! While S3 and OpenSearch are also important for storing the data, it's the Knowledge Base that processes the documents and finds the useful information for your chatbot to use.
>     

  
  

**How They Work Together**

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/webapp-flow.png)

  

When someone asks your chatbot a question:

1.  **Frontend** captures the question and sends it to the backend.
    
2.  **Backend** formats the question into an API request and sends it to Amazon Bedrock.
    
3.  **Data Layer** i.e. the Knowledge Base sends relevant information from your documents to the AI model, which uses it to generate a proper chat response.
    
4.  **Backend** receives the chat response and sends it back.
    
5.  **Frontend** displays the response in a nice chat format.
    

  
  

**Examine `web_app.py`**

-   Switch tabs back to the [**GitHub repository.**](https://github.com/NatNextWork1/nextwork-rag-webapp/tree/main)
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-22.png)

  

-   Open the `web_app.py` file.

-----
Yayyy welcome to web_app.py! This file extends our basic API (main.py) with features needed to serve a web interface. Let's look at the key differences:  

-----
### More Tools Imported

`web_app.py` imports extra modules (lines 9-17):

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-40.png)

  

-   `from fastapi.responses import HTMLResponse`: For serving HTML responses.
    
-   `from fastapi.staticfiles import StaticFiles`: For serving static files like CSS and JavaScript.
    
-   `from fastapi.templating import Jinja2Templates`: For using Jinja2 templates to render HTML.
    
-   `import logging`: For logging application events.
    

> 💡 **What are these imports for?**  
> These imports help FastAPI, the framework we're using to build our API, handle web pages and files:
> 
> -   `HTMLResponse` - Lets FastAPI send full web pages (HTML) to the browser instead of just raw data (JSON).
>     
> -   `StaticFiles` - Helps serve files like images, CSS, and JavaScript so your web app looks and works properly.
>     
> -   `Jinja2Templates` - Lets you insert Python code into your HTML to create pages that change based on data or user input.
>     
> -   `logging` - Helps track errors and events in your app, making it easier to debug and see what’s happening behind the scenes.
>     

-   To explore more of the `web_app.py` file, you can jump back ⬆️ to the top of these tabs!


------
### Logging setup


`web_app.py` also includes some additional setup for logging (lines 19-24)!

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-41.png)

  

> 💡 **Why do we need this configuration?**
> 
> -   Logging helps us track what's happening in our app - like having a security camera recording everything! This can be helpful for debugging and monitoring the application.
>

------

### Environment Variables



`web_app.py` loads an extra environment variable (line 26).

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-42.png)

  

-   `MODEL_ID = os.getenv("MODEL_ID")` loads the `MODEL_ID` environment variable, which tells Bedrock which AI model to use when generating responses.

----
### Static Files & Templates



`web_app.py` also adds code to serve static files (like CSS and JavaScript) and HTML templates from line 38:

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-43.png)

  



```python
# Configure static files and templates
app.mount("/static", StaticFiles(directory="static"), name="static")
templates = Jinja2Templates(directory="templates")

```

-   `app.mount("/static", StaticFiles(directory="static"), name="static")`: This line tells FastAPI to serve static files from the `static` directory at the URL path `/static`.
    
-   `templates = Jinja2Templates(directory="templates")`: This initializes Jinja2 templates, which are used to render HTML files from the `templates` directory.
    

> 💡 **Why do we need this configuration?**
> 
> -   Logging helps us track what's happening in our app - like having a security camera recording everything
>     
> -   Static files configuration tells FastAPI where to find things like CSS and JavaScript.
>     
> -   Templates configuration sets up our HTML template system - like setting up a document template in Microsoft Word
>     
> -   Model configuration lets us choose which AI model to use - like picking which brain our chatbot will use
>

------

### Chat Interface



-   `web_app.py` adds a new API endpoint that talks directly to the AI model (line 56):
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/invoke.png)

  

> 💡 **How does this compare to the Knowledge Base endpoint?**
> 
> -   The `/bedrock/query` endpoint in `main.py`:
>     
>     -   First searches your documents for relevant information.
>         
>     -   Then asks the AI to generate an answer using that information.
>         
>     -   Results are more accurate for questions **about your specific documents**.  
>           
>         
> -   This new `/bedrock/invoke` endpoint in `web_app.py`:
>     
>     -   Skips the document search completely.
>         
>     -   Asks the AI model directly, like ChatGPT.
>         
>     -   **Better for general questions,** but won't know about your specific documents.
>

-------



  


    

✋ These additions in `web_app.py` are what let it serve the web app interface, handle user interactions, and display the chatbot in a browser.


Next up, let's look at the `index.html` file that sets up the structure and content of our web app's user interface. In other words, it's the frontend that `web_app.py` is serving!

  
  

-   In your **GitHub repository**, head to the `templates` folder and open the `index.html` file.
    
-   Scroll down to the bottom of the `index.html` file. You'll find a `<script>` section containing JavaScript code from line 156 - this code creates the chat interface!
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-45.png)

  



```javascript
const endpoint = "/bedrock/query";

function sendMessage() {
    // Get user input
    const inputField = document.getElementById("user-input");
    const message = inputField.value;
    
    // Clear input field
    inputField.value = "";
    
    // Send to API and handle response
    fetch(`${endpoint}?text=${encodeURIComponent(message)}`)
        .then(response => response.json())
        .then(data => {
            // Display response in chat window
            displayMessage("You", message);
            displayMessage("Bot", data.response);
        });
}

```

> 💡 **How does this code work?**  
> Think of this JavaScript code like a postal service:
> 
> 1.  When you type a message and hit send, it's like putting a letter in an envelope.
>     
> 2.  The code sends that envelope to our API (the `endpoint`).
>     
> 3.  When it gets a response back, it's like opening a reply letter.
>     
> 4.  Finally, it displays both your message and the response in the chat window.
>     

This JavaScript code is responsible for handling user interactions in the web app. Let's look at some key parts:

-   `const endpoint = "/bedrock/query";`: This line defines a JavaScript constant `endpoint` and sets it to `"/bedrock/query"`. This is the API endpoint that the web app will use to send queries to the Bedrock chatbot API.
    
-   `function sendMessage() { ... }`: This function is called when the user sends a message (e.g., by pressing Enter or clicking a send button). It does the following:
    
    1.  Gets the user's input text from the input field.
        
    2.  Sends a `GET` request to the API endpoint (`/bedrock/query`) with the user's text as a query parameter (`text`).
        
    3.  Receives the response from the API.
        
    4.  Displays the user's message and the chatbot's response in the chat interface.
        

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-45.png)

  

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-46.png)

  



**How It All Fits Together**

Here's how all these pieces work together:

1.  When you open the chat in your browser, FastAPI serves the `index.html` template
    
2.  The JavaScript code in `index.html` handles your chat interactions
    
3.  When you send a message, JavaScript makes an API call to `/bedrock/query`
    
4.  The API (powered by `web_app.py`) processes your message using Bedrock
    
5.  The response comes back and JavaScript displays it in your chat window
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-46.png)

  



**🎉 Secret Mission Accomplished!** You now understand how our web app works under the hood. This knowledge will help you customize and enhance the chatbot interface in the future!

----

## Step #5

### Running the web app

Now that we have the API running, we'll run the web app, and interact with the chatbot through the web interface.

  
  

**In this step, you're going to:**

-   Run the web app using `uvicorn` with `web_app.py`.
    
-   Access the web app in your browser and interact with the chatbot.
    
-   Add the `MODEL_ID` environment variable to your `.env` file.
    
-   Test how the chatbot's responses change based on whether RAG is enabled or not.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/architecture-5.png)

  



**Run the web app**

-   Go back to your terminal.
    
-   If the `uvicorn` server is still running, press **Ctrl+C** to stop it.
    
-   Run the following command to start the `uvicorn` server, but this time, specify `web_app:app` instead of `main:app`:
    



```bash
python3 -m uvicorn web_app:app --reload

```

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-47.png)

  

This command is similar to the one we used to run `main.py`, but it tells `uvicorn` to load the FastAPI application from `web_app.py` instead.

  
  

**Open web app in Browser**

-   Once the `uvicorn` server for `web_app.py` is running, open your web browser.
    
-   Go to the same URL as before (usually `http://127.0.0.1:8000`).
    

  
  

This time, instead of just seeing a JSON message, you should see the full web app interface!

![Looking good!](https://learn.nextwork.org/projects/static/ai-rag-webapp/webapp.png)

Looking good!

  

  
  

**Test the Chatbot**

-   On the homepage, select **Chat with my projects**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-48.png)

  

-   You'll be taken to the chat window.
    
-   Start by saying hello!
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/hello.png)

  

-   Next, let's ask `Who is NextWork?`
    
-   Wait for the chatbot to respond. It should give you an answer based on the documents in your Knowledge Base.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/success.png)

  

-   Yayyyyyyy!! Your entire web app is working! 😭🙏
    

> 💡 **How does the web app work?**  
> When you type a question in the chat interface and send it, the web app does the following:
> 
> 1.  **Sends the question to the FastAPI API:** The web app sends your question to the API endpoint we tested in Step #6 (`/bedrock/query`).
>     
> 2.  **API queries Bedrock Knowledge Base:** The FastAPI API receives the question, and uses the Bedrock command we used in Step #4 to query your Knowledge Base with the question.
>     
> 3.  **Bedrock retrieves and generates response:** Bedrock searches your Knowledge Base for relevant information and uses the Llama 3.3 70B Instruct model to generate a human-like response based on the retrieved information.
>     
> 4.  **API sends response back to web app:** The FastAPI API sends the response from Bedrock back to the web app.
>     
> 5.  **Web app displays response:** The web app displays the response in the chat interface for you to see.
>     



**Experiment with "Talk to AI directly"**

-   Check the **Talk to AI directly** checkbox below the chat input box.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-54.png)

  

> 💡 **What is "Talk to AI directly"?**  
> The **Talk to AI directly** checkbox controls whether the chatbot uses **Retrieval-Augmented Generation (RAG)** or not.
> 
> -   **Checked (Talk to AI directly):** When checked, the chatbot will **bypass** the Knowledge Base and talk directly to the AI model (Llama 3.3 70B Instruct). In this mode, the chatbot will answer questions based on its general knowledge, without using your specific documents.
>     
> -   **Unchecked (RAG enabled):** When unchecked, the chatbot will use RAG. It will first search your Knowledge Base for relevant information, and then use the AI model to generate a response based on the retrieved information. This mode lets your chatbot to answer questions specifically based on your documents, making it more accurate and grounded in your knowledge base.
>     

-   Type the same question again: `Who is NextWork?` and press **Enter** or select the send button.
    
-   Hmmm.... no response yet!
    
-   To troubleshoot this, let's check the logs in your terminal.
    
-   **Oops!** The terminal says `500 Internal Server Error`. Looks like there's an error in the API...
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/500.png)

  

-   Copy the API endpoint that's causing the error.
    
-   Add the endpoint to the end of your web browser's URL, i.e. `http://127.0.0.1:8000/bedrock/invoke?text=Who%20is%20NextWork`
    
-   Interesting! You might see an error message like `{"detail":"Model ID is missing"}`.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/modelid.png)

  

-   This is because we haven't configured the `MODEL_ID` environment variable yet. Let's fix that next.
    

> 💡 **Recap: What is `MODEL_ID`?**  
> `MODEL_ID` is the ID of the AI model **to call it directly.** It's a simpler ID that just names the model, without any region or account information. That's why it's called an ID, not a Model ARN!
> 
> While you need an ARN to query your Knowledge Base (because an ARN includes permissions and configurations for RAG), you only need an ID to query the AI model directly.

  
  

**Add `MODEL_ID` to `.env` File**

-   Go back to your terminal where the API is running.
    
-   Press **Ctrl+C** to stop the API server.
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-147.png)

  

-   Run the following command to open the `.env` file:
    


```bash
nano .env

```

-   In the `.env` file, add a new line for `MODEL_ID`.
    
-   **Can't find your model ID?** 👀 You can extract the Model ID from the Model ARN! The Model ID is the part after `model/` in the ARN
    
-   Add the `MODEL_ID` line to your `.env` file. Your complete file should look similar to this:
    

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-150.png)

  

-   Save the `.env` file - the instructions for this depend on your operating system:  
      
    

### MacOS/Linux

-   In nano:
    
    -   Press `Ctrl + X`
        
    -   Press `Y` to confirm.
        
    -   Press `Enter` to save.
        

![](https://learn.nextwork.org/projects/static/test_project_full/screenshot-130.png)

  

**Verify Environment Variables**

-   Check that your `.env` file was updated correctly:
    



```bash
cat .env

```

-   You should see the `MODEL_ID` line in your terminal!
    

![](https://learn.nextwork.org/projects/static/ai-rag-api/cat.png)

  

> 🙋‍♀️ **I don't see my environment variables!**  
> If you don't see your environment variables:
> 
> 1.  Make sure you saved the `.env` file in the correct location (your project directory)
>     
> 2.  Check that the file name is exactly `.env` (including the dot)
>     
> 3.  Try creating the file again using a different text editor
>     

  
  

**Restart the Web App**

-   Restart your web app:
    


```bash
python3 -m uvicorn web_app:app --reload

```

  
  

**Open web app in Browser**

-   Once the `uvicorn` server for `web_app.py` is running again, open your web browser.
    
-   Go to the same URL as before (`http://127.0.0.1:8000`).
    
-   On the homepage, select **Chat with my projects**.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-48.png)

  

-   In the chat input box, check **Talk to AI directly** and ask `Who is NextWork?`
    
-   Wait for the chatbot to respond. It should give you an answer that's... a little less accurate. That's because the chatbot is now using the AI model directly, without using your Knowledge Base!
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/screenshot-53.png)

  



![](https://learn.nextwork.org/projects/static/ai-rag-webapp/success.png)

  

**Awesome! You've successfully run your RAG chatbot web app and chatted with it!** You've seen how the chatbot responds to questions based on your knowledge base when RAG is enabled, and how it responds based on general AI knowledge when RAG is disabled 😤💪

You've now built a fully functional RAG chatbot from scratch!



------


  
## 💎 Secret Mission

### Customizing the Web App (Secret Mission)

Ready for a secret mission? In this optional step, you'll get to customize the look and feel of your web app! We'll use ChatGPT to generate a new frontend design for our chatbot interface, and then integrate it into our project.

  
  

**In this step, you're going to:**

-   Use a ChatGPT prompt to generate a new HTML file or modify the existing `index.html`.
    
-   Integrate the generated HTML into your project.
    
-   Test your customized web app.
    

> 💎 **Secret Mission unlocked!**


  
  

**Create new index.html with ChatGPT**

-   Open [ChatGPT](https://chatgpt.com/) (or your preferred AI assistant, like Claude or Gemini).
    
-   Use the following prompt (or a similar one) to ask ChatGPT to generate a new HTML file for your web app.
    
-   Make sure to attach the original `index.html` and `style.css` files to the prompt:
    
    -   Right click on the links and select `Save as...` to download it.
        
    -   [Original index.html](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Turn%20Your%20Data%20into%20an%20AI%20Chatbot/index.html)
        
    -   [Original style.css](https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Turn%20Your%20Data%20into%20an%20AI%20Chatbot/style.css)
        


```text
I have attached the original index.html file (along with style.css) that implements a chat application using API calls (to endpoints like /bedrock/invoke and /bedrock/query). I'd like you to generate a completely custom HTML frontend that:

1. Retains the same API integration:
   - Use the same mechanisms for triggering the API (i.e. send chat messages via the same endpoints as in the original index.html).
   - Ensure that only the expected user text is sent (i.e. avoid prepending extra system prompts to the API request if it might break the backend).

2. Provides a new visual design:
   - The design should be entirely different from the original.
   - You may override the provided style.css by writing new CSS code directly in the index.html (i.e. adding inline styles or a <style> block) to achieve the custom aesthetic, whether it's whimsical, minimalist, or any other style—all while keeping the API integration unchanged.

3. Is plug-and-play:
   - The new frontend must work with the existing backend API without changes.
   - All necessary JavaScript (for sending messages, displaying loading indicators, and updating the chat window) should be included in the HTML.

Please produce a complete, self-contained HTML file that implements this new frontend while ensuring that the API function calls and error handling remain the same as in the attached original index.html.


```

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-14.png)

  

-   You can adjust this prompt to use your desired design, colors, layout, and features. Be creative and experiment!
    

> 💡 **Why use AI tools like ChatGPT?**  
> AI tools like ChatGPT can be helpful for quickly prototyping and generating code, including HTML, CSS, and JavaScript for web interfaces. While the code generated by AI might not always be perfect or production-ready, it can give you a great starting point and save you a lot of time in creating a basic UI design. You can then further customize and refine the generated code to fit your exact needs. We'd highly recommend going back and forth with the AI to provide feedback and refine the code until you're happy with the result!

-   Let's send off the prompt. Off it goes!
    

  
  

While we wait for ChatGPT to generate the code...

> 💡 **Recap: What are the components of our web app's code?**  
> Our web app's code is built with two main parts:
> 
> -   **Frontend (index.html)**
>     
>     -   The user interface that people interact with
>         
>     -   Written in HTML, CSS, and JavaScript
>         
>     -   Handles displaying messages and collecting user input
>         
>     -   Makes API calls to the backend
>         
> 
>   
> * **Backend (web_app.py)** - Processes requests from the frontend - Communicates with Amazon Bedrock - Returns responses to the frontend - Manages all the business logic
> 
>   
> Note: The data layer is so important to our web app too - we've already set up a **Bedrock Knowledge Base** and an **Amazon S3 bucket** to store our documents, so we don't need to write the data layer code ourselves!
> 
>   
> 💡 **Why can we safely change the frontend?**  
> The frontend and backend are **loosely coupled** - they only communicate through the API you've set up in `web_app.py`:
> 
> -   The frontend makes HTTP requests to specific URLs (like `/bedrock/query`)
>     
> -   The backend processes these requests and sends back responses
>     
> -   As long as we keep using the same API endpoints in our new frontend design, the application will continue to work
>     
> -   This means we can completely redesign how the chat interface looks without touching any of the backend logic!
>     



  
  

**Integrate Generated HTML**

-   While we wait for ChatGPT to generate the HTML code, find `index.html` in your project. It should be in your project's `templates` folder.
    
-   Open `index.html` in a code editor, like VS Code or Cursor. If you don't have a code editor, you can use the text editor built into your operating system e.g. TextEdit on Mac or Notepad on Windows.
    
-   Now, you can either wait until ChatGPT is done generating the code, or you can see an example update to `index.html`!  
      
    

I'll just wait for the code to finish generatingSee an example of a custom frontend

-   All good! You can always switch to the next tab to see this example frontend in action.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-12.png)

  

**Update index.html with ChatGPT's code**

-   Head back to your ChatGPT tab.
    
-   Once ChatGPT is done generating the HTML code, you can copy the generated code.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-19.png)

  

-   Head back into your code editor, and replace everything inside your existing `index.html` file with it.
    

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/new-18.png)

  

-   Make sure to save `index.html`.
    

  
  

**Test Customized web app**

-   Once you've saved your updated `index.html`, refresh the tab running your web app.
    
-   You should now see your customized web app interface!
    
-   Test it out by sending messages and interacting with the chatbot. Make sure all the features (chat window, input field, send button) are working as you expected.
    

> 🙋‍♀️ **Ah dang it! I ran into an error**  
> It's totally normal to run into errors with AI generated code! You can troubleshoot the error by:
> 
> 1.  Checking for a specific error message in your terminal.
>     
> 2.  Copying the error message and sending it to ChatGPT to get help.
>     
> 3.  Paste any updated index.html code back into your code editor and save the file.
>     
> 4.  Refresh your web browser and test again.
>     

  
  


**Woop woop! Secret mission accomplished - you've customized your web app interface!**

-----

  
## 🗑️ Before you go

### Delete your resources

Now that we've built and tested our chatbot, it's time to clean up the resources we created. This is important to avoid getting charged for unused resources.

  
  

**Resources to delete:**

Delete the **Bedrock Knowledge Base**.

Delete the **S3 bucket**.

Delete the **IAM access key**.

Delete the **OpenSearch Serverless collection** (vector store).

Deactivate the **virtual environment** and delete your cloned repository.


------
## 🎉 Mission Accomplished

### That's a wrap!

Nice work! 🤖 You've just built a powerful RAG chatbot web app using Amazon Bedrock.

![](https://learn.nextwork.org/projects/static/ai-rag-webapp/architecture-complete.png)

  

**You've learned how to:**

-   🚀 Set up and configure AWS services:
    
    -   Create an S3 bucket for document storage
        
    -   Configure a Knowledge Base in Amazon Bedrock
        
    -   Set up secure AWS credentials and access
        

  
  

-   🤖 Work with AI and RAG:
    
    -   Request access to AI models in Bedrock
        
    -   Create a RAG-powered chatbot
        
    -   Test and experiment with different AI responses
        

  
  

-   💻 Build a web app:
    
    -   Set up a Python development environment
        
    -   Create a FastAPI web app
        
    -   Build an interactive chat interface
        
    -   Configure environment variables
        
    -   Debug and troubleshoot your application
        
    -   (💎) Completely redesign your web app's frontend


------
