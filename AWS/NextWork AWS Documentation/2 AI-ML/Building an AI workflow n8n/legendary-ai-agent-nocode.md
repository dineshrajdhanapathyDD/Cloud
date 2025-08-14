<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build Your First AI Workflow



**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

## Building an AI Workflow

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/ai-agent-nocode_sdrjg8e123dv)

---





Let's build a workflow that uses AI to manage your calendar!


## Summary

Welcome to this project on building an AI workflow!

AI workflows are truly where automation 🤝 meets 🤝 intelligence.

This project is a great way to build your skills for roles like **Backend Developer**, **Automation Engineer**, **AI Specialist**, or **Project Manager**, where it's important to know how to use AI to become more efficient.

### What we're building today...

How do you add a new event in your calendar? 📆

Chances are, you have to open up your calendar app, select a start and end time, write an event title, click save, then close the app again 😮‍💨 Calendar management can really add up - imagine doing this multiple times a day, especially if you're constantly booking meetings or adding events!

We're going to build an AI workflow to solve this problem.

By the end of this project, you can add an event just by sending a text to your workflow, which is going to be your AI calendar assistant. Watch your assistant create calendar events for you straight away!





### Let's get ready to...

🚀 Set up an AI workflow using **n8n.**

🤖 Integrate **ChatGPT** and your calendar to your workflow.

💎 Level up your AI workflow skills with **prompt engineering!**

----
In this project, I will demonstrate setting up an AI workflow using n8n. I'm doing this project to learn how to integrate ChatGPT and my calendar, while also leveling up my prompt engineering skills!

-----
## ✍️ Step #1

### Sign up for n8n

  

To build our workflow, we need to set up our workspace.

We'll use a tool called **n8n** to set up a workflow from scratch and connect different services like ChatGPT and Google Calendar! 🏡

  
  

**In this step, you're going to:**

-   Sign up for n8n (for free).
    
-   Set up your first workflow.
    



  
  

**Sign up for n8n**

-   Head to the [**n8n website.**](https://n8n.io/)
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-1.1.png)

  

> 💡 **What is n8n?**  
> **n8n** is a no-code platform that helps you automate tasks.
> 
> You automate a task on n8n by connecting different applications and setting up how you'll move data between them. For example, an automation can automatically send an email to all new email addresses you add to a spreadsheet in real time!
> 
> The awesome thing about n8n is that it's easy to use, even if you don't know how to code. You can create workflows by dragging and dropping blocks.
> 
>   
> 💡 **What is a workflow?**  
> A workflow is a set of steps designed to complete a task. **Automating** a workflow means the steps can happen on their own without you needing to do things manually, which saves you time and reduces errors.
> 
> A workflow becomes an **AI workflow** when it integrates AI to automate tasks or decision-making. For example:
> 
> -   Using **image recognition** to sort and categorize photos you upload to a folder.
>     
> -   Using **predictive analytics** to forecast sales trends in a generated monthly report.
>     
> -   Using **generative AI** to automatically draft a reply to new emails in your inbox.
>     


-   Select **Get started for free.**
    
-   Off we go!
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-1.2.png)

  

-   Enter your details to start a free trial. **You won't be asked for any payment or card details.**
    

> 💡 **What do I get for free?**  
> The free trial gives you access to n8n's platform for 14 days, and lets you build up to 5 workflows! We'll only be building one today, so we won't need to upgrade from the trial.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-1.4.png)

  

> 🙋‍♀️ **My account name is getting rejected**  
> Your n8n **Account name** has to be completely unique - think of it as your account's unique ID! If your first one gets rejected, try again until it gets accepted.
> 
> ![](https://learn.nextwork.org/projects/static/ai-agent-nocode/unframed/step-1.3.png)
> 
>   

  
  

**Set Up Your First Workflow**

-   Awesome work! Once you've created your signup details, you'll need to answer a few questions.
    
-   These questions include:
    
    -   **What team are you on?** If you're unsure, you can select **Other** and enter `Student`
        
    -   **What is the size of your company?** Since we're here to learn, you can select the last option i.e. **I'm not using n8n for work**.
        
    -   **Have you used any of these tools before?** Select any of the tools you've used before, or go for **No** if workflows and automation are new to you!
        
    -   **How did you hear about n8n?** Feel free to select **Other** and enter `NextWork project` 😏
        

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-1.9.png)

  

