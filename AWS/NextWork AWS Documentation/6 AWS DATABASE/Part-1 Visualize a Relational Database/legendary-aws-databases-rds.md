<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Visualize a Relational Database

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-rds)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

## Visualise a Relational Database

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-rds_1fddb0b5)

---

## Introducing Today's Project!

### What is Amazon RDS?

Amazon RDS is a managed database service that simplifies setup, scaling, and maintenance of relational databases. It’s useful for automating backups, improving security, and reducing administrative overhead.

### How I used Amazon RDS in this project

I used Amazon RDS to create a relational database, store structured data, secure access with security groups, and connect it to QuickSight for visualization, ensuring efficient data management and analysis.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was needing to update the QuickSight execution role with a custom IAM policy to allow VPC access. It was crucial for securely connecting QuickSight to RDS.

### This project took me...

This project took me a few hours, including setting up RDS, configuring security groups, making it private, updating IAM roles, connecting to QuickSight, and creating visualizations. A great hands-on experience.

---

## In the first part of my project...

### Creating a Relational Database

I created my relational database by setting up an Amazon RDS instance, choosing MySQL, configuring settings, enabling public access, connecting via a SQL client, and creating tables to store data. 

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-rds_43343546)

---

## Understanding Relational Databases

A relational database is a structured collection of data organized into tables with rows and columns, where relationships between tables are defined using keys to ensure efficient data management and retrieval.

### MySQL vs SQL

The difference between MySQL and SQL is that SQL (Structured Query Language) is a language for managing & manipulating databases, while MySQL is a relational database management system (RDBMS) that uses SQL.

---

## Populating my RDS instance

The first thing I did was make my RDS instance public because it allows MySQL Workbench on my local machine to connect to it, making it easier to manage, query, and visualize data outside the AWS network.

I had to update the default security group for my RDS schema because it controls database access. By allowing only my IP, I ensure MySQL Workbench can connect securely from my local machine.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-rds_91b9fd1g)

---

## Using MySQL Workbench

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-rds_1fddb0b5)

To populate my database, I used SQL INSERT statements to add employee records into the newhire table, ensuring each row had relevant details like job title, salary, hire date, and department.

---

## Connecting QuickSight and RDS

To connect my RDS instance to QuickSight, I updated the security group, role to allow QuickSight access, added RDS as a data source in QuickSight, entered database credentials, and verified the connection.

This solution is risky because making the RDS instance public exposes it to potential security threats. Allowing inbound traffic increases the risk of unauthorized access, so stricter access controls are needed.

### A better strategy

First, I made a new security group so that only QuickSight can access my RDS instance. This restricts inbound traffic, enhancing security while allowing seamless data visualization in QuickSight.

Next, I connected my new security group to QuickSight by creating a connection to QuickSight and my vpc and my security group. i had to update my IAM role policy and also used it.

---

## Now to secure my RDS instance

To make my RDS instance secure, I made it private, created a dedicated security group, and allowed access only from QuickSight’s security group, ensuring restricted and secure data communication. 

I made sure that my RDS instance could be accessed from QuickSight by updating the RDS security group to allow inbound traffic from QuickSight’s security group, ensuring a secure and private connection.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-rds_1709b26b)

---

## Adding RDS as a data source for QuickSight

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-rds_1709b29b)

This data source is different from my initial data source because it now uses a private RDS instance with restricted access via security groups, ensuring a more secure and controlled connection for QuickSight.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-rds_1709b30b)

---

---
