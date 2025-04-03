<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Load Data into DynamoDB

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-dynamodb)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

## Load Data into a DynamoDB Table

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-dynamodb_b481c730)

---

## Introducing Today's Project!

### What is Amazon DynamoDB?

Amazon DynamoDB is a fully managed NoSQL database that offers fast performance, scalability, and flexibility. It’s useful for handling high-traffic applications, real-time data, and dynamic schemas. 

### How I used Amazon DynamoDB in this project

In today's project, I used Amazon DynamoDB to create tables, load data, and update records. I also explored batch writing, querying, and managing attributes, gaining hands-on experience with NoSQL databases.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how flexible DynamoDB is compared to relational databases. Being able to store items with different attributes without a fixed schema was really insightful.

### This project took me...

This project took me a few hours to complete, including creating tables, loading data, and updating records. Exploring DynamoDB’s flexibility and speed made the learning process engaging and valuable. 

---

## Create a DynamoDB table

DynamoDB tables organize data using items and attributes instead of fixed rows and columns. Each item can have a unique set of attributes, offering flexibility not possible in relational databases.

An attribute is a piece of data describing an item in DynamoDB. Each item can have multiple attributes, and unlike relational databases, items in DynamoDB can have unique attribute sets.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-dynamodb_a3cefee0)

---

## Read and Write Capacity

Read capacity units (RCUs) and write capacity units (WCUs) are measures of DynamoDB's performance. 1 RCU supports 2 reads/sec, while 1 WCU allows 1 write/sec. Usage impacts cost and scalability. 

Amazon DynamoDB's Free Tier covers 25GB storage, 25 RCUs, and 25 WCUs, handling 200M requests/month for free. I turned off auto scaling to avoid unexpected costs and control resource allocation.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-dynamodb_ef47dd8f)

---

## Using CLI and CloudShell

AWS CloudShell is a browser-based shell in the AWS Management Console that lets you run commands. It comes with AWS CLI pre-installed, making it easy to manage AWS resources without setup. 

AWS CLI is a command-line tool that allows users to create, manage, and automate AWS resources using commands instead of the AWS console, making cloud operations faster and more efficient.

I ran a CLI command in AWS CloudShell that created four DynamoDB tables: ContentCatalog, Forum, Post, and Comment, each with defined attributes, key schemas, and provisioned throughput settings. 

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-dynamodb_81e0258b)

---

## Loading Data with CLI

I ran a CLI command in AWS CloudShell that used batch-write-item to load data into four DynamoDB tables: ContentCatalog, Forum, Post, and Comment, by reading data from JSON files. 

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-dynamodb_791c600b)

---

## Observing Item Attributes

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-dynamodb_b481c731)

I checked a ContentCatalog item, which had the following attributes: id, content type, difficulty, price, project category, URL, published status, and title—all defining the project’s details. 

I checked another ContentCatalog item, which had a different set of attributes: Services, title, URL, videotype, etc.,

---

## Benefits of DynamoDB

A benefit of DynamoDB over relational databases is flexibility because each item can have unique attributes, unlike relational databases that require uniform columns. This makes it ideal for e-commerce and dynamic data.

Another benefit over relational databases is speed because DynamoDB uses partition keys to quickly locate items, while relational databases must scan entire tables, which slows down performance for large datasets. 

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-dynamodb_b481c730)

---

---