-   In the next page, select **Skip**. We won't need to invite others to your account!
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-1.10.png)

  

-   Once your account is all set up, select **Start automating.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-1.11.png)

  

Nice work! This kicks off your free trial of n8n, which should last 14 days.


> 🤫 P.S. n8n also comes in a **Community Edition,** which is completely free to use with no trial or credit card required. The Community Edition takes longer to set up, so we'll save that for later projects in this AI Agent series! For now, we'll focus on diving into workflows as soon as we can.

**Your Quick n8n Tour**

Welcome to your n8n workspace!

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-1.12.png)

If you'd like, you can switch to the dark mode of n8n!



>>> 🌙Skip dark mode ⏭️

#### Set up dark mode 

-   Select the three dots on the bottom left corner of the workspace.
    
-   Select **Settings**.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-1.13.png)

  

-   Scroll to the bottom of the page.
    
-   Under **Personalisation**, change the theme to **Dark theme.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-1.14.png)

  

-   Select **Save.**
    

> 🙋‍♀️ **The Save button isn't working for me!**  
> You might have a profile field that isn't filled out yet.
> 
> Scroll back up your profile page - is the **Last Name** field blank?
> 
> ![](https://learn.nextwork.org/projects/static/ai-agent-nocode/unframed/step-1.16.png)
> 
>   

-   Once you're ready, select the **<- Settings** button to head back to the main workspace.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-1.17.png)

-----


## ✨ Step #2

### Start a new workflow

  

Now that we have n8n set up, let's set up a workflow from scratch!

A workflow is a chain of tools and actions that we automate. In this case, we're going to automate the process of booking new events into your digital calendar (ooo exciting)!

Let's see how we can start this workflow in n8n.

  
  

**In this step, you're going to:**

-   Create a new **workflow** in n8n.
    
-   Add a **chat trigger** to the workflow - this sets up how you'll send instructions to your workflow!
    



  
  

**Create a new workflow**

-   Back in your n8n workspace, select **Start from scratch.**
    

> 💡 **What's the other option?**  
> You might notice that the other option is to **Test a ready-to-go AI Agent example.** n8n also has a library of templates that you can use to speed up developing AI agents and workflows.
> 
> We'll stick with building from scratch, but you can definitely explore [workflow templates](https://n8n.io/workflows) when you're ready to build another AI workflow!

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-2.1.png)

  

  
  

**Your first workflow**

Welcome to your first workflow!

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-2.3.png)

  

-   Let's start by selecting **Add first step** in the middle of your canvas.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-2.4.png)

  

-   Here, you're asked for your workflow's **trigger.**
    

> 💡 **What is a workflow trigger?**  
> A workflow trigger is like a starting point for a workflow.
> 
> It's what tells the workflow to begin. It can be something that happens at a **specific time,** like every hour, or something that happens because of an **event,** like getting a new email.

-   Select **On chat message**.
    

> **💡 What does this trigger do?**  
> We're using n8n's built-in chat window for our workflow, because it's the easiest one to test with. With this trigger, your workflow runs every time you enter a chat message! n8n will set up the chat window for you in just a second.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-2.6.png)

  

  
  

**Set up your Chat Trigger**

-   You're now in your chat trigger's setup!
    
-   This is where you can set up your trigger to be available publicly e.g. if you integrated the chat window into an app or website.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-2.7.png)

  

-   We won't be using this setting for now (to keep things simple), so select **Back to canvas**.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-2.8.png)

  


  
  

**Test your Chat Trigger**

