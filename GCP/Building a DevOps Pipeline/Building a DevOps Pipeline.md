

# Building a DevOps Pipeline



## Overview

 you will build a continuous integration pipeline using Cloud Source Repositories, Cloud Build, build triggers, and Artifact Registry.

![Continuous integration pipeline architecture](https://cdn.qwiklabs.com/K6AxXI6Pn59dCySH0XsAMKmqU9MlAHTPnuekPGr1wls%3D)

## Objectives

you will learn how to perform the following tasks:

-   Create a Git repository
-   Create a simple Python application
-   Test Your web application in Cloud Shell
-   Define a Docker build
-   Manage Docker images with Cloud Build and Artifact Registry
-   Automate builds with triggers
-   Test your build changes

![1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/8946778f-7086-4e59-86c0-e1a4b628dd65)

## Task 1. Create a Git repository

First, you will create a Git repository using the Cloud Source Repositories service in Google Cloud. This Git repository will be used to store your source code. Eventually, you will create a build trigger that starts a continuous integration pipeline when code is pushed to it.

1.  In the Cloud Console, on the  **Navigation menu**, click  **Source Repositories**. A new tab will open.
2.  Click  **Add repository**.
3.  Select  **Create new repository**  and click  **Continue**.
4.  Name the repository  **devops-repo**.
5.  Select your current project ID from the list.
6.  Click  **Create**.

![2](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/9541c309-b34d-45de-8101-b01d698268bb)

7.  Return to the Cloud Console, and click  **Activate Cloud Shell**  (![Cloud Shell icon](https://cdn.qwiklabs.com/ep8HmqYGdD%2FkUncAAYpV47OYoHwC8%2Bg0WK%2F8sidHquE%3D "Cloud Shell")).
8.  If prompted, click  **Continue**.
9.  Enter the following command in Cloud Shell to create a folder called  `gcp-course`:
```
mkdir gcp-course
````


10.  Change to the folder you just created:
```
cd gcp-course
```


11.  Now clone the empty repository you just created:
```
gcloud source repos clone devops-repo
```


**Note:** You will see a warning that you have cloned an empty repository. That is expected at this point.

12.  The previous command created an empty folder called  `devops-repo`. Change to that folder:
```
cd devops-repo
```

![3](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/94d16c2c-9086-48cf-8e60-a3a5c9fbfa35)

Click  _Check my progress_  to verify the objective.

Create a git repository.

Check my progress


![4](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/96dcfedc-059c-4d32-a3ad-e0b75250477e)


## Task 2. Create a simple Python application

You need some source code to manage. So, you will create a simple Python Flask web application. The application will be only slightly better than "hello world", but it will be good enough to test the pipeline you will build.

1.  In Cloud Shell, click  **Open Editor**  (![Editor icon](https://cdn.qwiklabs.com/zxK8nW520maN72Qq6D1Lt9gCeDh7QOMGWCwhny5S8sQ%3D)) to open the code editor. If prompted click  **Open in a new window**.
2.  Select the  **gcp-course > devops-repo**  folder in the explorer tree on the left.

![5](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f66420b6-e9bb-4678-ad5e-e4c19a927176)

3.  Click on  **devops-repo**
4.  On the  **File menu**, click  **New File**
5.  Paste the following code into the file you just created:
```
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")
def main():
    model = {"title": "Hello DevOps Fans."}
    return render_template('index.html', model=model)

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=8080, debug=True, threaded=True)
```


![6](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a0151690-a6de-470e-a4f2-c217041cffad)

6.  To save your changes. Press  __CTRL + S_,_  and name the file as  `main.py`.
7.  Click on  **SAVE**
8.  Click on the  `devops-repo`  folder.
9.  Click on the  **File menu**, click  **New Folder**, Enter folder name as  `templates`.
10.  Click  **OK**
11.  Right-click on the  `templates`  folder and create a new file called  `layout.html`.
12.  Add the following code and save the file as you did before:
```
<!doctype html>
<html lang="en">
<head>
    <title>{{model.title}}</title>
    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">

</head>
<body>
    <div class="container">

        {% block content %}{% endblock %}

        <footer></footer>
    </div>
</body>
</html>
```

![7](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/84801fdf-6e0b-409a-95b7-63aaee858d82)

12.  Also in the templates folder, add another new file called  `index.html`.
    
13.  Add the following code and save the file as you did before:
    
```
{% extends "layout.html" %}
{% block content %}
<div class="jumbotron">
    <div class="container">
        <h1>{{model.title}}</h1>
    </div>
</div>
{% endblock %}
```


14.  In Python, application prerequisites are managed using pip. Now you will add a file that lists the requirements for this application.
    
15.  In the  **devops-repo**  folder (_not the templates folder_), create a  **New File**  and add the following to that file and save it as  `requirements.txt`:
    
```
Flask>=2.0.3
```
![8](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/fe36561f-8ed8-48d5-b199-6a8b4795e4e2)

16.  You have some files now, so save them to the repository. First, you need to add all the files you created to your local Git repo. In Cloud Shell, enter the following code:

```
cd ~/gcp-course/devops-repo
git add --all
```


17.  To commit changes to the repository, you have to identify yourself. Enter the following commands, but with your information (_you can just use your Gmail address or any other email address_):
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
````


18.  Now, commit the changes locally:
```
git commit -a -m "Initial Commit"
```


19.  You committed the changes locally, but have not updated the Git repository you created in Cloud Source Repositories. Enter the following command to push your changes to the cloud:
```
git push origin master
```
![9](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e33b113e-64d5-4601-8171-840df05b85f0)

20.  Refresh the  **Source Repositories**  web page. You should see the files you just created.



![10](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/ff7ee977-2157-4d8c-92fe-6c955441312f)

![11](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/6739d510-5525-4c00-b1e6-f46cb6726e37)
![12](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/314ca0e9-4e02-4e87-9842-8ac8f749c920)


## Task 3. Define a Docker build

The first step to using Docker is to create a file called  **Dockerfile**. This file defines how a Docker container is constructed. You will do that now.

1.  In the Cloud Shell Code Editor, expand the  **gcp-course/devops-repo**  folder. With the  **devops-repo**  folder selected, on the  **File**  menu, click  **New File**  and name the new file  **Dockerfile**.

The file  _Dockerfile_  is used to define how the container is built.

2.  At the top of the file, enter the following:
```
FROM python:3.9
```

This is the base image. You could choose many base images. In this case, you are using one with Python already installed on it.

3.  Enter the following:
```
WORKDIR /app
COPY . .
```


These lines copy the source code from the current folder into the /app folder in the container image.

4.  Enter the following:
```
RUN pip install gunicorn
RUN pip install -r requirements.txt
```


This uses pip to install the requirements of the Python application into the container. Gunicorn is a Python web server that will be used to run the web app.

5.  Enter the following:

ENV PORT=80
CMD exec gunicorn --bind :$PORT --workers 1 --threads 8 main:app



The environment variable sets the port that the application will run on (in this case, 80). The last line runs the web app using the gunicorn web server.

6.  Verify that the completed file looks as follows and save it:
```
FROM python:3.9
WORKDIR /app
COPY . .
RUN pip install gunicorn
RUN pip install -r requirements.txt
ENV PORT=80
CMD exec gunicorn --bind :$PORT --workers 1 --threads 8 main:app
```
![13](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/aedab003-8059-422e-81df-19ea83929e89)

## Task 4. Manage Docker images with Cloud Build and Artifact Registry

The Docker image has to be built and then stored somewhere. You will use  **Cloud Build**  and  **Artifact Registry**.

1.  Return to Cloud Shell. Make sure you are in the right folder:
```
cd ~/gcp-course/devops-repo
```


2.  The Cloud Shell environment variable DEVSHELL_PROJECT_ID automatically has your current project ID stored. The project ID is required to store images in Artifact Registry. Enter the following command to view your project ID:
```
echo $DEVSHELL_PROJECT_ID
```


3.  Enter the following command to create an Artifact Registry repository named devops-repo:
```
gcloud artifacts repositories create devops-repo \
    --repository-format=docker \
    --location=us-central1
```


4.  To configure Docker to authenticate to the Artifact Registry Docker repository, enter the following command:
```
gcloud auth configure-docker us-central1-docker.pkg.dev
```

![14](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/bd448903-419a-464b-add6-ef37e40a9b3d)


![15](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/18bcefb1-3b96-4a73-acdc-1c41529b0cea)

![16](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/dea4b4d5-3449-4f20-837a-9532e5c1c4c0)

5.  To use Cloud Build to create the image and store it in Artifact Registry, type the following command:
```
gcloud builds submit --tag us-central1-docker.pkg.dev/$DEVSHELL_PROJECT_ID/devops-repo/devops-image:v0.1 .
```


_Notice the environment variable in the command_. The image will be stored in Artifact Registry.

6.  Return to the  **Cloud Console**  and on the  **Navigation menu**  (  ![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **Artifact Registry**  and then click  **devops-repo**.


![17](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/d8647ff1-f692-4f93-9f97-ab4bdd2a0f6e)
    
![18](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/549ae7ea-ddf7-483a-8687-a754771f4806)


7.  Click  **devops-image**. Your image should be listed.

![19](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/0bc67479-917e-4373-bca8-b2d11e1c4af3)
    
8.  Now navigate to the  **Cloud Build**  service, and your build should be listed in the history.

![20](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f0fe57c9-0a5c-4a2f-8d00-496eacd88633)

![21](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/638fe23b-9d0a-4234-8d9a-1fc08a9e24bd)

![22](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/afb1e1d9-c89a-42c3-b2da-065d96064425)
    

You will now try running this image from a Compute Engine virtual machine.

9.  Navigate to the  **Compute Engine**  service.
    
10.  Click  **Create Instance**  to create a VM.


![23](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/1a086a39-5caf-458c-81b6-b196cabaa851)
    
11.  On the  **Create an instance**  page, specify the following, and leave the remaining settings as their defaults:
    

**Property**

**Value**

**Container**

Click DEPLOY CONTAINER

**Container image**

`us-central1-docker.pkg.dev/<insert-your-project-id-here>/devops-repo/devops-image:v0.1`  (change the project ID where indicated) and click SELECT

![24](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a97a3fdc-7376-441e-99f6-4ac74aabf6aa)


**Firewall**

Allow HTTP traffic

12.  Click  **Create**.



![25](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/70fa6b50-b0ff-4f56-be8f-31b64f82c6b5)


    
13.  Once the VM starts, click the VM's external IP address. A browser tab opens and the page displays  `Hello DevOps Fans.`
    
![26](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/5daed31e-2b45-4fcc-bf71-b57552ac70b3)

![27](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/83d753ba-a967-4300-a9b7-d60817f49a78)

**Note:** You might have to wait a minute or so after the VM is created for the Docker container to start.

14.  You will now save your changes to your Git repository. In Cloud Shell, enter the following to make sure you are in the right folder and add your new Dockerfile to Git:
```
cd ~/gcp-course/devops-repo
git add --all
```


15.  Commit your changes locally:
```
git commit -am "Added Docker Support"
```


16.  Push your changes to Cloud Source Repositories:
```
git push origin master
```
![28](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/d7dad512-6575-4574-adac-ff55f1c73ebf)

17.  Return to Cloud Source Repositories and verify that your changes were added to source control.

Click  _Check my progress_  to verify the objective.

Manage Docker images with Cloud Build and Artifact Registry.

Check my progress

![29](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/73802919-5908-43ab-95da-305011fc5ba9)


## Task 5. Automate builds with triggers

1.  On the  **Navigation menu**, click  **Cloud Build**. The  **Build history**  page should open, and one or more builds should be in your history.
    
2.  Click the  **Triggers**  link on the left.
    
3.  Click  **Create trigger**  and specify the following:


![30](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/8b997eed-dce2-42b8-918b-b5fe7ee42a4e)
    

**Property**

**Value**

**Name**

devops-trigger

**Repository**

devops-repo(Cloud Source Repositories)

**Branch**

.*(any branch)

**Configuration**

Dockerfile

**Image name**

`us-central1-docker.pkg.dev/<insert-your-project-id-here>/devops-repo/devops-image:$COMMIT_SHA`  (change the project ID where indicated)

4.  Accept the rest of the defaults, and click  **Create**.

![35](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a1acbda8-4967-4779-b9e9-6599e4b878aa)
    
5.  To test the trigger, click  **Run**  and then  **Run trigger**.
    
6.  Click the  **History**  link and you should see a build running. Wait for the build to finish, and then click the link to it to see its details.
    
7.  Scroll down and look at the logs. The output of the build here is what you would have seen if you were running it on your machine.

![36](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/0f0566df-d264-448d-8111-74166066f145)
    
8.  Return to the Artifact Registry service. You should see a new image in the  **devops-repo**  >  **devops-image**  folder.

![38](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a6cff9a7-8d2b-46df-ab6d-91405011dc54)

![39](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a4e08fde-b7fd-4c22-bc02-d0dd2720156c)

    
9.  Return to the  **Cloud Shell Code Editor**. Find the file  `main.py`  in the  `gcp-course/devops-repo`  folder.
    
10.  In the main() function, change the title property to  `"Hello Build Trigger."`  as shown below:
    

![40](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/53a0c952-95b9-42f5-838e-b5b03f26a789)

```
@app.route("/")
def main():
    model = {"title":  "Hello Build Trigger."}
    return render_template("index.html", model=model)
```

11.  Commit the change with the following command:
```
cd ~/gcp-course/devops-repo
git commit -a -m "Testing Build Trigger"
```


12.  Enter the following to push your changes to Cloud Source Repositories:
```
git push origin master
```

![41](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/81e22e08-2970-45f1-8dc1-32204560f9fe)

13.  Return to the Cloud Console and the  **Cloud Build**  service. You should see another build running.


![42](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/887d788c-bee5-4dbb-a8c2-ccad95bf7c7a)

Click  _Check my progress_  to verify the objective.

Automate Builds with Trigger.

Check my progress

![43](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/d609d01e-3c8c-4dd5-94a2-b254a7e610e4)


## Task 6. Test your build changes

1.  When the build completes, click on it to see its details.
    
2.  Click  **Execution Details**,

![45](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/241ae4b0-885b-4b06-9547-e179d5dae43a)
    
3.  Click the  **Image name**. This redirects you to the image page in Artifact Registry.

![46](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/28ff4777-28a6-4601-983b-80a9b097ac1f)
    
4.  At the top of the pane, click  **copy**  next to the image name. You will need this for the next steps. The format will look as follows.
    

`us-central1-docker.pkg.dev/qwiklabs-gcp-04-ac8940f14d1d/devops-demo/devops-image@sha256:8aede81a8b6ba1a90d4d808f509d05ddbb1cee60a50ebcf0cee46e1df9a54810`

**Note:** Do not use the image name located in Digest.

5.  Go to the  **Compute Engine**  service. As you did earlier, create a new virtual machine to test this image. Click  **DEPLOY CONTAINER**  and paste the image you just copied.
    
6.  Select  **Allow HTTP traffic**.


![47](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/32da1967-4d69-4648-84ac-1916b219fa4f)
    
7.  When the machine is created, test your change by making a request to the VM's external IP address in your browser. Your new message should be displayed.
    

**Note:** You might have to wait a few minutes after the VM is created for the Docker container to start.

Click  _Check my progress_  to verify the objective.

Test your Build Changes.

Check my progress

![49](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/b02a797a-442a-4356-bcb5-bb0e5543b042)


## Congratulations!

you built a continuous integration pipeline using the Google Cloud tools Cloud Source Repositories, Cloud Build, build triggers, and Artifact Registry.
