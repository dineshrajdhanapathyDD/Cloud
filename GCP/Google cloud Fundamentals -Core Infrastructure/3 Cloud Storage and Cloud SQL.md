

# Google Cloud Fundamentals: Getting Started with Cloud Storage and Cloud SQL



## Overview

In this lab, you create a Cloud Storage bucket and place an image in it. You also configure an application running in Compute Engine to use a database managed by Cloud SQL. For this lab, you configure a web server with PHP, a web development environment that is the basis for popular blogging software. Outside this lab, you will use analogous techniques to configure these packages.

You also configure the web server to reference the image in the Cloud Storage bucket.

## Objectives

In this lab, you learn how to perform the following tasks:

-   Create a Cloud Storage bucket and place an image into it.
-   Create a Cloud SQL instance and configure it.
-   Connect to the Cloud SQL instance from a web server.
-   Use the image in the Cloud Storage bucket on a web page.

## Task 1. Sign in to the Google Cloud Console

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

## Task 2. Deploy a web server VM instance

1.  In the Google Cloud Console, on the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **Compute Engine**  >  **VM instances**.
    
2.  Click  **Create Instance**.
    
3.  On the  **Create an Instance**  page, for  **Name**, type  `bloghost`
    
4.  For  **Region**  and  **Zone**, select the region and zone assigned by Qwiklabs.


![1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/9287ce4b-ceca-4236-828c-e5f4b3534b18)
    
5.  For  **Machine type**, accept the default.
    
6.  For  **Boot disk**, if the  **Image**  shown is not  **Debian GNU/Linux 11 (bullseye)**, click  **Change**  and select  **Debian GNU/Linux 11 (bullseye)**.
    
7.  Leave the defaults for  **Identity and API access**  unmodified.
    
8.  For  **Firewall**, click  **Allow HTTP traffic**.
    
9.  Click  **Advanced options**  to open that section of the dialog.
    
10.  Click  **Management**  to open that section of the dialog.
    
11.  Scroll down to the Automation section, and enter the following script as the value for  **Startup script**:
    
```
apt-get update
apt-get install apache2 php php-mysql -y
service apache2 restart
```
- Copied!


![2](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/ac739f24-265c-4d20-8fd9-2d49093e42fa)

**Note:**  Be sure to supply that script as the value of the  **Startup script**  field. If you accidentally put it into another field, it won't be executed when the VM instance starts.

12.  Leave the remaining settings as their defaults, and click  **Create**.

**Note:**  Instance can take about two minutes to launch and be fully available for use.

13.  On the  **VM instances**  page, copy the  **bloghost**  VM instance's internal and external IP addresses to a text editor for use later in this lab.

- Click  _Check my progress_  to verify the objective.

- Deploy a web server VM instance

- Check my progress


![3](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/91d626c3-9c3b-4797-9c62-b3d69a0e8014)

## Task 3. Create a Cloud Storage bucket using the gcloud storage command line

All Cloud Storage bucket names must be globally unique. To ensure that your bucket name is unique, these instructions will guide you to give your bucket the same name as your Google Cloud project ID, which is also globally unique.

Cloud Storage buckets can be associated with either a region or a multi-region location:  **US**,  **EU**, or  **ASIA**. In this activity, you associate your bucket with the multi-region closest to the region and zone that Qwiklabs or your instructor assigned you to.