We don't have your workflow set up yet, but a great feature of **n8n** is that you can constantly test your workflow, and even isolate testing single parts of the workflow.

-   At the bottom of the canvas, select **Chat**.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-2.9.png)

  

-   Send your first chat message: `Hello`
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-2.10.png)

  

-   n8n throws you an error.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-2.11.png)

  

That's okay! We haven't set up anything in the workflow to process a chat message yet. At least we've confirmed that we have a chat window for triggering the workflow!


-----

## 🧠 Step #3

### Integrate AI

  

Now that our workflow has a chat to receive instructions, we'll add the "brain" of our workflow: an AI Model.

The AI model will be responsible for turning chat commands like "book a meeting for tomorrow 10am" into instructions for scheduling events.

  
  

**In this step, you're going to:**

-   Integrate AI to your workflow.
    



  
  

**Connect a new node**

-   Select the **+** button to add a new node.
    

> 💡 **What is a node?**  
> **Nodes** are the key building blocks of a workflow. They can do a range of things, from triggering a workflow, to processing data, and to fetching data. Every block you add to your workflow is a node.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-3.1.png)

  

-   From the list of options, select **Advanced AI.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-3.2.png)

  

-   Select **AI Agent.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-3.3.png)

  

> 💡 **Hold on, are we creating an AI agent?**  
> Ah, great question! Here's where it gets a little tricky - while the node we're adding here is called an "AI agent", what we're building won't qualify as an actual AI agent.
> 
> An **AI agent** is a system that doesn't need any triggers to act. Agents gather data to decide what to do and act on their own.
> 
> What we're building has a **trigger** i.e. a chat message being sent, which means we're building an AI **workflow** instead. As a recap, an AI workflow runs a series of **predefined** tasks that's integrated with AI.
> 
> The node is called an **AI agent** because it can become autonomous if you make it complex enough, but that's not how we're using it today. We'll continue referring to the node as an **AI Agent** so you can identify it in your n8n canvas, but it's a good idea to differentiate AI workflows vs agents!
> 
> P.S. The definition of an AI agent vs. workflow is becoming a growing discussion in the world of AI. [You can read more here if you're interested!](https://www.anthropic.com/research/building-effective-agents)

  
  

**Configure the AI Agent node**

Welcome to your AI Agent setup page!

As a quick rundown, the setup page is split in three parts:

1.  The left hand side represents the **inputs** i.e. the chat messages you send that triggers your workflow.
    
2.  The middle section represents the AI agent's **setup**.
    
3.  The right hand side represents the **outputs** i.e. the actions or results your agent will deliver.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-3.4.png)

  

  
In the middle section, we'll make sure that:

The agent is a **Tools Agent.**

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-3.7.png)

  

> 💡 **What is a Tools Agent?**  
> A **Tools Agent** means the Agent will connect with third party tools (like Google Calendar) to complete specific tasks.
> 
>   
> 💡 **Extra for PROs: What are the other Agent options?**  
> You might notice that there are multiple agent types:
> 
> -   A **Conversational Agent** is designed to translate prompts into API calls and JSON data. An AI workflow with a Conversational Agent could handle customer service inquiries, translating user queries into API calls that fetch account information or track order status.
>     
> -   An **OpenAI Functions Agent** uses built in OpenAI functions, like image generation. An AI workflow with an OpenAI Functions Agent could generate marketing materials by creating images and text content tailored to your inputs.
>     
> -   A **Plan and Execute Agent** creates a high-level plan for complex tasks and then executes each step. This is great for more complex workflows. An AI workflow with a Plan and Execute Agent could organize a complex event, coordinating venue bookings, speaker schedules, and attendee notifications step-by-step.
>     
> -   A **ReAct Agent** works by thinking about a problem, taking an action, and then using the results of that action to think about the problem again. This process repeats until the problem is solved. An AI workflow with a ReAct Agent could optimize energy consumption in smart homes by adjusting settings in real-time based on usage patterns and external weather conditions.
>     
> -   An **SQL Agent** specializes in working with SQL databases e.g. extracting insights. An AI workflow with an SQL Agent could perform monthly data cleanups in a database, ensuring data integrity and optimizing performance by running diagnostic queries and applying fixes.
>     

