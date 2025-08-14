<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build Your First AI Workflow

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-agent-nocode)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

## Building an AI Workflow

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/ai-agent-nocode_sdrjg8e123dv)

---

## Introducing Today's Project!

In this project, I will demonstrate setting up an AI workflow using n8n. I'm doing this project to learn how to integrate ChatGPT and my calendar, while also leveling up my prompt engineering skills!

### Tools and Techniques

Services I used were n8n, OpenAI, and Google Calendar. Key concepts and skills I learned include AI workflow automation, integrating APIs, prompt engineering, and automating meeting scheduling efficiently.

### Project reflection

This project took me approximately 2 hours. The most challenging part was troubleshooting calendar integration. It was most rewarding to see the AI automate meeting scheduling seamlessly in real time.

I did this project today to build an AI workflow that automatically schedules meetings with Google Calendar. This project met my goals by successfully integrating AI and calendar automation for efficient task management.

---

## Exploring n8n

I'm using n8n in this project to automate tasks and integrate AI. Workflows are sequences of automated actions that streamline processes. You can involve AI in a workflow by adding AI tools.

I signed up for a free trial for n8n, which includes 14 days of access to n8n and the ability to create up to 5 workflows. I don't need to enter credit card details to start the trial, so I won't be charged

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/ai-agent-nocode_c9d8f7a2)

---

## Starting an AI Workflow

To set up a workflow, I first configured a trigger, which means the action or schedule time that kicks off the workflow (make it run). My trigger is chat message. Other options include scheduled time (e.g., every day at 8 a.m.). or a manual trigger.

I connected my trigger with an AI agent node. AI agents are automated systems that process data and perform tasks using AI. But, in this project, I am building a workflow, which does require triggers/steps 

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/ai-agent-nocode_fmtkjyrg)

---

## Integrating ChatGPT

An AI workflow can be broken into three key components, which are chat model (i.e. the brains of the agent), Memory (i.e. storing past interactions and data), and tools (i.e., software and code to help carry out tasks)

My workflow's chat model uses OpenAI's services. Usually, connecting with OpenAI requires an API key. I could connect with OpenAI for free by using the claim 100 API credits offered in n8n.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/ai-agent-nocode_o5p6q7r8)

---

## Integrating Google Calendar

In this workflow, the tool is Google Calendar because it enables the AI to schedule, retrieve, and manage events, making it an essential component for automating time management tasks seamlessly.

To connect with Google Calendar, you have to allow n8n access to your calendar data and event management. For security best practices, it's important to grant only necessary permissions and revoke unused ones.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/ai-agent-nocode_c9d8dfgv2)

---

## Testing My Workflow

I tested my AI workflow by asking it to book a meeting for tomorrow at 10 am. The response was that it started sending the invite link for the events. which is an error because its at the wrong time, and the workflow should only book the event once.

To troubleshoot errors, you can investigate the AI agent's logs. I observed that the logs for the calendar tool showcased no input, which means its not getting any information around the proper start and end time for the event you want to book.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/ai-agent-nocode_c9d8egrfdv)

---

## JSON Expressions

I decided to troubleshoot by reviewing our calendar tool's setup. where I noticed an error in the tool's start and end time configuration. By default, it takes in the current time as the start time—this ignore input/information from the chat model

I updated the start and end times in the calendar tool to JSON references for information in the AI model to gather. For example, instead of the current time, the start time is now '{{ $fromAI('start_time') }}'. the AI model will fill it out for us.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/ai-agent-nocode_897rg465e)

---

## System Messages

On my second test, my workflow successfully created an event and took in input from our AI chat model. but it still made an error in scheduling the right date. This was because our chat model is passing the wrong date to my calendar tool.

This time, I tried to troubleshoot the error by writing a system message, which is a predefined instruction that guides the AI's behavior, ensuring accurate responses and workflow execution.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/ai-agent-nocode_rfgdhn456)

---

## Success!

On my final test, a new event was scheduled at the right time because my system message was set as an expression (and not fixed). This means my AI agent will get accurate information around today's date, calculated automatically at every message.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/ai-agent-nocode_w3x4y5z6)

---

## System Message Variation

---

---
