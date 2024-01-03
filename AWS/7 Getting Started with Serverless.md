
# Getting Started with Serverless

AWS Lambda is a compute service that lets you run code without provisioning or managing servers. Lambda runs your code on a high-availability compute infrastructure and performs all the administration of the compute resources, including server and operating system maintenance, capacity provisioning and automatic scaling, and logging. With Lambda, you can run code for virtually any type of application or backend service.

In this Module, you acquire the knowledge that you need to start using AWS Lambda. You learn about the benefits of serverless services and how to use serverless services to decouple your architectures. You learn about the key concepts and features of AWS Lambda including creating functions, configuring functions, monitoring and best practices. You also learn about additional AWS serverless services that are available to you.


# Getting Started with AWS Lambda

you create and configure an AWS Lambda function to be initiated when an image is uploaded to an Amazon Simple Storage Service (Amazon S3) bucket. You review related logs to determine how the function is performing. You modify the function configuration to optimize for performance.

### Objectives

you will know how to do the following:

-   Create a Lambda function.
    
-   Configure an S3 trigger on a Lambda function.
    
-   Observe logs and metrics for a Lambda function to determine performance.
    
-   Size and configure a Lambda function for optimal performance.
    
    
## Accessing the AWS Management Console

1.  choose AWS.
    
   - This opens the AWS Management Console in a new browser tab. The system automatically logs you in.
    
2.  Arrange the **AWS Management Console** tab so that it displays along side these instructions. Ideally, you will be able to see both browser tabs at the same time so that you can follow the lab steps more easily.

![1](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/15afb7cf-7ea2-4df2-81ea-4e0dc3d8a63b)


## Task 1: Creating a Lambda function

3.  In the **AWS Management Console**, on the **Services** menu, enter **Lambda**. From the search results, choose **Lambda**.

![2](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/8011b218-9b7d-4456-902d-ff527b74b36c)
    
4.  Choose **Create Function**.

![3](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/6720c0cf-5c4a-46b5-8574-3139217e1d94)
    
5.  Edit the following: **Function name:**  `resize_image` **Runtime:** Python3.9


![4](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/2c4add0b-e7d2-4687-b94f-b74b3fe51e25)
    
6.  Expand the **Change default execution role** section. Choose **Use an existing role**. In the dropdown list for **Existing Role**, choose **ResizeImageLambdaRole**.

![5](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/b6db47ec-bd89-4d76-a5e7-0119ca8a7ed1)
    
7.  Choose **Create function**.

![6](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/bd5d0626-4d66-4fe2-9d56-6a3075b5520a)
 
8.  Scroll to the **Layers** section.

![7](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/178880c6-4acd-4961-80d7-69b1a0946180)

   9.  Choose **Add a layer**.
    
10.  Choose **Custom layers**.
    
11.  From the **Custom layers** dropdown list, choose **PillowPythonLambdaLayer**.
    
12.  From the **Version** dropdown list, choose **1** or the option with the highest version number.

![8](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/e17b3e5d-a2f1-4037-8412-e3b1dd2ef6f2)
    
13.  Choose **Add**.

![9](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/550709fc-1e9b-4d1c-8746-b65f9cef51fa)
   

14.  Scroll to the **Code source** section of the page.


![10](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/88392768-6ebc-4dcb-adf1-d79c0db9946d)
    
15.  Copy the code below, and replace the default source code in the lambda_function.py file with it.
    
```
import boto3

import os

import sys

import uuid

from urllib.parse import unquote_plus

from PIL import Image

import PIL.Image

s3_client = boto3.client('s3')

def resize_image(image_path, resized_path):

 with Image.open(image_path) as image:

 image.thumbnail(tuple(x / 2 for x in image.size))

 image.save(resized_path)

def lambda_handler(event, context):

 print('Begin resizing image')

 for record in event['Records']:

 bucket = record['s3']['bucket']['name']

 key = unquote_plus(record['s3']['object']['key'])

 print(bucket)

 print(key)

 tmpkey = key.replace('/', '')

 download_path = '/tmp/{}{}'.format(uuid.uuid4(), tmpkey)

 upload_path = '/tmp/resized-{}'.format(tmpkey)

 s3_client.download_file(bucket, key, download_path)

 resize_image(download_path, upload_path)

 s3_client.upload_file(upload_path, os.environ['RESIZED_BUCKET'], key)

 print('Resizing image complete')
```
16.  To deploy your Lambda function, choose **Deploy**.

![11](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/60177a65-d99d-4a25-bad0-e0b60cb19ed2)
    
17.  Choose the **Configuration** tab, and then choose **General configuration**. Choose **Edit**.
    
18.  In the **Memory** field, enter `512` MB. Then, choose **Save**.

![12](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/8465d03e-9c82-4f09-bf62-184d98fc6e5f)
    
19.  At the top of these instructions, choose Details. Next to AWS, choose Show. Copy the value next to **ResizedBucketName**. Use it as the value in step 23.
    
20.  In the **AWS Management Console**, choose **Environment variables**.
    
21.  Choose **Edit**.
    
22.  Choose **Add environment variable**.
    
23.  Enter the following values: **Key:**  `RESIZED_BUCKET` **Value:** Enter the value that you retrieved in step 19.


![13](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/b36ef641-5b87-4a24-be2a-da5109f73548)
    
24.  Choose **Save**.
    

You have created a Lambda function.

## Task 2: Configuring an Amazon S3 trigger to invoke a Lambda function

In this task, you configure an S3 trigger on an existing S3 bucket and your Lambda function. The Lambda function resizes images and places them in another bucket.