The **Source for Prompt** is a **Connected Chat Trigger Node.**

> 💡 **What is the Source for Prompt?**  
> The **Source for Prompt** tells you where the AI agent gets its information. In our case, it's the chat window.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-3.6.png)

  

-   Select **Back to Canvas.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-5.png)

  

> 💡 **What are the three different sections underneath the AI agent?**  
> An AI agent is made of three key parts that you set up individually:
> 
> -   The **Chat Model** is the AI agent's brain, trained to analyze data to make decisions.
>     
> -   The **Memory** section stores data, past interactions, and learned information. This helps the AI agent learn from its past experiences and make better decisions over time.
>     
> -   The **Tool** section are the third party software your agent will use. You can also use tools to enhance your AI agent, like using tools that help the AI communicate and speak in a different language.
>     
>     A tool in this workflow would be Google Calendar, because the workflow needs it to schedule new events.
>     



  
  

**Set up your Chat Model**

-   Select the **+** for your agent's **Chat Model.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-3.8.png)

  

-   Select the `OpenAI Chat Model`
    

> 💡 **What is a chat model?**  
> A chat model is a type of artificial intelligence (AI) that can understand and respond to text.
> 
> It's like a computer program that can have conversations with you. You type in a message, and the chat model uses its knowledge to understand what you're saying and generate a response.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-3.9.png)

  

On to your chat model's setup!

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-3.png)

  

-   Select **Claim credits** at the top of the setup panel.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-3.11.png)

  

> 💡 **What am I claiming?**  
> Normally, if you want to use OpenAI’s services (e.g. using its chat model in your workflow), you need to set up access through their API, which means setting up API keys and paying for API requests your workflow makes. This process can be time-consuming and costs you money!
> 
> Claiming the 100 free credits is like setting up a paid API account. This lets you start using OpenAI's chat model right away.
> 
>   
> 💡 **What do "100 API credits" mean?**  
> Having 100 API credits means you can send 100 separate requests to the API. In other words, 100 chat messages with your chat model.



-   Your setup should auto-fill now.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-3.12.png)

  

-   The **Credential to connect with** setting should say **n8n free OpenAI API credits**.
    
-   The **Model** setting should say **gpt-4o-mini** model.
    

> 💡 **There are multiple OpenAI models?**  
> Yup! OpenAI offers different AI models. Each model is made for different jobs. Some models are good at simple tasks like finishing sentences, while otherse are better at complex tasks like understanding conversations. We'll be using their simplest model, which still works perfectly for simple tasks like creating calendar events.
> 
> You can even check out OpenAI's own breakdown [here.](https://platform.openai.com/docs/models/overview)


-   Select **Back to Canvas.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-4.png)

  
-----

## 🗓️ Step #4

### Connect to Google Calendar

  

You're getting really close! Next up, let's add calendar access for your AI agent.

  
  

**In this step, you're going to:**

-   Add a connection to Google Calendar.
    
-   Test your workflow.
    



  
  

**Add and connect the Google Calendar node**

-   Select the **+** button for your AI Agent's **Tool.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.1.png)

  

> 💡 **Recap: What is a Tool in my AI Agent?**  
> A Tool is a piece of code or third party software that the agent can use to do a task.
> 
> Tasks could include retrieving data from a database, or in our case, creating an event in an external calendar (Google Calendar).

-   Search for `Google Calendar` and select it. We're going to use it to create new events in your calendar!
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.2.png)

  

> 🙋‍♀️ **I don't use Google Calendar**  
> You can also try this project using `Outlook`, and use the exact same setup over the rest of this project!
> 
> ![](https://learn.nextwork.org/projects/static/ai-agent-nocode/unframed/step-4.4.png)
> 
>   



-   Now you're in your Google Calendar tool's set up page!
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.3.png)

  

