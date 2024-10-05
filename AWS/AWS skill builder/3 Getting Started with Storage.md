
# Getting Started with Storage

When you consider running your workloads on Amazon Web Services (AWS), you might first consider your storage options. AWS storage provides the services that you need to build the storage solution that’s right for your business. You will review the primary storage types and the differences between them. You will also learn how to identify the right solution in the cloud based on your requirements.

You will then focus on Amazon Simple Storage Service (Amazon S3), an object storage service that offers industry-leading scalability, data availability, security, and performance. Customers of all sizes and industries can use Amazon S3 to store and protect any amount of data for a range of use cases. These use cases include websites, mobile applications, backup and restore, archive, enterprise applications, Internet of Things (IoT) devices, and big data analytics.

In this course, you acquire the knowledge that you need to start using Amazon S3. You learn about the key elements of Amazon S3 and explore how to configure them. You learn how to upload data to Amazon S3 and what additional AWS services you can use to transfer data to Amazon S3 at scale. You also learn the basic elements of security within Amazon S3.


## Objectives

By the end of this course you will be able to do the following:

-   Discuss different types of storage solutions and their features and benefits.
-   Discuss the features and concepts of Amazon S3.
-   Describe Amazon S3 storage classes and associated use cases.
-   Discuss how to use Amazon S3 to create a bucket, upload objects, and work with objects.
-   Describe Amazon S3 configurations for cost savings and security.
-   Identify other AWS storage solutions and their use cases.
-   Use Amazon S3 to create a static website.

###  Content


-   [Task 1: Creating a bucket in Amazon S3]()
-   [Task 2: Configuring a static website on Amazon S3]()
-   [Task 3: Uploading content to your bucket]()
-   [Task 4: Turning on public access to the objects]()
-   [Task 5: Securely sharing an object using a presigned URL]()
-   [Task 6: Using a bucket policy to secure your bucket]()
-   [Task 7: Updating the website]()
-   [Task 8: Exploring file versions]()


## Task 1: Creating a bucket in Amazon S3

In this task, you create an S3 bucket and configure it for static website hosting.

4.  In the  **AWS Management Console**, on the  **Services**  menu, choose  **S3**.
![2](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e7a5374c-065d-4d4a-89e8-def8899bf4cb)

    
5.  Choose  **Create bucket**

![3](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/d37c8560-0bba-4c18-a1b7-a4c60797f262)

    
   - An S3 bucket name is globally unique, and all AWS accounts share the namespace. After you create a bucket, no other AWS accounts in any AWS Regions can use the name of that bucket unless you delete the bucket.
    
  - you use a bucket name that includes a random number, such as  **website-9999**.

![3 1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/50a95989-e145-40fd-bff5-3445c00950f5)
    
6.  For  **Bucket name**, enter
    
   - website-<9999>  and replace  _<9999>_  with a random number.

    Note: check the bucketname with number already exist not accept

   - Public access to buckets is blocked by default. Because the files in your static website will need to be accessible through the internet, you must permit public access.
    
7.  For  **Object Ownership**, choose  **ACLs enabled**.

![5](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/87774e5a-0e5f-48fc-b3ba-62326aa0afb2)
    
8.  Choose  **Bucket owner preferred**.
    
9.  For  **Block Public Access settings for this bucket**, clear the check box for  **Block  _all_  public access**, and then select the box that states  **I acknowledge that the current settings might result in this bucket and the objects within becoming public.**

 ![6](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/ef573d97-2317-4c1e-a554-70be2e7f88f9)
    
11.  For  **Bucket Versioning**, choose  **Enable**.
    
    **Note:**  Once you turn on (enable) bucket versioning, you can’t turn it off.
    
12.  For  **Tags**, choose  **Add tag**, and enter the following:
    

-   **Key:** = Department
    
-   **Value:** =  Marketing

![7](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/c41a71ad-f52d-4534-9f40-43b15544d8ff)
    
   -   You can use tags to add additional information to a bucket, such as a project code, cost center, or owner.

![8](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/fc5987bb-26c4-4317-ab7d-23a838545cc3)

12.  Choose  **Create bucket**


![9](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/2e6ea4a3-9ebb-4c97-81ca-c9d6e4258083)
    
13.  In the  **Buckets**  section, choose the name of your new bucket.
    
14.  Choose the  **Properties**  tab.

![10](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/8da6a933-41ca-4326-a481-d1c5f5c8f388)
    

## Task 2: Configuring a static website on Amazon S3