24.  In the **Function overview** section of the Lambda console near the top of the page, choose **Add trigger**.


    
25.  In the **Trigger configuration** section, choose **S3** from the dropdown list.
    
26.  For Bucket, choose the bucket with **original** in the name.
    
27.  For Event Type, choose **All object create events**.
    
28.  Acknowledge the notification for **Recursive invocation** by selecting the check box.

![15](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/b8447edd-99c0-4f2f-8149-dfc7eb74391e)

    
29.  Choose **Add**.
    
![16](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/76745b8a-51bb-487a-891d-f0e5080008de)

You have configured your Lambda function to be initiated when a new object is uploaded to the S3 bucket.

## Task 3: Uploading an image to the Amazon S3 bucket

In this task, you upload an image file to your bucket.

30.  Open the context (right-click) menu for the following link, and download the file to your computer:
    

-   [large-image.jpg](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/d4632100-e1a7-4acc-85d4-f8f4d2b2d0b1)

![large-image](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/d4632100-e1a7-4acc-85d4-f8f4d2b2d0b1)
    

31.  In the **AWS Management Console**, on the **Services** menu, enter **S3**. From the search results, choose **S3**.


![17](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/87f1a665-8820-4649-9a78-fa7f6481933c)

    
32.  Choose the link for the bucket that has **original** in the name.

![18](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/df08a404-60e4-4695-8e44-e23695881edd)
    
33.  Choose **Upload**.


![19](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/5458fe82-5866-4cd2-8205-d5a4143bc172)
    
34.  Choose **Add files**.
    
35.  Choose the file that you downloaded.

![20](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/08cbc4fc-4ac5-4181-8312-d6052eac7095)
    
36.  Choose **Upload**. Your file is uploaded to the bucket.

![21](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/db25be55-37af-4e5a-b30a-dba7ade5011c)
    
37.  Choose **Close**.
    

_If you are working on Task 4, you can now return to [step 51]()

When your Lambda function runs correctly, the image file that you uploaded is reduced in size and placed in the S3 bucket that you specified when you set the environment variable for **RESIZED_BUCKET**.

38.  Return to the **Buckets** section in the S3 Console.
    
39.  Choose the link for the bucket that has **resized** in the name.
    

Notice the file size. It's significantly reduced from the original size of 4.9 MB.

  

When you uploaded the image file, S3 initiated the **resize_image** Lambda function. Review the logs to see how your function performed.

![22](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/13e26fd1-a178-45a5-8e4d-6696c05412c4)

40.  Navigate back to the Lambda console.
    
41.  Choose the link for the **resize_image** function.
    
42.  Choose the **Monitor** tab.
    
43.  Choose **Logs**.
    
44.  In the **Recent Invocations** table, choose a row to expand the details. Notice the metrics that are recorded for each function invocation. You might have to wait for up to one minute for the data to be updated.
   
        The **DurationInMS** column tells you how long your function ran for this invocation.
    
   The first time that your Lambda function is invoked, the Lambda execution environment has to download your code and start a new execution environment. This process is called a cold start. The **@initDuration** metric in the **Recent invocation** details signifies the cold start time.
    
    Note the **MemorySetInMB** column. The amount of memory that's available to your Lambda function can be adjusted to affect the performance of your Lambda function.
        
   The amount of memory also determines the amount of virtual CPU available to a function. Adding more memory proportionally increases the amount of CPU, which increases the overall computational power available. If a function is CPU-, network- or memory-bound, then changing the memory setting can dramatically improve its performance.

![23](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/a66358a2-2c73-402b-99af-4f19456c823f)

  
![24](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/b394e72e-951b-4a02-9207-e57dcd181486)  
    Notice how long it took your function to run. It could be faster. Adjust your Lambda function so that it runs faster.
    

## Task 4: Optimizing Lambda function memory for performance

45.  Choose the **Configuration** tab.
    
46.  Choose **General Configuration**.
    
47.  Choose **Edit**.

![25](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/b50e02e7-f126-42f4-8dab-f2e50356efcc)
    
48.  Adjust **Memory** to `1024` MB.

![26](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/21496291-1537-4008-894f-bed70ad76a01)
    
49.  Choose **Save**.
    

![27](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/78350b93-acc6-4a2c-b564-583854f036a2)


50.  Upload your image to the original S3 bucket again. If you need help, review steps [32-38]().

![28](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/6500c6bf-d316-43f3-88c0-a6567a7b86f1)

![29](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/402fcee2-0e4a-47e6-972b-f0c676f227c5)

![30](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/f0e4fa18-80ae-46ed-98ec-eefeb295b94d)

51.  Repeat steps 45-49 using `2048` MB and `3008` MB as the value for **Memory**.
    
![31](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/cd8700c0-07f8-4de1-8430-8df33537f6f9)

Your function now runs in approximately 500 milliseconds with 3008 MB of memory and an image that is 5 MB.

## Summary

you created a Lambda function and configured an S3 trigger on that Lambda function. You uploaded an image to an S3 bucket which initiated the Lambda function to resize the image and place it in another bucket. After reviewing the logs to see performance metrics, you optimized the Lambda function by increasing the available memory for the function.


## Keytakeaway

you will be able to do the following:
-   Describe microservices and Serverless concepts.
-   Discuss event-driven architectures.
-   Describe the features and benefits of AWS Lambda functions.
-   Discuss how to configure AWS Lambda functions.
-   Identify how to monitor AWS Lambda functions.
-   Describe the best practices for working with AWS Lambda.
-   Identify the features and benefits of additional AWS Serverless services.

![Capture](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/1aa84a2f-53cc-4506-a6f1-e0b1a442d353)

**Credits : AWS Educate**