-   Under **Credential to connect with**, select **+ Create new credential.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.5.png)

  

-   Select **Sign in with Google**.
    

> **💡 Why do I need to sign in with Google?**  
> This authorization lets your workflow act on your behalf, adding and checking events in your Google Calendar.
> 
> Without this authorization, your workflow can't access your calendar or do it's job.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.6.png)

  

-   Select the account that's connected to a Google Calendar you use.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.9.png)

  

-   Allow n8n access to both your **events** and **calendars.** Your workflow will need this to create new events in the correct calendar.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.14.png)

  

> 🙋‍♀️ **I don't want to give away access**  
> You can remove access very easily at the end of this project - we'll show you how. Once access is removed, n8n will not be able to add or edit items in your calendar.

-   Select **Continue.**
    
-   Once you're all connected, you'll see a success message that says:  
    **Got connected. The window can be closed now.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.11.png)

  

-   Close the tab, and head back to **n8n.**
    
-   Nice - you're all connected to your Google account!
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.12.png)

  


-   Select the **x** icon on the top right corner.
    
-   Double check the default settings for your Google Account tool:
    

The **Tool Description** is **Set Automatically.**

The **Resource** is **Event**.

The **Operation** is **Create**.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.13.png)

  

> 💡 **What do these default settings mean?**
> 
> -   Tool Description is **Set Automatically**: This option means n8n will automatically write the prompts that instruct the AI agent on how to use this tool. You'd write this manually when you become more familiar creating workflows (hint: we're doing this in the next project... 👀)
>     
> -   Resource is **Event**: This tells the tool that it should focus on handling calendar **events**, instead of trying to create and edit the calendar itself.
>     
> -   Operation is **Create**: The tool's main job is to put new events into your calendar. There are other operations available, like **Get** and **Update**, which you could add to make your workflow do even more things and become more useful.
>     

-   From the **Calendar** list, select you calendar.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.15.png)

  

-   Head back to your canvas.  
      
    

  
  

Great! You have your AI chat model _and_ calendar now set up.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-7.png)

  

  
  

**Test Your Workflow**

The moment of truth! Let's test our calendar workflow and see if it can create an event.

-   Select the **Chat** button again.
    
-   Start the conversation with `Hello` again.
    
-   Wooo! This time, our chat responds back. This is because the Chat Model, the brains of our workflow, is in place.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.17.png)

  

-   Now try to book a time in your own calendar.
    
-   Open your [Google Calendar.](https://calendar.google.com/)
    
-   Look for a 1-hour slot that's **free** (i.e. empty in your calendar) for tomorrow.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.19.png)

  

-   Head back to your chat window, and ask your workflow that you'd like to book that time. Make sure you mention `tomorrow` in the request.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-4.18.png)

  

-   Hmm... your AI model says that time is not available. That doesn't seem right.
    



We'll have to investigate what went wrong. For now, don't forget to **Save** your workflow's progress.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-8.png)

-----
## 🧪 Step #5

### Troubleshoot Your Workflow

  

Your AI workflow tells you you're busy, at a time when you're actually free!

Why is that?

Let's investigate your AI model's setup and try fix it together.

  
  

**In this step, you're going to:**

-   Analyze your AI workflow's logs.
    
-   Troubleshoot an error in your Calendar tool's setup.
    
-   Test your chat again.
    



  
  

**Analyze your AI agent's logs**

-   Let's try to fix the error in your workflow by investigating your AI agent's logs.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-5.1.png)

  

-   ✋ **PAUSE**
    
-   Would you like to try finding the error yourself first?
    

  
  

### I'll hunt for this bug myself

You got it! Try find the error in your AI Agent's logs 🕵️‍♀️

You can always reveal the answer at any time.


You got this! Testing and running into errors are big parts of the learning journey. We'll investigate how we can fix this, and learn some cool things along the way 😎

-----
-----
### Give me the answer!