You will now configure the bucket for static website hosting.

15.  Scroll to the  **Static website hosting**  panel.
    
16.  Choose  **Edit**
    
17.  Configure the following settings:
    

-   **Static web hosting:**  Choose  **Enable**.
-   **Hosting type:**  Choose  **Host a static website**.
-   **Index document:**  Enter
    
    index.html
    
-   **Error document:**  Enter
    
    error.html

![11](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/fdb39526-02c4-4bc4-b9e8-0c94d671849e)
    
   
     **Note**: You must enter index.html and error.html even though they are already displayed.
 

18.  Choose  **Save changes**


![12](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/4b63409c-a1ce-4220-b84a-1d4f478b9677)
    
19.  In the  **Static website hosting**  panel under  **Bucket website endpoint**, choose the link.
    
![13](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/4391221c-cca4-43fa-a56c-fd1efd5ff9cb)

  -   You receive a  _403 Forbidden_  message because you have not yet configured the bucket permissions. Keep this tab open in your web browser so that you can return to it later.
    
    - You have configured your bucket to host a static website.

![14](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/96f8e028-8ba0-4190-b791-ea50cfc48335)
    

## Task 3: Uploading content to your bucket

In this task, you upload the static files to your bucket.

20.  Choose (right-click) each of the following links, and download the files to your computer:

Ensure that each file keeps the same file name, including the extension.