1.  On the  **Google Cloud console**, on the top right toolbar, click the  **Activate Cloud Shell**  ![Activate Cloud Shell icon](https://cdn.qwiklabs.com/ep8HmqYGdD%2FkUncAAYpV47OYoHwC8%2Bg0WK%2F8sidHquE%3D). If a dialog box appears, click  **Continue**.

![4](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e529915f-bbd7-4b61-bcb4-949d6a1b5592)
    
2.  For convenience, enter your chosen location into an environment variable called LOCATION. Enter one of these commands:
    

`export LOCATION=US`

Or

`export LOCATION=EU`

Or

`export LOCATION=ASIA`



3.  In Cloud Shell, the DEVSHELL_PROJECT_ID environment variable contains your project ID. Enter this command to make a bucket named after your project ID:

`gcloud storage buckets create -l $LOCATION gs://$DEVSHELL_PROJECT_ID`



If prompted, click  **Authorize**  to continue.

4.  Retrieve a banner image from a publicly accessible Cloud Storage location:

`gcloud storage cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png`



5.  Copy the banner image to your newly created Cloud Storage bucket:

`gcloud storage cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png`



6.  Modify the Access Control List of the object you just created so that it's readable by everyone:

`gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png`

- Copied!

![5](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/9d4b0952-005a-4f2f-ab6c-a36e52a1f548)


- Click  _Check my progress_  to verify the objective.

- Create a Cloud Storage bucket using the gcloud storage command line

- Check my progress

![6](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/133860ec-dcee-4a59-8373-5faf4a93a948)

## Task 4. Create the Cloud SQL instance

1.  In the Google Cloud Console, on the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **SQL**.
    
2.  Click  **Create instance**.
    
3.  For  **Choose a database engine**, select  **Choose MySQL**.
    
4.  For  **Instance ID,**  type  **blog-db**, and for  **Root password**  type a password of your choice.
    
![8](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/ea0c2548-7e9f-4201-a764-e2e3a425c5a2)

**Note:**  Choose a password that you remember. There's no need to obscure the password because you use mechanisms to connect that aren't open access to everyone.

5.  For  **Choose a Cloud SQL edition**, click  **Enterprise**  and then select  **Sandbox**  from the dropdown.
    
6.  Select  **Single zone**  and set the region and zone assigned by Qwiklabs.
    
  ![9](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f6810c89-661f-43ae-90c0-df7d812cdf3e)  

**Note:**  This is the same region and zone into which you launched the  **bloghost**  instance. The best performance is achieved by placing the client and the database close to each other.

7.  Click  **Create Instance**.

**Note:**  Wait for the instance to finish deploying. It will take a few minutes.

8.  Click the name of the instance,  **blog-db**, to open its details page.


![10](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/b78a6288-68f8-4b8e-8fea-e151d2136564)
    
9.  From the SQL instances details page, copy the  **Public IP address**  for your SQL instance to a text editor for use later in this lab.
    
10.  Click  **Users**  menu on the left-hand side, and then click  **Add User Account**.
    
11.  For  **User name**, type  `blogdbuser`
    
12.  For  **Password**, type a password of your choice. Make a note of it.
    
13.  Click  **Add**  to add the user account in the database.
    
![11](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a485faf0-c19d-4b72-a47c-2646c1d97e6e)

**Note:**  Wait for the user to be created.

14.  Click  **Connections**  menu on the left-hand side, and then click  **Networking**  tab.
    
15.  Click  **Add a Network**.
    

**Note:**  If you're offered the choice between a  **Private IP**  connection and a  **Public IP**  connection, choose  **Public IP**  for purposes of this lab.

**Note:**  The  **Add network**  button may be unavailable if the user account creation is not yet complete.

16.  For  **Name**, type  `web front end`
    
17.  For  **Network**, type the external IP address of your  **bloghost**  VM instance, followed by  `/32`
    

The result will look like this:

35.192.208.2/32

**Note:**  Be sure to use the external IP address of your VM instance followed by /32. Do not use the VM instance's internal IP address. Do not use the sample IP address shown here.

18.  Click  **Done**  to finish defining the authorized network.
    
19.  Click  **Save**  to save the configuration change.
    
![12](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/ae3e83ae-4658-4aff-b365-6e361b2d9c50)

**Note**: If the message appears like  **Another operation is in progress**, wait for few minutes until you see the green check for  **blog-db**  to save the configuration.

- Click  _Check my progress_  to verify the objective.

- Create the Cloud SQL instance

- Check my progress

![13](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/3b318853-29fb-4c5b-ad60-05396fa9e668)


## Task 5. Configure an application in a Compute Engine instance to use Cloud SQL

1.  On the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **Compute Engine**  >  **VM instances**.
    
2.  In the VM instances list, click  **SSH**  in the row for your VM instance  **bloghost**.
    
![16](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/8707ae8f-a042-444e-a6f6-206dee5c7e5b)

3.  In your ssh session on  **bloghost**, change your working directory to the document root of the web server:
    

`cd /var/www/html`



4.  Use the  **nano**  text editor to edit a file called  **index.php**:

`sudo nano index.php`



5.  Paste the content below into the file:

```
<html>
<head><title>Welcome to my excellent blog</title></head>
<body>
<h1>Welcome to my excellent blog</h1>
<?php
 $dbserver = "CLOUDSQLIP";
$dbuser = "blogdbuser";
$dbpassword = "DBPASSWORD";
// In a production blog, we would not store the MySQL
// password in the document root. Instead, we would store it in a
// configuration file elsewhere on the web server VM instance.

$conn = new mysqli($dbserver, $dbuser, $dbpassword);

if (mysqli_connect_error()) {
        echo ("Database connection failed: " . mysqli_connect_error());
} else {
        echo ("Database connection succeeded.");
}
?>
</body></html>
```


**Note:**  In a later step, you will insert your Cloud SQL instance's IP address and your database password into this file. For now, leave the file unmodified.

6.  Press  **Ctrl+O**, and then press  **Enter**  to save your edited file.
    
7.  Press  **Ctrl+X**  to exit the nano text editor.
    
8.  Restart the web server:
    

`sudo service apache2 restart`



9.  Open a new web browser tab and paste into the address bar your  **bloghost**  VM instance's external IP address followed by  **/index.php**. The URL will look like this:

35.192.208.2/index.php

![14](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/13ca7845-0053-4911-a3b3-0d8c31c60a3f)


**Note:**  Be sure to use the external IP address of your VM instance followed by /index.php. Do not use the VM instance's internal IP address. Do not use the sample IP address shown here.

When you load the page, you will see that its content includes an error message beginning with the words:

Database connection failed: ...

**Note:**  This message occurs because you have not yet configured PHP's connection to your Cloud SQL instance.

10.  Return to your ssh session on  **bloghost**. Use the  **nano**  text editor to edit  **index.php**  again.

`sudo nano index.php`



11.  In the  **nano**  text editor, replace  `CLOUDSQLIP`  with the Cloud SQL instance Public IP address that you noted above. Leave the quotation marks around the value in place.
    
12.  In the  **nano**  text editor, replace  `DBPASSWORD`  with the Cloud SQL database password that you defined above. Leave the quotation marks around the value in place.
    
13.  Press  **Ctrl+O**, and then press  **Enter**  to save your edited file.
    
14.  Press  **Ctrl+X**  to exit the nano text editor.
    
15.  Restart the web server:
    
```
sudo service apache2 restart
```
- Copied!



16.  Return to the web browser tab in which you opened your  **bloghost**  VM instance's external IP address. When you load the page, the following message appears:

Database connection succeeded.

**Note:**  In an actual blog, the database connection status would not be visible to blog visitors. Instead, the database connection would be managed solely by the administrator.

## Task 6. Configure an application in a Compute Engine instance to use a Cloud Storage object

1.  In the Google Cloud Console, click  **Cloud Storage > Buckets**.
    
2.  Click the bucket that is named after your GCP project.
    
3.  In this bucket, there is an object called  **my-excellent-blog.png**. Copy the URL behind the link icon that appears in that object's  **Public access**  column, or behind the words "Public link" if shown.
  
  ![15](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/99ac2426-53b7-4806-ac13-38d2246b5f5d)  
    

**Note:**  If you see neither a link icon nor a "Public link", try refreshing the browser. If you still do not see a link icon, return to Cloud Shell and confirm that your attempt to change the object's Access Control list with the  **gsutil acl ch**  command was successful.

4.  Return to your ssh session on your  **bloghost**  VM instance.
    
5.  Enter this command to set your working directory to the document root of the web server:
    

`cd /var/www/html`



6.  Use the  **nano**  text editor to edit  **index.php**:

`sudo nano index.php`



7.  Use the arrow keys to move the cursor to the line that contains the  **h1**  element. Press  **Enter**  to open up a new, blank screen line, and then paste the URL you copied earlier into the line.
    
8.  Paste this HTML markup immediately before the URL:
    

<img src='

9.  Place a closing single quotation mark and a closing angle bracket at the end of the URL:

```
'>

The resulting line will look like this:

 <img src='https://storage.googleapis.com/qwiklabs-gcp-00-90441971045e/my-excellent-blog.png'>


The effect of these steps is to place the line containing  `<img src='...'>`  immediately before the line containing  `<h1>...</h1>`
```

**Note:**  Do not copy the URL shown here. Instead, copy the URL shown by the Storage browser in your own Cloud Platform project.

10.  Press  **Ctrl+O**, and then press  **Enter**  to save your edited file.
    
11.  Press  **Ctrl+X**  to exit the nano text editor.
    
12.  Restart the web server:
    

`sudo service apache2 restart`


![17](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/d5f88d8d-5224-4dfc-a356-6764b87dc029)




13.  Return to the web browser tab in which you opened your  **bloghost**  VM instance's external IP address. When you load the page, its content now includes a banner image.

![18](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f0ef00ee-b90c-47d7-8200-74ffb0999cb2)

In this lab, I configured a Cloud SQL instance and connected an application in a Compute Engine instance to it. You also worked with a Cloud Storage bucket.

## End lab