-   Select the first log, which records the **OpenAI Chat Model's** first interaction with you.
    
-   The input seems to accurately log your request, but it doesn't seem like there's any output going out of the model.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-5.2.png)

  

> 💡 **Extra for PROs: Why is there no output going out of the chat model?**  
> It might seem odd that the chat model shows no output, but that's actually normal in this setup!
> 
> The chat model is processing the information **within** the AI agent, since the Calendar tool is connected to the same agent. Outputs are only necessary if the agent needs to send information to another node or agent in the workflow.

-   Next, select the second log, which records **Google Calendar's** actions after you sent your prompt.
    
-   Hmmm, the **Input** section is empty, which means the Tool didn't receive any information from ChatGPT.
    
-   But, your tool still created an output!
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-5.3.png)

  

-   Check the start and end time mentioned in the output - do they match up with the time you mentioned for tomorrow?
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-5.4.png)

  

-   You might notice that your Calendar tool is referencing an incorrect time... it might reference the current time instead!
    

> 💡 **Why is my Calendar tool doing this?**  
> If the input section of your Calendar tool is empty, it means it hasn't received any data from the chat model or other parts of the AI agent. Communication within your agent is broken somewhere!
> 
> Without information on when to schedule your event, the Calendar tool defaults to using the current time. This mismatch between your chat message and the Calendar makes the AI agent think you're busy at the time you've requested!
> 
> This is our first peek into the hidden complexities of building an AI workflow - you need to make sure every part of the workflow is correctly receiving and processing the right data.


You got this! Testing and running into errors are big parts of the learning journey. We'll investigate how we can fix this, and learn some cool things along the way 😎


**Update Your Calendar Tool**

-   Select your **Calendar** tool.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-9.png)

  

-   Check your tool's setup... especially the **Start Time** and **End Time** settings!
    

> 💡 **What's in my Start and End time settings?**  
> **Start** and **End** time settings control when events are scheduled.
> 
> If you set the start time to `now` and the end time to `now + 1 hour`, your Calendar will always look to create events that start immediately and last for one hour. This ignores any time suggestions from the AI model.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-5.16.png)

  



-   Notice the top of the setup panel - there's a tip on how you can use data that should be filled by your model.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-5.18.png)

  

-   Let's put this in practice.
    
-   Update the **Start** to `{{ $fromAI('start_time') }}`
    
-   Update the **End Time** to `{{ $fromAI('end_time') }}`
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-10.png)

  