-   [index.html](https://us-west-2-tcprod.s3.us-west-2.amazonaws.com/courses/CUR-TF-100-EDSTOR/v1.0.2.prod-68c99051/01-lab-s3/instructions/assets/index.html)
-   [script.js](https://us-west-2-tcprod.s3.us-west-2.amazonaws.com/courses/CUR-TF-100-EDSTOR/v1.0.2.prod-68c99051/01-lab-s3/instructions/assets/script.js)
-   [style.css](https://us-west-2-tcprod.s3.us-west-2.amazonaws.com/courses/CUR-TF-100-EDSTOR/v1.0.2.prod-68c99051/01-lab-s3/instructions/assets/style.css)

21.  Return to the Amazon S3 console, and choose the  **Objects**  tab.
    
22.  Choose  **Upload**

![15](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/56bddfc4-16ef-4b94-86d6-a0fde3a2c7d1)
    
23.  Choose  **Add files**

24.  Choose the three files that you downloaded.


![16](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/3f93a4fe-2799-4b19-affc-071570d46ed2)
    

    
25.  Choose  **Upload**



![17](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/509dfce5-c39e-43b1-886c-496b26578391)
    

Your files are uploaded to the bucket.

26.  Choose  **Close**

![18](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/4763d0ba-60bc-434f-b916-c32353e643a3)


## Task 4: Turning on public access to the objects

Objects that are stored in Amazon S3 are private by default. This setting helps keep your organization’s data secure.

you make the uploaded objects publicly accessible so users can view your website.

First, confirm that the objects are currently private.

27.  Return to the browser tab that showed the  _403 Forbidden_  message.
    
28.  Refresh  the webpage.
    

If you accidentally closed this tab, go to the  **Properties**  tab, and in the  **Static website hosting**  panel, choose the  **Bucket website endpoint**  link again.

You should still see a  _403 Forbidden_  message. This response is expected! This message indicates that your static website is being hosted by Amazon S3 but that the content is private.

You can make Amazon S3 objects public through two different ways:

-   To make either a whole bucket public or a specific directory in a bucket public, use a bucket policy.
    
-   To make individual objects in a bucket public, use an access control list (ACL). It is normally safer to make individual objects public because doing so avoids accidentally making other objects public. However, if you know that the entire bucket contains no sensitive information, you can use a bucket policy.
    
    You now configure the individual objects to be publicly accessible.
    

29.  Keep the website tab open, and return to the web browser tab with the Amazon S3 console.

![19](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/b126703f-4557-46ee-b055-7d9c10933615)

    
30.  Choose  all three objects.

![20](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/0624d2a7-6490-447a-bb13-343e735c87e7)
    
31.  In the  **Actions**  menu, choose  **Make public using ACL**.

![21](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/b2af2980-6fd3-4cdd-b985-462eca5f4077)
    

A list of the three objects is displayed.

32.  Choose  **Make public**

![22](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e7da4570-c0e0-4e11-b9a7-593e43858496)

Your static website is now publicly accessible.

33.  Choose  **Close**



![23](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/01013191-c515-49c3-8657-3393e13e5e3e)

    
34.  Return to the web browser tab that has the  _403 Forbidden_  message.

![14](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/96f8e028-8ba0-4190-b791-ea50cfc48335)
    
35.  Refresh  the webpage.
    
![24](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/4c4cbf52-5df9-4fe2-b3f3-753982c29cff)

You should now see the static website that is being hosted by Amazon S3.

Now you know how to share objects with everyone by making them public. However, there may be times when you need to share an individual object for a limited amount of time. In the next task, you learn how to temporarily share an object.

## Task 5: Securely sharing an object using a presigned URL

When you need to temporarily and securely share an object with a person or group of people, you can create a presigned URL. When you create the URL, you must configure how long the URL will be valid. Then, you can share this URL with the users who should have access to the object.

As long as the presigned URL is valid, anyone who has it can get to the object. Avoid keeping the URL active longer than necessary, and only share the URL with people you trust.

36.  Choose (right-click) the following link, and download the file to your computer:  Ensure that the file keeps the same file name, including the extension.

-   [new-report.png](https://us-west-2-tcprod.s3.us-west-2.amazonaws.com/courses/CUR-TF-100-EDSTOR/v1.0.2.prod-68c99051/01-lab-s3/instructions/assets/new-report.png)

37.  Return to the Amazon S3 console, and choose the  **Objects**  tab.
    
38.  Choose  **Upload**
    
39.  Choose  **Add files**
    
40.  Choose the file that you downloaded.
    
41.  Choose  **Upload**


![25](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/be74592a-9d01-46c1-a163-2cd928b9908b)
    

You have uploaded your file to the bucket.

42.  Choose  **Close**

![26](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e26bdd14-f8b3-49f6-82db-f21611573049)

    
   -  Like when you first uploaded the website files, the  **new-report.png**  file is private by default. This time, instead of making the object public, you create a presigned URL to access the file.
    
43.  In the  **Objects**  tab, choose  **new-report.png**.
    
44.  From the  **Actions**  menu, select  **Share with a presigned URL**

![27](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/5d278249-ba5b-4588-bcc4-b8359f572f5a)

    
45.  In the pop-up window, configure the  **Time interval until the presigned URL expires**:
    

-   Choose  **Minutes**

46.  Choose  **Create presigned URL**



![28](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f91e4612-9266-4eca-bc80-2e21179a33ae)

    
47.  From the banner at the top of the page, choose  **Copy presigned URL**.

![29](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/c29ded2e-95a0-4af5-bec2-7e700a2cec74)
    
48.  Open a new browser tab, and paste the URL you copied into the address bar.
    
 -    A report is displayed in the web browser.

![30](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a6bf57c7-5ced-4640-bd5f-6a15ae35aaef)
    
   -  If you wait 1 minutes and use the link again, you will find that the URL has expired and no longer works.
![31](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/9260b6b8-6aa3-464e-ae07-ed4716da251c)


    

## Task 6: Using a bucket policy to secure your bucket

You want to protect your website files and make sure that no one can delete them. To do this, you apply a bucket policy that denies delete privileges on your website files.

49.  Return to the Amazon S3 console, and choose the  **Permissions**  tab.

![32](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/02a115dd-e0d6-4c48-b419-bb1d1f247b74)

50.  Under  **Bucket policy**, choose  **Edit**

![33](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f9f73e4a-4767-43f9-bed7-d5d9333332d2)

51.  Copy the following policy text. In the  **Policy**  text editor, replace the existing policy text with this text:

```
{
	"Version": "2012-10-17",
	"Id": "MyBucketPolicy",
	"Statement": [
		{
			"Sid": "BucketPutDelete",
			"Effect": "Deny",
			"Principal": "*",
			"Action": "s3:DeleteObject",
			"Resource": [
				"arn:aws:s3:::<bucket-name>/index.html",
				"arn:aws:s3:::<bucket-name>/script.js",
				"arn:aws:s3:::<bucket-name>/style.css"
        ]
		}
	]
}
```

- This policy prevents everyone from deleting the three files that make your website work.

52.  Next, you update the text in the policy editor. In the following lines of code in the policy editor, replace the  _<bucket-name>_  placeholders with the name of your bucket.

```
"arn:aws:s3:::<bucket-name>/index.html",
"arn:aws:s3:::<bucket-name>/script.js",
"arn:aws:s3:::<bucket-name>/style.css"
```


- Your updated code should look similar to the following:

```
"arn:aws:s3:::website-9999/index.html",
"arn:aws:s3:::website-9999/script.js",
"arn:aws:s3:::website-9999/style.css"
```
![34](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/559c430e-f542-4a63-9233-b3af486ef9fb)



**Note:**  Your bucket name will be different. Be sure to use the name of the bucket that you created.

53.  Choose  **Save changes**


![35](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/61b9c9ba-45a2-489c-a360-142b53be5595)
    
54.  Return to the the  **Object tab**
    
55.  Select  **index.html**.

![36](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/40283dcf-c5f3-45bf-aed5-5950f054f337)
    
56.  Choose  **Delete**.
    
57.  In the  **Delete objects**  panel, enter
    
    delete
    
    to confirm that you want to remove this file.
    
58.  Choose  **Delete objects**

![37](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/41e65271-b26a-4f71-9ec3-302032152fb7)
    
59.  Notice that the  **index.html**  file is listed in the  **Failed to delete**  pane.

![38](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/5f040ddc-bd06-4794-b034-8abd1edc4956)
    
  -   This confirms that your policy is working and preventing the website’s files from being deleted.
    
60.  Choose  **Close**  to return to the  **Objects**  tab.
    

## Task 7: Updating the website

Although you have configured a policy to prevent deletion of website files, you can still update the website by editing the HTML file and uploading it to the S3 bucket again.

Amazon S3 is an object storage service, so you must upload the whole file. This action replaces the existing object in your bucket. You cannot edit the contents of an object; instead, you must replace the whole object.

61.  On your computer, load the  **index.html**  file into a text editor (for example, Notepad or TextEdit).
    
62.  Find the text  **Served from Amazon S3**, and replace it with
    
    Created by <YOUR-NAME>
    
    and substitute your name for  _<YOUR-NAME>_  (for example,  **Created by DD**).

![notepad](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/1f6325db-1e2e-4bae-b48d-eaf604c41caa)
    
63.  Save the file.
    
64.  Return to the Amazon S3 console, and upload the  **index.html**  file that you just edited.

![39](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f6044039-310a-4521-bdec-62440ba57298)

![40](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/2730bea0-30cb-4814-ab10-a711e231412a)
    
65.  Choose  **index.html**, and in the  **Actions**  menu, choose the  **Make public using ACL**  option again.

![41](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/91f87428-897e-4b5a-8a61-0ee30410a141)

    
66.  Choose  **Make public**.


![42](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f85732a1-265e-42ce-89ab-b6a98f5a1c3c)
    
![43](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/49f1d0fa-354c-44ff-a31f-6800b3dcde6f)

67.  Return to the web browser tab with the static website, and refresh  the page.

![44](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/216c80f5-b7e8-412e-9dbe-a8109c32f9bb)

    

Your name should now be on the page.

Your static website is now accessible on the internet. Because it is hosted on Amazon S3, the website has high availability and can serve high volumes of traffic without using any servers.

## Task 8: Exploring file versions

Bucket versioning is turned off by default. When versioning is turned off, changes to objects can’t be undone. For example, if you upload a new version of a file, the old file is replaced with the new one. The original file is lost. If you delete a file, it is permanently deleted, and you can’t get it back.

However, when versioning is turned on, changed and deleted versions of files are saved. Previous versions of objects are not presented by default, but you can access them using the console or programmatically. Because you are keeping earlier versions of objects, you can recover them if you need to.

It is important to remember that once you turn on version, you cannot turn it off. However, you can suspend versioning. For more information on bucket versioning, see the  [Amazon Simple Storage Service Users Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html).

Recall that when you created your bucket, you turned on versioning. In this task, you view the object versions available in your bucket.

68.  Return to the Amazon S3 console, and choose the  **Objects**  tab.
    
69.  Choose  **Show versions**  to turn on bucket versioning.
    
70.  Review the list of objects in the bucket.
    
![45](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f60a27ac-b276-4de4-9ff3-b0c4758c842a)


-   Notice that each file has a  **Version ID**. These IDs are automatically generated by Amazon S3 when versioning is turned on.
-   You should also find two versions of the  **index.html**  file because you uploaded a new version of the file. The current version is the file that you uploaded when you updated your website.

## Summary

you created a personalized, publicly accessible static website. You learned how to use a presigned URL to temporarily share objects in your bucket. You also protected your work with a bucket policy that prevents file deletion and turned on bucket versioning in case you need to recover previous versions of files. Excellent work!