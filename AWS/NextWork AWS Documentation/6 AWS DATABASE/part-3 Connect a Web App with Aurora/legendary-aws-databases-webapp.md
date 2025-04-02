<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Connect a Web App with Aurora

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-webapp)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

## Connect a Web App to Amazon Aurora

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-webapp_1709b26b)

---

## Introducing Today's Project!

### What is Amazon Aurora?

Amazon Aurora is a fully managed relational database offering high performance, scalability, and automatic failover. It’s useful for secure, cost-efficient apps needing MySQL or PostgreSQL compatibility.

### How I used Amazon Aurora in this project

I used Amazon Aurora to create a relational database that stores user-submitted data from my web app. It ensures high availability, scalability, and seamless integration with my EC2-hosted application.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was the challenge of connecting via SSH, switching to the bash shell, and ensuring a stable connection to the Aurora database, requiring extra debugging and configurations.

### This project took me...

This project took me a few hours, including setting up the EC2 instance, configuring the Aurora database, troubleshooting SSH and Bash connections, and ensuring smooth database integration with the web app.

---

## Creating a Web App

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-webapp_b7999168)

To connect to my EC2 instance, I used SSH with the command: ssh -i NextWorkAuroraApp.pem ec2-user@ec2-3-110-165-76.ap-south-1.compute.amazonaws.com, ensuring secure access with my key pair.

To help me create my web app, I first installed Apache (httpd), PHP, MySQL extension (php-mysqli), and MariaDB (mariadb105) using sudo dnf install -y, ensuring my server can run PHP and connect to Aurora.

---

## Connecting my Web App to Aurora

I set up my EC2 instance's connection details to my database by creating a dbinfo.inc file in the inc directory and adding my Aurora endpoint, database name, username, and password for secure access.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-webapp_1709b25b)

---

## My Web App Upgrade

Next, I upgraded my web app by creating a new PHP file to connect to the database, adding a simple frontend with a submission form, and displaying stored data in a table for a user-friendly experience.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-webapp_2709b25b)

---

## Testing my Web App

To make sure my web app was working correctly, I tested it in the browser, submitted data through the form, and used MySQL CLI queries to check if the data was successfully stored in my Aurora database.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-databases-webapp_1409z22b)

---

---