> 💡 **How did we determine these parameter names?**  
> **Parameter names** are like hints to your AI model around what information it should look for in the chat. For example, if you choose a parameter called {{ $fromAI('email') }}`, the AI model will intuitively look for an email address in in the chat instead of a start/end time.
> 
>   
> 🙋‍♀️ **Why are both expressions in red?**  
> Nothing to worry about! Red expressions in n8n usually indicate errors or missing data. In our case, it simply means the AI model needs a new chat message to start filling in values for these expressions. In the meantime, these values are empty.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-5.19.png)

  



  
  

**Re-Test Your Chat**

-   Head back into the **Chat** window. Let's test your AI workflow again!
    
-   Select the down arrow ↓ in your keyboard to repeat the previous request.
    
-   Send the same request to schedule for a time you should be available.
    
-   Woohooo! Looks like our AI agent went to book an event right away!
    

> 🙋‍♀️ **My AI agent didn't try to book an event**  
> That's okay! If your agent didn't book an event, that doesn't necessarily mean you've set things up wrong. There's still one more fix left to make in our workflow... before we make that fix, it's totally possible for an AI agent to provide different kinds of responses to your request!

-   But look closely at the agent's message... did it say it booked you an event for the wrong date?
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-5.21.png)

  

-   [Check your calendar](https://calendar.google.com/) for the new event.
    
-   It looks like our AI agent did set up a meeting for us, but for the wrong time... the event is set in a different year!
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-11.png)

  

-   You know what to do - check the logs from your AI Agent to see what went wrong this time.
    
-   The second log shows your calendar now successfully gets an input. Strangely enough, the start and end times don't seem correct! You'll likely see a date in the wrong year.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-12.png)

-   Why do you think your workflow is still making mistakes?
    
### Tell me the answer
> 💡 **Why is my workflow still making mistakes?**  
> In order to find your availability for **tomorrow**, your AI agent needs to know what day it is **today!**
> 
> We haven't told our AI agent what the date is today yet... so your agent is making its best guess. Even though the Calendar tool is retrieving the start and end times from your AI model (i.e. OpenAI), now it's your AI model that's making a mistake and passing an incorrect date.

### Let me figure it out
-   **Save** your workflow's progress before a final round of troubleshooting 🤺
    

Overall, we still made some good progress on our AI workflow. Updating the start and end time in the Calendar tool made a difference, and now we just need to do a similar thing for the AI agent. You got this!

----
## ✍️ Step #6

### Write a System Message

  

Finally, let's give your AI agent some information on today's date.

That's the final misssing piece to a working AI workflow!

  
  

**In this step, you're going to:**

-   Give your AI agent information by writing a **system message.**
    
-   Test your chat again.
    
-   Watch your assistant book an event in your calendar!
    



  
  

**Add a System Message**

-   Double click on your **AI Agent**.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-13.png)

  

-   This time, select **Add Option** at the bottom of the screen.
    
-   Select **System Message**.
    

> **💡 What is a system message?**  
> The system message is a prompt that your workflow sends to the AI agent before agent starts processing your chat message.
> 
> If you don't enter a system message (oops, that's us so far), your AI agent doesn't have any instructions on what it's meant to do and the current context (e.g. today's date).
> 
> 

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-5.5.png)

  

-   Enter a system message that tells your AI Agent what it's meant to do, and information on today's date.
    


```text
You are a calendar assistant. Your job is to check my availability and create new events for times that my calendar is free. 

You are to use the Chat Model to process the user's requests, then check using the Check Availability tool on whether that time is free. You can use the Google Calendar tool to create a new event in my calendar if I am available.

Today's date is {{DateTime.now().setZone('TIMEZONE').toFormat('dd LLL yyyy HH:mm:ss')}}

