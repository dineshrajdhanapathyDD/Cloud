<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy an App Across Accounts

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-ecr)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-compute-ecr_3e91948719)

---

## Introducing Today's Project!

In this special multiplayer project, I'm working with a buddy to build and deploy containerized apps with AWS. My teammate, Praneeth Bhandwalkar, and I have slight tweaks in our apps but the same challenge!


### What is Amazon ECR?

Amazon ECR is a managed container registry for storing, sharing, and deploying Docker images. In today's project, we used it to push, pull, and run container images while fixing repository permissions.

### One thing I didn't expect...

One thing I didn't expect was a port conflict because my assigned port was already in use. I had to change the port and rerun the Docker image to successfully access the application.

### This project took me...

This project took me some time due to troubleshooting ECR permissions and resolving a port conflict. Overall, setting up access, pulling the image, running the container, and testing took about an hour.

---

## Creating a Docker Image

I set up index.html and Dockerfile. Both files are needed because index.html defines the app's content, while Dockerfile containerizes it for deployment, ensuring consistency across environments.

My Dockerfile tells Docker to create a containerized app by setting a base image, copying index.html, exposing a port, and running a web server. This ensures the app runs consistently across environments.


### I also set up an ECR repository

ECR stands for Amazon Elastic Container Registry. It is important because it securely stores, manages, and deploys container images, integrating with AWS services for scalability, security, and automation.


![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-compute-ecr_e7f8g9h0)

---

## Set Up AWS CLI Access

### AWS CLI can let me run ECR commands

AWS CLI is a command-line tool to interact with AWS services. The CLI asked for my credentials because it needs an access key to authenticate, as it doesn’t use Management Console logins


To enable CLI access, I set up a new IAM user with the permission needed for my tasks. I also set up an access key for this user, which means the CLI can authenticate and interact with AWS securely.


To pass my credentials to the AWS CLI, I ran the command aws configure. I had to provide the Access Key ID, Secret Access Key, my AWS region code, and left the output format as default (JSON).



![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-compute-ecr_4aa3e4fe6)

---

## Pushing My Image to ECR

Push commands are used to upload container images to Amazon ECR. After authentication, I tag the image and push it using "docker push YOUR-ACCOUNT-ID.dkr.ecr.YOUR-REGION.amazonaws.com/your-repo".

### There are three main push commands

To authenticate Docker with my ECR repo, I used the command: "aws ecr get-login-password --region YOUR-REGION | docker login --username AWS --password-stdin YOUR-ACCOUNT-ID.dkr.ecr.YOUR-REGION.amazonaws.com"

To push my container image, I ran the command "docker push 466742534146.dkr.ecr.ap-south-1.amazonaws.com/nextwork/cross-account-docker-app:latest". Pushing means uploading my image to ECR for deployment.


When I built my image, I tagged it with the label latest. This means it represents the most recent version, so deployments pulling latest always get the updated container image. 


---

## Resolving Permission Issues

When I tried pulling my project buddy's container image for the first time, I saw the error "403 Forbidden." This was because Amazon ECR repositories are private by default, and I didn't have the necessary permissions to access the image.

To resolve each other's permission errors, my buddy and I updated our ECR repository policies by adding each other's ARN, ensuring proper access. We then saved the changes and reattempted pulling the image.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-compute-ecr_74b90da414)

---

## Deploying the App

---

## Resolving Deployment Issues

---

---
