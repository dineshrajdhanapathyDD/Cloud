


# Hello Cloud Run



## Overview

![Cloud Run Logo](https://cdn.qwiklabs.com/1d2sNybCwEWoWfxc%2FNEUFPsGq9ntjZEQgOgq2RJHmE4%3D)

[Cloud Run](https://cloud.google.com/run)  is a managed compute platform that enables you to run stateless containers that are invocable via HTTP requests. Cloud Run is serverless: it abstracts away all infrastructure management, so you can focus on what matters most — building great applications.

[Cloud Run](https://cloud.google.com/run)  is built from  [Knative](https://cloud.google.com/knative/), letting you choose to run your containers either fully managed with Cloud Run, or in your  [Google Kubernetes Engine](https://cloud.google.com/kubernetes)  cluster with Cloud Run on GKE.

The goal of this lab is for you to build a simple containerized application image and deploy it to Cloud Run.

### Objectives

In this lab, you learn to:

-   Enable the Cloud Run API.
-   Create a simple Node.js application that can be deployed as a serverless, stateless container.
-   Containerize your application and upload to Container Registry (now called "Artifact Registry.")
-   Deploy a containerized application on Cloud Run.
-   Delete unneeded images to avoid incurring extra storage charges.

## Setup and requirements

For each lab, you get a new Google Cloud project and set of resources for a fixed time at no cost.

1.  Sign in to Qwiklabs using an  **incognito window**.
    
2.  Note the lab's access time (for example,  `1:15:00`), and make sure you can finish within that time.  
    There is no pause feature. You can restart if needed, but you have to start at the beginning.
    
3.  When ready, click  **Start lab**.
    
4.  Note your lab credentials (**Username**  and  **Password**). You will use them to sign in to the Google Cloud Console.
    
5.  Click  **Open Google Console**.
    
6.  Click  **Use another account**  and copy/paste credentials for  **this**  lab into the prompts.  
    If you use other credentials, you'll receive errors or  **incur charges**.
    
7.  Accept the terms and skip the recovery resource page.
    

**Note:**  Do not click  **End Lab**  unless you have finished the lab or want to restart it. This clears your work and removes the project.

#### How to start your lab and sign in to the Console

1.  Click the  **Start Lab**  button. If you need to pay for the lab, a pop-up opens for you to select your payment method. On the left is a panel populated with the temporary credentials that you must use for this lab.
    
    ![Credentials panel](https://cdn.qwiklabs.com/%2FtHp4GI5VSDyTtdqi3qDFtevuY014F88%2BFow%2FadnRgE%3D)
    
2.  Copy the username, and then click  **Open Google Console**. The lab spins up resources, and then opens another tab that shows the  **Choose an account**  page.
    
    **Note:** Open the tabs in separate windows, side-by-side.
    
3.  On the Choose an account page, click  **Use Another Account**. The Sign in page opens.
    
    ![Choose an account dialog box with Use Another Account option highlighted ](https://cdn.qwiklabs.com/eQ6xPnPn13GjiJP3RWlHWwiMjhooHxTNvzfg1AL2WPw%3D)
    
4.  Paste the username that you copied from the Connection Details panel. Then copy and paste the password.
    

**Note:** You must use the credentials from the Connection Details panel. Do not use your Google Cloud Skills Boost credentials. If you have your own Google Cloud account, do not use it for this lab (avoids incurring charges).

5.  Click through the subsequent pages:

-   Accept the terms and conditions.
-   Do not add recovery options or two-factor authentication (because this is a temporary account).
-   Do not sign up for free trials.

After a few moments, the Cloud console opens in this tab.

**Note:** You can view the menu with a list of Google Cloud Products and Services by clicking the  **Navigation menu**  at the top-left.  ![Cloud Console Menu](https://cdn.qwiklabs.com/9vT7xPlxoNP%2FPsK0J8j0ZPFB4HnnpaIJVCDByaBrSHg%3D)

### Activate Google Cloud Shell

Google Cloud Shell is a virtual machine that is loaded with development tools. It offers a persistent 5GB home directory and runs on the Google Cloud.

Google Cloud Shell provides command-line access to your Google Cloud resources.

1.  In Cloud console, on the top right toolbar, click the Open Cloud Shell button.
    
    ![Highlighted Cloud Shell icon](https://cdn.qwiklabs.com/00tA48qOVOyHrSa1DA7LwccfwQ9Z%2BE6dkvQ1MYPHzhQ%3D)
    
2.  Click  **Continue**.
 
 ![1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/b781ea63-0c45-43ce-80c9-6ae5dc4f6bae)   

It takes a few moments to provision and connect to the environment. When you are connected, you are already authenticated, and the project is set to your  _PROJECT_ID_. For example:

![Project ID highlighted in the Cloud Shell Terminal](https://cdn.qwiklabs.com/hmMK0W41Txk%2B20bQyuDP9g60vCdBajIS%2B52iI2f4bYk%3D)

**gcloud**  is the command-line tool for Google Cloud. It comes pre-installed on Cloud Shell and supports tab-completion.

-   You can list the active account name with this command:

`gcloud auth list`


**Output:**

Credentialed accounts:
 - @.com (active)

**Example output:**

Credentialed accounts:
 - google1623327_student@qwiklabs.net

-   You can list the project ID with this command:

`gcloud config list project`



**Output:**
```
[core]
project = 
```
**Example output:**
```
[core]
project = qwiklabs-gcp-44776a13dea667a6
```

![3](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/b361ab8c-5503-4743-ba4e-d23188487c8b)

**Note:** Full documentation of  **gcloud**  is available in the  [gcloud CLI overview guide](https://cloud.google.com/sdk/gcloud) .

### Reference

### Basic Linux Commands

Below you will find a reference list of a few very basic Linux commands which may be included in the instructions or code blocks for this lab.


|                |Command                         |Action                       |
|----------------|-------------------------------|-----------------------------|
|1 |`**mkdir**  (_make directory_)            |create a new folder            |
|2 |**cd**  (_change directory_)|change location to another folder|
|3|**ls**  (_list_  )|list files and folders in the directory|
|4|**cat**  (_concatenate_)|read contents of a file without using an editor|
|5|**apt-get update**|update package manager library|
|6 |**ping**|signal to test reachability of a host|
|7|**mv**  (_move_  )|moves a file|
|8|**cp**  (_copy_)|makes a file copy|
|9|**pwd**  (_present working directory_  )|returns your current location|
|10|**sudo**  (_super user do_)|gives higher administration privileges|





.
![2](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a5d6d678-9da5-4c75-a18b-049360c4d8d5)

## Task 1. Enable the Cloud Run API and configure your Shell environment

1.  From Cloud Shell, enable the  **Cloud Run API**  :

`gcloud services enable run.googleapis.com`



2.  If you are asked to authorize the use of your credentials, do so. You should then see a successful message similar to this one:

Operation "operations/acf.cc11852d-40af-47ad-9d59-477a12847c9e" finished successfully.

**Note:** You can also enable the API using the  **APIs & Services** section of the console.

3.  Set the compute region:

`gcloud config set compute/region "REGION"`



4.  Create a LOCATION environment variable:

`LOCATION="Region"`

![4 task 1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/c7162941-538a-45e4-a0f4-91f73ae8d131)

## Task 2. Write the sample application

In this task, you will build a simple express-based NodeJS application which responds to HTTP requests.

1.  In Cloud Shell create a new directory named  `helloworld`, then move your view into that directory:

`mkdir helloworld && cd helloworld`



2.  Next you'll be creating and editing files. To edit files, use  `nano`  or the Cloud Shell Code Editor by clicking on the  **Open Editor**  button in Cloud Shell.
    
3.  Create a  `package.json`  file, then add the following content to it:
    

`nano package.json`

```
{
  "name": "helloworld",
  "description": "Simple hello world sample in Node",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "author": "Google LLC",
  "license": "Apache-2.0",
  "dependencies": {
    "express": "^4.17.1"
  }
}
```


Most importantly, the file above contains a start script command and a dependency on the Express web application framework.

4.  Press  **CTRL+X**, then  **Y**, then  **Enter**  to save the  `package.json`  file.
    
5.  Next, in the same directory, create a  `index.js`  file, and copy the following lines into it:
    

`nano index.js`


```
const express = require('express');
const app = express();
const port = process.env.PORT || 8080;

app.get('/', (req, res) => {
  const name = process.env.NAME || 'World';
  res.send(`Hello ${name}!`);
});

app.listen(port, () => {
  console.log(`helloworld: listening on port ${port}`);
});
```


This code creates a basic web server that listens on the port defined by the  `PORT`  environment variable. Your app is now finished and ready to be containerized and uploaded to Container Registry.

6.  Press  **CTRL+X**, then  **Y**, then  **Enter**  to save the  `index.js`  file.


![5 task 2](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/cd4aaab6-d399-48b6-9a86-d26cacad9ffc)

**Note:** You can use many other languages to get started with Cloud Run. You can find instructions for Go, Python, Java, PHP, Ruby, Shell scripts, and others from the  [Quickstarts guide](https://cloud.google.com/run/docs/quickstarts/build-and-deploy).

## Task 3. Containerize your app and upload it to Artifact Registry

1.  To containerize the sample app, create a new file named  `Dockerfile`  in the same directory as the source files, and add the following content:

`nano Dockerfile`



# Use the official lightweight Node.js 12 image.
### https://hub.docker.com/_/node

`FROM node:12-slim`

# Create and change to the app directory.

`WORKDIR /usr/src/app`

### Copy application dependency manifests to the container image.
### A wildcard is used to ensure copying both package.json AND package-lock.json (when available).
### Copying this first prevents re-running npm install on every code change.
`COPY package*.json ./`

### Install production dependencies.
### If you add a package-lock.json, speed your build by switching to 'npm ci'.
### RUN npm ci --only=production
`RUN npm install --only=production`

### Copy local code to the container image.
`COPY . ./`

### Run the web service on container startup.
`CMD [ "npm", "start" ]`



2.  Press  **CTRL+X**, then  **Y**, then  **Enter**  to save the  `Dockerfile`  file.
    
3.  Now, build your container image using Cloud Build by running the following command from the directory containing the  `Dockerfile.`  (Note the $GOOGLE_CLOUD_PROJECT environmental variable in the command, which contains your lab's Project ID):
    

`gcloud builds submit --tag gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld`



Cloud Build is a service that executes your builds on GCP. It executes a series of build steps, where each build step is run in a Docker container to produce your application container (or other artifacts) and push it to Cloud Registry, all in one command.

Once pushed to the registry, you will see a SUCCESS message containing the image name (`gcr.io/[PROJECT-ID]/helloworld`). The image is stored in Artifact Registry and can be re-used if desired.

4.  List all the container images associated with your current project using this command:

`gcloud container images list`



5.  Register  `gcloud`  as the credential helper for all Google-supported Docker registries:

`gcloud auth configure-docker`



6.  To run and test the application locally from Cloud Shell, start it using this standard  `docker`  command:

`docker run -d -p 8080:8080 gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld`

![6](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/753d00d0-6647-48ff-8578-30aa88d95e54)


7.  In the Cloud Shell window, click on  **Web preview**  and select  **Preview on port 8080**.

This should open a browser window showing the "Hello World!" message. You could also simply use  `curl localhost:8080`.

![9](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/7728e247-91f9-4694-8b1e-2dc8cbd4c147)

## Task 4. Deploy to Cloud Run

1.  Deploying your containerized application to Cloud Run is done using the following command adding your Project-ID:

`gcloud run deploy --image gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld --allow-unauthenticated --region=$LOCATION`



The allow-unauthenticated flag in the command above makes your service publicly accessible.

2.  When prompted confirm the  `service name`  by pressing  **Enter**.

Wait a few moments until the deployment is complete.

![7](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/794a502b-93d2-494d-ae55-e8dd305cbe16)

On success, the command line displays the service URL:

Service [helloworld] revision [helloworld-00001-xit] has been deployed
and is serving 100 percent of traffic.

Service URL: https://helloworld-h6cp412q3a-uc.a.run.app

You can now visit your deployed container by opening the service URL in any browser window.

![10](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/10fded73-1ba5-4918-98f9-88abe15af61d)

**Congratulations!**  You have just deployed an application packaged in a container image to Cloud Run. Cloud Run automatically and horizontally scales your container image to handle the received requests, then scales down when demand decreases. In your own environment, you only pay for the CPU, memory, and networking consumed during request handling.

For this lab you used the  `gcloud`  command-line. Cloud Run is also available via Cloud Console.

-   From the  **Navigation menu**, in the Serverless section, click  **Cloud Run**  and you should see your  `helloworld`  service listed:

![11](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/bf8d560e-65ae-4483-9801-7f41c5b90185)

## Task 5. Clean up

While Cloud Run does not charge when the service is not in use, you might still be charged for storing the built container image.

1.  You can either decide to delete your GCP project to avoid incurring charges, which will stop billing for all the resources used within that project, or simply delete your  `helloworld`  image using this command :

`gcloud container images delete gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld`



2.  When prompted to continue type  `Y`, and press  **Enter**.
    
3.  To delete the Cloud Run service, use this command :
    

`gcloud run services delete helloworld --region="REGION"`



4.  When prompted to continue type  `Y`, and press  **Enter**.

`curl localhost:8080`

![12](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/9adb06d2-68f8-4940-ba8d-3e83d4f1c4aa)