```

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-5.6.png)

  

-   Check: Make sure to replace the `TIMEZONE` placeholder in the last line of the System Message with your local time zone.
    

> 🙋‍♀️ **How do I find my time zone?**  
> You have two choices...
> 
> 1.  Search for your time zone manually [using this list](https://github.com/dmfilipenko/timezones.json/blob/master/timezones.json).
>     
> 2.  Ask an AI model like ChatGPT for help. Here's a prompt you could use:
>     
>   
>     
>     ```text
>     You are setting a date in the local time zone for my city. Replace the TIMEZONE placeholder to my location. The ideal output format is simply the updated reference.
>     {{DateTime.now().setZone('TIMEZONE').toFormat('dd LLL yyyy HH:mm:ss')}}
>     
>     ```
>     
>     ![](https://learn.nextwork.org/projects/static/ai-agent-nocode/unframed/step-6.1.png)
>     
>     Tell ChatGPT your local city, and you'll get an updated time zone reference.
>     
>     ![](https://learn.nextwork.org/projects/static/ai-agent-nocode/unframed/step-6.2.png)
>     
>     Paste the updated reference to your System Message window
>     


-   Jump back into the canvas!
    

  
  

**Re-Test Your Chat**

-   Head back into the **Chat** window. Let's test your AI workflow again!
    
-   Select the down arrow ↓ in your keyboard **twice** to repeat the previous request.
    
-   Send the same request to schedule for a time you should be available.
    
-   Check your calendar - what do you see now?  
      
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-15.png)

  

Ahh! The new meeting is still scheduled at the wrong time.

-   Check you AI Agent's logs again. You'll notice that the start and end time for your **Calendar** tool still aren't right.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-16.png)

  

> 💡 **Why is there still an error?**  
> We know that the Calendar tool will take whatever **start** and **end** time the AI model gives it.
> 
> If there was an error in the Calendar tool's input, it would be because the AI model isn't giving the correct values yet.

  
  

Don't give up! You're so close now. You're doing an amazing job 😤🔥

  
  

-   Double click on your **AI Agent**. Let's open it up to troubleshoot the error.
    
-   Take a guess - what do you think needs to change about your **System Message?** You can fix this with a simple click of a button 👀
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-6.4.png)

  

-   Switch your System Message setting from **Fixed** to **Expression.**
    

> 💡 **What does the Expression setting do?**  
> The **Expression** setting means you're entering dynamic input i.e. input that can change based on the JSON functions you've put inside.
> 
> Before, you were using a **Fixed** setting. This meant your **DateTime** JSON function wasn't being used to calculate today's date. Your AI model was just reading the function as a piece of text, which doesn't give it the date information it needs.

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-17.png)

  

-   Jump back into the canvas!
    

 
**Re-Test Your Chat**

-   Head back into the **Chat** window. Let's test your AI workflow again!
    
-   Select the down arrow ↓ in your keyboard **twice** to repeat the previous request.
    
-   Send the same request to schedule for a time you should be available.
    
-   Check your calendar - what do you see now?
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-6.8.png)

  

Congrats! A meeting is scheduled at the right time. Looks like writing a system message made a big difference in getting the workflow to _work._ 💪



Well done! Practice makes perfect, and you've definitely mastered how to set up a basic AI workflow in this project.

It's awesome to see the difference you can make with small changes to your workflow. Congrats on building a successful AI-powered calendar assistant!


----

## 🗑️ Before you go

### Delete your resources

  

Congrats on completing this project on building an AI workflow!

Now that you've set up a working calendar assistant, it's time to wrap up and clean up the resources we created.

You **won't** be charged for leaving your resources in your account, but we'd recommend removing credential information if you no longer want to share you Calendar details with n8n.

  
  

**Resources to delete:**

Delete your Google Calendar credentials in n8n.

**OPTIONAL:** Delete the n8n workflow.

**OPTIONAL:** Delete the test events in Google Calendar.

  
  

### Delete your credentials

-   From your left hand menu, select **Overview.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-delete.1.png)

  

-   You might get prompted to save your changes before leaving. If this is the case, you can select **Save.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-delete.2.png)

  

-   Great! Now you're at the Overview page, which lets you see all your workflows and settings.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-delete.3.png)

  

-   Select the **Credentials** tab.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-delete.4.png)

  

-   Select the three dots for your **Google Calendar account**, and select **Delete**.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-delete.5.png)

  

-   Select **Yes, delete** to confirm your deletion. Note that this means your workflow will be broken until you set up the connection again!
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-delete.6.png)


### Delete the n8n workflow




-   Head back to the **Workflows** tab.
    
-   Select the three dots next to **My workflow.**
    
-   Select **Delete.**
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-delete.7.png)

  

-   Select **Yes, delete** to confirm the deletion.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-delete.8.png)


### Delete the test events



-   Switch tabs from **n8n** to **Google Calendar.**
    
-   Select a test event created by your AI assistant.
    
-   Select **Delete**, or simply press the **delete** key on your keyboard.
    

![](https://learn.nextwork.org/projects/static/ai-agent-nocode/step-delete.9.png)


-----


🎉 Mission Accomplished

### That's a wrap!

  

You've just built an AWESOME AI workflow.

  
  

**You've just learned how to:**

-   Use **n8n** to build a workflow.
    
-   Integrate **ChatGPT** as your AI model to understand requests.
    
-   Integrate **Google Calendar** as your calendar tool.
    

![Yup - you built all that!](https://learn.nextwork.org/projects/static/ai-agent-nocode/new-21.png)

Yup - you built all that!

  

As you might imagine, there is a lot more you can explore with this AI workflow...


-----
