<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Aurora Database with EC2

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-aurora)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

## Connect a Web App to Amazon Aurora

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-aurora_44443546)

---

## Introducing Today's Project!

### What is Amazon Aurora?

Amazon Aurora is a fully managed relational database offering high performance, scalability, and automatic failover. It’s useful for cost-efficient, fault-tolerant applications needing MySQL or PostgreSQL compatibility.

### How I used Amazon Aurora in this project

I used Amazon Aurora to create a highly available relational database cluster, ensuring fault tolerance and scalability. It connects to an EC2-hosted web app, providing efficient data storage and retrieval.

### One thing I didn't expect in this project was...

I didn’t expect the ARN role permission issue when creating the EC2 instance for the database. It required additional IAM permissions to allow proper access, delaying the setup and needing troubleshooting.

### This project took me...

This project took me a few hours, including setting up the EC2 instance, configuring the Aurora database, troubleshooting IAM role issues, and ensuring proper connectivity between the web app server and database.

---

## In the first part of my project...

### Creating an Aurora Cluster

A relational database is a structured system that stores data in tables with rows and columns. It uses SQL for queries and maintains relationships between tables using keys, ensuring data integrity and efficiency.

Aurora is a good choice when you need a fully managed, high-performance relational database with auto-scaling, fault tolerance, and up to 5x MySQL or 3x PostgreSQL speed at lower costs than commercial DBs.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-aurora_44443546)

---

## Halfway through I stopped!

I stopped creating my Aurora database because I needed to set up an EC2 instance first to act as a web app server, ensuring a seamless connection between the application and the database for smooth operation.

### Features of my EC2 instance

I created a new key pair for my EC2 instance because it provides a secure way to connect via SSH, ensuring only authorized access while protecting the instance from unauthorized logins and security threats.

When I created my EC2 instance, I took particular note of the public IP, private IP, security group, instance ID, and key pair. These are crucial for secure access, network setup, and managing the instance.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-aurora_91b9fd1g)

---

## Then I could finish setting up my database

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-aurora_1fddb0b5)

Aurora Database uses clusters because they ensure high availability, fault tolerance, and scalability by using a primary instance for writes and multiple read replicas for backups and failover protection.

---

---
