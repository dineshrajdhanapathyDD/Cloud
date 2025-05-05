<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Encrypt Data with AWS KMS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-kms)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-security-kms_w0x1y2z3)

---

# Encrypt Data with AWS KMS

Protect a database using encryption with AWS KMS!



WHAT YOU'LL NEED

-   An AWS account -  [Create one here!](https://link.nextwork.org/projects/aws-account-setup?utm_source=project-app)

KEY CONCEPTS

-   [AWS Key Management Service (KMS)](https://aws.amazon.com/kms/)
-   [Amazon DynamoDB](https://aws.amazon.com/dynamodb/)
-   [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)



## ⚡️ 30 second Summary

Welcome to this hands-on project on **data encryption** with **AWS KMS** (Key Management Service)!

Data security is a big deal - it's how companies and engineers (like you) protect sensitive information, customer data, or even national secrets. That's why data breaches are often [a top concern of company leaders](https://www.statista.com/statistics/1315411/concerns-of-cyber-business-leaders-worldwide/), and they're costing companies an average of [$4.5 million](https://secureframe.com/blog/data-breach-statistics) to resolve and recover from.

So how can you protect your data from unauthorized access, while making sure the right people can see and use it?

That’s where encryption comes in.

**Encryption** converts data into a secure format that only authorized users can transform back and read. You use **encryption keys**, which are like digital codes, to encrypt and decrypt the data.

  

**Get ready to...**

-   🔑 Create encryption keys with **AWS KMS (Key Management Service).**
    
-   🗄️ Encrypt a **DynamoDB** database with a KMS key.
    
-   ➕ Add and retrieve data from your database to **test** your encryption.
    
-   🕵️‍♀️ Observe how AWS stops **unauthorized** access to your data.
    
-   💎 Give a user encryption access.
  
  
![](https://learn.nextwork.org/projects/static/aws-security-kms/architecture-complete.png)  

This project is highly relevant for roles like **Cloud Security Engineer,** **Solutions Architect,** or **DevOps Engineer**—where it is a key responsibility to safeguard cloud environments and set up secure access to resources.

-------

## 🔑 Step #1

### Create a KMS Key

  

We're kicking things off by creating a key in AWS Key Management Service (KMS). This key will encrypt data in a DynamoDB table.

  
  

**In this step, you're going to:**

-   Create a key for encryption.
    
-   Set up the admins and users of that key.
    

> 💡 **What is encryption?**  
> **Encryption** is a process that uses algorithms to convert data into a secure format called ciphertext. Only authorised users can decrypt and restore the data to its original, readable state. Otherwise, it looks like a scrambled piece of text like `bihtueg34509ua`!
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-kms/encryption.png)
> 
> Software developers use encryption to secure user data, transactions, files and more.
> 
> In fact, many apps, websites, and devices use encryption behind the scenes. When you visit a site with "https" in the URL, your connection is encrypted. When you upload files to a cloud storage service like S3 or Google Drive, the service automatically encrypts your data. When you're having a call over Zoom or WhatsApp, the platform is also using encryption to protect your audio and video.

![](https://learn.nextwork.org/projects/static/aws-security-kms/architecture-1.0.png)

  



  
  

**Navigate to KMS**

-   Log in to the AWS Management Console [as your IAM Admin user.](https://signin.aws.amazon.com/oauth?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fhomepage&response_type=code&iam_user=true&account=)
    
-   Search for `Key Management Service`
    
    ![Screenshot 2025-04-28 173827](https://github.com/user-attachments/assets/8f4ed10c-ed82-47e4-845e-3cf532bf6b0c)

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_23.png)

  

> **💡 What is AWS KMS?**  
> **AWS Key Management Service (KMS)** is a secure vault for your encryption keys. You use KMS to create, manage, and use encryption keys that protect the data in your AWS resources.
> 
>   
> 💡 **What are encryption keys?**  
> During the encryption process, the encryption algorithm reads an **encryption key.** This key tells the algorithm exactly how it would transform plain text into the jumbled up format called cipher text. For example, the key could tell the algorithm to swap out certain parts of the data or shuffle the order of data to break up patterns.
> 
> Fun fact: Encryption keys themselves look like cipher text that only the algorithm can understand, like `A7F3E5C4B1D2`. The longer the key, the harder it is to crack the encrypted message!
> 
>   
> 💡 **Why would I need a vault for encryption keys?**  
> A vault for encryption keys, aka a key management system, helps you manage all your encryption keys, like what it encrypts or who has access, in one place. Your keys are safe in a KMS, so you wouldn't have to worry about losing them or someone stealing them. You can also use a KMS to create new keys needed for encryption or decryption.
> 
> On top of the security benefits, a KMS gives you logs on every time a key was used. This helps companies/developers meet **compliance** requirements for data security!



  
  

**Create a Key**

-   In the left navigation pane, select **Customer managed keys**.
    

> **💡 What are AWS managed keys vs. customer managed keys?**  
> AWS offers two main types of keys: AWS managed keys and customer managed keys.
> 
> **AWS managed keys** are automatically created and managed by AWS to encrypt data in the services you use. They're convenient because everything's managed for you, but you have less control over how they work and who has access.
> 
> **Customer managed keys (CMKs),** on the other hand, give you full control. You can adjust how it encrypts data and manage who can access the key.
> 
> For this project, we're using a CMK so you can experience the full power of KMS.

-   Select **Create key**.
    
    ![Screenshot 2025-04-28 174114](https://github.com/user-attachments/assets/f6d78cbc-5dfc-4cfb-adfc-73ca0e83be14)

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_22.png)

  ![Screenshot 2025-04-28 174133](https://github.com/user-attachments/assets/8ab051cb-900d-48c8-a790-db587129b38a)


-   Keep **Symmetric** for the key type.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_24.png)

![Screenshot 2025-04-28 174227](https://github.com/user-attachments/assets/668dd8e5-7eac-4121-bc9e-3bac24b32ad3)
  

> **💡 What is symmetric encryption?**  
> **Symmetric encryption** use a single encryption key to both lock (encrypt) and unlock (decrypt) your data. They are generally faster and more efficient for encrypting large amounts of data, which is why we're using one for our DynamoDB table.
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-kms/symmetric.png)
> 
>   
> 
>   
> **💡 What's the difference between symmetric and asymmetric encryption?**  
> **Asymmetric encryption** works with a pair of keys: a **public** key to encrypt and a **private** key to decrypt. It’s often used when you need to securely share data between multiple parties, like sending information over the internet.
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-kms/asymmetric.png)
> 
>   



-   Keep **Encrypt and decrypt** for the key usage.
    

> **💡 What does key usage mean?**  
> **Key usage** means what your key is designed to do. For example, a key can be used for encrypting data, decrypting data, or generating and verifying digital signatures (a way to prove your data is authentic and hasn’t been altered).
> 
> The key usage you pick fundamentally changes the format and structure of your key, so they're only compatible with the algorithms that match the key usage type.
> 
> **Extra for PROs:** The other option you see is **Generate and verify MAC** (Message Authentication Code), which is a way to use a single key to share data with another party. A MAC is a small piece of data created from a message and a secret key. When you send a message with a MAC, the receiver uses the same secret key to generate a MAC for the received message. If the two MAC messages are identical, it confirms that the message hasn’t been changed by someone else.

-   Select **Next**.
    
-   Give your key an alias: `nextwork-kms-key`. This alias helps you easily identify your key later on.
    
-   For the description, enter:
    



```
KMS key that will encrypt a DynamoDB database. Created for NextWork's Encryption with AWS KMS project.
```

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_25.png)

  ![Screenshot 2025-04-28 174534](https://github.com/user-attachments/assets/05598aaf-42c8-475f-b999-64c42ab23922)

-   Select **Next**.
    
-   Select your own IAM Admin User as a key administrator.

![Screenshot 2025-04-28 174610](https://github.com/user-attachments/assets/cc56bb4a-14d2-43da-acfa-e4cf22e49dd5)
    

> **💡 What is a key administrator?**  
> Key administrators control who can access and use the encryption keys. They have control over the key's lifecycle and its policies, even if they might not use the key themselves.
> 
>   
> **💡 What does a key lifecycle mean?**  
> A key lifecycle are the stages an encryption key goes through, from creation to deletion. Managing this lifecycle means you're setting rules for using, storing, and eventually deleting keys to secure them and the data they protect.

-   Select **Next**.
    
-   Select your own IAM Admin User as a key user.
    

> **💡 What is a key user?**  
> A key user is someone who has permissions to use the key in cryptographic operations, like encrypting and decrypting data. Unlike administrators, key users don't have the permission to manage the key's settings or lifecycle.

-   Scroll to the bottom of the page - notice that **Other AWS accounts** can get access to the key too!
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_26.png)

  
![Screenshot 2025-04-28 174636](https://github.com/user-attachments/assets/994e9ba3-2708-4b78-a91e-ee34cfec7b47)


> **💡 How can other AWS accounts get access?**  
> Other AWS accounts can get access to your KMS keys through cross-account access policies.
> 
> This is useful for scenarios where resources are shared across different AWS accounts. For example, a freelance developer might build an app using their AWS account, while their client stores encrypted data in theirs. The client can share keys that give the app access to the data, without giving the developer access to their account.

-   Select **Next**.
    
-   Note that there's a **Key policy** panel at the bottom of the review page 👀
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_28.png)

![Screenshot 2025-04-28 175415](https://github.com/user-attachments/assets/a88d4894-281b-4cbd-9242-7ce5aad3a508)


  ```
{
	"Id": "key-consolepolicy-3",
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Enable IAM User Permissions",
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::466742534146:root"
			},
			"Action": "kms:*",
			"Resource": "*"
		},
		{
			"Sid": "Allow access for Key Administrators",
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::466742534146:user/DD-IAM-ADMIN"
			},
			"Action": [
				"kms:Create*",
				"kms:Describe*",
				"kms:Enable*",
				"kms:List*",
				"kms:Put*",
				"kms:Update*",
				"kms:Revoke*",
				"kms:Disable*",
				"kms:Get*",
				"kms:Delete*",
				"kms:TagResource",
				"kms:UntagResource",
				"kms:ScheduleKeyDeletion",
				"kms:CancelKeyDeletion",
				"kms:RotateKeyOnDemand"
			],
			"Resource": "*"
		},
		{
			"Sid": "Allow use of the key",
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::466742534146:user/DD-IAM-ADMIN"
			},
			"Action": [
				"kms:Encrypt",
				"kms:Decrypt",
				"kms:ReEncrypt*",
				"kms:GenerateDataKey*",
				"kms:DescribeKey"
			],
			"Resource": "*"
		},
		{
			"Sid": "Allow attachment of persistent resources",
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::466742534146:user/DD-IAM-ADMIN"
			},
			"Action": [
				"kms:CreateGrant",
				"kms:ListGrants",
				"kms:RevokeGrant"
			],
			"Resource": "*",
			"Condition": {
				"Bool": {
					"kms:GrantIsForAWSResource": "true"
				}
			}
		}
	]
}
```

> **💡 Why is there a key policy for my key?**  
> A key policy is a set of rules attached directly to a KMS key. These rules define who can access the key and what they can do with it.
> 
> When you set up your key's administrators and users in the console, AWS was simply converting your clicks to the necessary policy statements in the background.

![Screenshot 2025-04-28 175643](https://github.com/user-attachments/assets/34ae2c09-57a5-43aa-8ec6-240caacbb562)
![Screenshot 2025-04-28 175700](https://github.com/user-attachments/assets/2bc0cd05-2003-4b8b-a826-8a6ad585398b)


-   Select **Finish**.
    
-   Success!
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_29.png)

  ![Screenshot 2025-04-28 175711](https://github.com/user-attachments/assets/f3a01ff7-0608-4582-abbf-64221b9d0d2b)

-----

## 🗄️ Step #2

### Create and Encrypt a DynamoDB Table

  

Now that we have our encryption key, let's create a DynamoDB table and secure it with our newly created key!

This makes sure that all data stored in the table is **encrypted at rest,** adding an extra layer of security.

> **💡 What does 'at rest' mean?**  
> Data **at rest** means any data that's stored somewhere and not currently used or moved. This could be files on your computer's hard drive, information in a database, or backups stored in S3. When data is just sitting there, it’s considered "at rest."
> 
> This is different from data in transit (e.g. an email being sent over the internet) and data in use (e.g. a social media app showing a database of content).
> 
> **Extra for PROs:** Security engineers use a data's type and state (whether it's at rest, in transit, or in use) to apply the best encryption option. AWS KMS is designed to manage long-lived encryption keys for stored data i.e. data at rest. Data in transit relies on short-lived session keys generated by protocols like TLS (Transport Layer Security), and data in use requires real-time access, which is not what a key management system is used for.

**In this step, you're going to:**

-   Create a DynamoDB table.
    
-   Set up your table's encryption with KMS.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/architecture-2.0.png)

  



  
  

**Create a Table**

-   In the AWS Management Console, search for `DynamoDB`
    
-   Select **DynamoDB**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_30.png)

  ![Screenshot 2025-04-28 175813](https://github.com/user-attachments/assets/402bc34e-0799-4c49-9aab-f115531dbbb6)

> **💡 What is DynamoDB?**  
> DynamoDB is one of AWS's database services. DynamoDB stands out as a fast and flexible way to store your data, which makes it a great choice for applications that need quick access to large volumes of data e.g. games.
> 
> If you enjoy using DynamoDB in this project, make sure to check out the [Load Data into DynamoDB](https://link.nextwork.org/projects/aws-databases-dynamodb?utm_source=project-app) project!

-   From your DynamoDB dashboard, select **Create table**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_31.png)

![Screenshot 2025-04-28 175952](https://github.com/user-attachments/assets/142e2f43-b48b-4d85-a800-90baba5257c4)
  

-   Give your table a name, such as `nextwork-kms-table`.
    
-   Define a **Partition key.** For this project, let's use a single string attribute called `id`.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_32.png)

  

> **💡 Extra for PROs: What is a partition key?**  
> A partition key is the heart of how DynamoDB organizes data. Think of it as a label that you can use to group similar items. Under the hood, the partition key is how DynamoDB spreads out your data across different servers for quick access and efficient querying.

-   Under **Table settings**, keep **Default settings**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_33.png)


![Screenshot 2025-04-28 180133](https://github.com/user-attachments/assets/1dff508d-6421-450c-aa33-ec4b6ee7ebd3)  

-   Select **Create table**.

![Screenshot 2025-04-28 180146](https://github.com/user-attachments/assets/802d467e-1b76-474b-8d97-7dd45d8fcf24)

    

  
  

-   Wait for the table status to change to **Active**. This might take a few moments...
    



![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_34.png)

![Screenshot 2025-04-28 180329](https://github.com/user-attachments/assets/6ec83fec-4ea6-48e8-a9b5-d67bc4d4b335)  

**Encrypt Your Table**

-   Select your table **nextwork-kms-table**.
    
-   Select **Additional settings,** which is the very last tab in your settings menu.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_35.png)

  
  ![Screenshot 2025-04-28 180600](https://github.com/user-attachments/assets/89a79001-13c0-4def-babb-cc97a75a4a10)

-   Scroll down to **Encryption**, and select **Manage encryption.**
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_36.png)

![Screenshot 2025-04-28 180619](https://github.com/user-attachments/assets/53110536-371a-4e49-a867-604dbcccd11d)
  
![Screenshot 2025-04-28 180625](https://github.com/user-attachments/assets/8955c3d1-6b91-49e9-9a0c-d80e0700ef23)


-   Choose **Stored in your account, and owned and managed by you**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_37.png)

  ![Screenshot 2025-04-28 180653](https://github.com/user-attachments/assets/3d3452d5-6c67-4ec0-b7dd-93244cfe415b)

> **💡 What are the different encryption options in DynamoDB?**  
> DynamoDB offers a few different encryption options:
> 
> -   **Owned by Amazon DynamoDB:** Amazon DynamoDB fully manages the key, so you have no access or visibility to the key. Great for basic encryption where you don't need any control.
>     
> -   **AWS managed key:** AWS Key Management Service (KMS) manages the key, so it's not a customer managed key like what we created! You can see the key and its usage, but management is done by AWS.
>     
> -   **Stored in your account, and owned and managed by you:** aka a customer managed key (CMK). You create and manage the key in KMS, giving you full control. This is the most secure option and the one we're using in this project.
>     

-   Select the KMS key you created in the previous step (`nextwork-kms-key`) from the dropdown menu.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_38.png)

  
![Screenshot 2025-04-28 180717](https://github.com/user-attachments/assets/12084f27-adeb-4cd3-98f6-9aecee1e9333)


-   Select **Save changes.**

![Screenshot 2025-04-28 180907](https://github.com/user-attachments/assets/dff98778-3a59-4c9d-b790-851c162689cb)
    
-   Scroll back down the **Additional Settings** tab, where you should see an updated **Encryption** panel.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_60.png)

  ![Screenshot 2025-04-28 180946](https://github.com/user-attachments/assets/2c440425-e5a3-4012-ab90-e2242b2e6cdb)
  
------
## ➕ Step #3

### Add Data to Your Table

  

Let's add some data to our newly encrypted table! This will let us test the encryption and see how it protects our data in action.

  
  

**In this step, you're going to:**

-   Add data to your DynamoDB table.
    
-   Verify whether you can see the encrypted data.
    



  
  

**Add Data**

-   Back in your table's settings page, select **Actions.**
    
-   Select **Create item**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_41.png)

  ![Screenshot 2025-04-28 181146](https://github.com/user-attachments/assets/5fc27e02-057d-4568-a4fd-da297c3c540d)

> **💡 What's an item?**  
> In DynamoDB, an item is a single data record in a table.

-   Let's add a simple item! Next to the **id** attribute, enter `1`
    
-   Select **Create item**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_42.png)

  ![Screenshot 2025-04-28 181205](https://github.com/user-attachments/assets/9a8957bc-0b99-4076-a416-f7b210c78486)


-   In the left hand side bar, select **Explore items**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_39.png)

![Screenshot 2025-04-28 181227](https://github.com/user-attachments/assets/7fb9491e-64e6-449e-ab9b-3c928160cb2f)  

-   Refresh your tab.
    
-   Sweet! Confirm that you can see the new item.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_43.png)

![Screenshot 2025-04-28 181308](https://github.com/user-attachments/assets/f30eca47-a32a-46ee-bfd3-d3682320de21)
  

> **💡 Why can I see the item?**  
> Even though the data is encrypted, you as a user have permissions to use the encryption key in KMS.
> 
> DynamoDB is designed to decrypt the data on your behalf. When data is requested by an authorized user (like you) or an authorized application, DynamoDB retrieves the encrypted data, decrypts it with the key, then shows you the decrypted format so you can use it instantly. This security feature is called **transparent data encryption.**
> 
> Transparent data encryption makes sure that your data is secure at rest, yet still accessible to authorized users that have the right permissions.


----
## 🧑‍💼 Step #4

### Create a Test User

  

To truly appreciate the power of KMS encryption, let's create a test IAM user _without_ permissions to use our KMS key.

> **💡 Why create a user without KMS access?**  
> We want to check if a user _without_ access to our KMS key can view the data in DynamoDB. This will confirm if encryption is working as expected, and simulate a real-world scenario where different users have different access levels.

What do you think your test user will see when they access the DynamoDB table?

  
  

**In this step, you're going to:**

-   Create a test user using IAM.
    
-   Grant the user full access to DynamoDB but _not_ to your KMS key.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/architecture-4.0.png)

  


  
  

**Create the IAM User**

-   Open the `IAM` console.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_44.png)

  ![Screenshot 2025-04-28 181510](https://github.com/user-attachments/assets/df7fa2a2-f96b-40c5-b1de-a6f39c25b4e3)


-   Select **Users** in the left navigation pane.
    
-   Select **Create user**.
    
-   Enter a username, such as `nextwork-kms-user`.
    
-   Check **Provide user access to the AWS Management Console - optional**. This will let us log in as the test user and see the KMS key's effect later.
    
-   Uncheck **Users must create a new password at next sign-in - Recommended**, to save ourselves time when we log in as the test user.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_45.png)

  
![Screenshot 2025-04-28 181731](https://github.com/user-attachments/assets/a29d243f-126c-4c32-9078-c2dee8127f89)

-   Select **Next**.
    
-   Select **Attach existing policies directly**.
    
-   Add `AmazonDynamoDBFullAccess` as a permission policy.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_46.png)

  ![Screenshot 2025-04-28 181829](https://github.com/user-attachments/assets/0ee5b425-d446-41ca-84fe-934a720425c4)

-   Select **Next**.

![Screenshot 2025-04-28 181915](https://github.com/user-attachments/assets/01baf647-a331-4507-974d-94f4728073b7)
    
-   Select **Create user**.
    
-   🚨 Stop!
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_48.png)

  ![Screenshot 2025-04-28 182005](https://github.com/user-attachments/assets/37a70912-f561-4271-9a18-55bd28a4b560)

-   Make sure to select **Download .csv file** to save a backup of your user's login details. You won't get this option again once you click out of this page.
    
-   Keep this tab on your screen for the next step.
    

----

## 🕵️ Step #5

### Validate KMS Encryption

  

Now for the moment of truth! Let's test what happens when our test user, who doesn't have KMS key permissions, tries to access the encrypted DynamoDB table.

  
  

**In this step, you're going to:**

-   Log into AWS as the test user.
    
-   Try to view items in the encrypted DynamoDB table.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/architecture-5.0.png)

  


  
  

**Log In**

-   Still in your test user's page, copy the **Console sign-in URL.**
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_50.png)

  

-   Open a **new incognito window** in your browser.
    

> 💡 **Why are we using an incognito window?**  
> We're about to go back and forth between using your test user and your IAM Admin User!
> 
> If you log into your test user in an **incognito** window, you can stay logged in to both users at the same time. No need to log out each time you switch between them.
> 
>   
> 🙋‍♀️ **How do I open a new incognito window?**  
> To open a new incognito window, you can use the shortcut `Ctrl+Shift+N` on Windows/Linux, or `Command+Shift+N` on macOS in most browsers.

-   Head to the console sign-in URL you copied.
    
-   Log in as your new IAM user (**nextwork-kms-user**). You can find your **IAM username** and **password** by copying from the IAM user page, or by opening the .csv file you downloaded.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_51.png)

![Screenshot 2025-04-28 182259](https://github.com/user-attachments/assets/c032ad9c-d077-4bc0-abb2-89193c0aa43e)  

-   Once you've signed in, make sure you're in the same **Region** as your IAM Admin User. You can check and change the region in the top right corner of the AWS console.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_52.png)

  

**Test Access to Encrypted Data**

-   Head to the `DynamoDB` console.

![Screenshot 2025-04-28 182801](https://github.com/user-attachments/assets/36f57c1c-7582-4140-8ea8-7e0313b31e68)
    
-   Head to the **Explore items** tab.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_53.png)

  

-   Select the **nextwork-kms-table** table.
    
-   You should see an error message indicating that access is denied!
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_54.png)

 ![Screenshot 2025-04-28 184811](https://github.com/user-attachments/assets/574e83d2-4f77-4b2a-af84-c03108188d5d) 

> **💡 Why is my access denied?**  
> The new IAM user you're logged in as (**nextwork-kms-user**) does not have the permission to decrypt the data.
> 
> Since the DynamoDB table is encrypted with a specific AWS KMS key, and your user does not have permission to use this key, the system prevents access for data security.
> 
>   
> **💡 What does the troubleshooting in the banner say?**  
> `You don't have permission to kms:Decrypt` means your user isn’t allowed to decrypt the data. This highlights how KMS works - a KMS key can be accessible to many users, but only those with the **right permissions** can use it to do **specific actions** like encryption or decryption.
> 
> In our case, we can give the test user the permission to see that a KMS key is available in your AWS environment, but they still wouldn't have the permissions to decrypt the data it protects.
> 
> This behavior is different from other types of keys, like EC2 instance access keys, which can be used as long as you have access to them.
> 
>   
> **💡 What can an administrator do with that information?**  
> With the access denial information, the key administrator can understand which permissions are missing for your user, and adjust the key's IAM policies! That's what we're doing in the secret mission...


----  
## 💎 Secret Mission

### Give Your Test User Access

  

Welcome to your 🤫 exclusive 🤫 secret mission!

Your mission, should you choose to accept it, is to give your test user access as the administrator.

  
  

💎 **Get ready to:**

-   Modify your KMS key's policy as the administrator.
    
-   Verify that the test user can decrypt data with the key.
    
-   Showcase your secret mission in your **project documentation.**
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/architecture-sm.png)

  

> 💎 **Congratulations** - Secret Mission unlocked!



**Navigate to KMS**

-   Head back to the window with your IAM Admin User logged in.
    
-   Head back to the `Key Management Service` console.
    

![Screenshot 2025-04-28 183723](https://github.com/user-attachments/assets/b38e1231-21dd-4ebe-b81f-231b802605bb)  
  

**Modify the Key Policy**

-   In the KMS dashboard, select **Customer-managed keys** from the left hand sidebar.
    
-   Select **nextwork-kms-key**.

![Screenshot 2025-04-28 183738](https://github.com/user-attachments/assets/5487a3fd-fb7d-4cea-9bb9-57de8ac64402)
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_55.png)

  

-   Scroll down the **Key policy** tab, and select **Add** next to **Key users**.
    
-   Add `nextwork-kms-user` as a test user of your key.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_56.png)

 ![Screenshot 2025-04-28 183841](https://github.com/user-attachments/assets/7913de63-e9e0-4d19-b998-29904c8b2732) 

> **💡 Why do IAM Roles show up as options for key users?**  
> It’s not just IAM users that can use a KMS key—IAM roles can also be key users.
> 
> **Extra for PROs:** You can grant a **role** the permissions to use a key, and multiple users can take on the role when they need to access encrypted data. This is handy in situations where users' responsibilities can change and you want a quick way to allow or deny access for multiple users. It's also helpful when automated services need to run tasks without having their own permanent credentials.

-   Select **Add**.
    
-   Scroll back up to the **Key policy** section and select **Switch to policy view.**
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_57.png)

  

-   Scroll down until you can see the policy section for `Allow use of the key`:
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_58.png)

![Screenshot 2025-04-28 184056](https://github.com/user-attachments/assets/55f3b55b-ccbc-4da2-aaa2-4efdc96bf07b)

  ```
{
	"Version": "2012-10-17",
	"Id": "key-consolepolicy-3",
	"Statement": [
		{
			"Sid": "Enable IAM User Permissions",
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::466742534146:root"
			},
			"Action": "kms:*",
			"Resource": "*"
		},
		{
			"Sid": "Allow access for Key Administrators",
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::466742534146:user/DD-IAM-ADMIN"
			},
			"Action": [
				"kms:Create*",
				"kms:Describe*",
				"kms:Enable*",
				"kms:List*",
				"kms:Put*",
				"kms:Update*",
				"kms:Revoke*",
				"kms:Disable*",
				"kms:Get*",
				"kms:Delete*",
				"kms:TagResource",
				"kms:UntagResource",
				"kms:ScheduleKeyDeletion",
				"kms:CancelKeyDeletion",
				"kms:RotateKeyOnDemand"
			],
			"Resource": "*"
		},
		{
			"Sid": "Allow use of the key",
			"Effect": "Allow",
			"Principal": {
				"AWS": [
					"arn:aws:iam::466742534146:user/nextwork-kms-user",
					"arn:aws:iam::466742534146:user/DD-IAM-ADMIN"
				]
			},
			"Action": [
				"kms:Encrypt",
				"kms:Decrypt",
				"kms:ReEncrypt*",
				"kms:GenerateDataKey*",
				"kms:DescribeKey"
			],
			"Resource": "*"
		},
		{
			"Sid": "Allow attachment of persistent resources",
			"Effect": "Allow",
			"Principal": {
				"AWS": [
					"arn:aws:iam::466742534146:user/nextwork-kms-user",
					"arn:aws:iam::466742534146:user/DD-IAM-ADMIN"
				]
			},
			"Action": [
				"kms:CreateGrant",
				"kms:ListGrants",
				"kms:RevokeGrant"
			],
			"Resource": "*",
			"Condition": {
				"Bool": {
					"kms:GrantIsForAWSResource": "true"
				}
			}
		}
	]
}
```


> **💡 What is this policy telling me?**  
> Notice that on the console side, we simply added your test user as a key user.
> 
> On the policy side, we can see that being a key user means you're allowed to perform the following actions:
> 
> -   `Encrypt:` You can encrypt data using the key.
>     
> -   `Decrypt:` You can decrypt data that was encrypted with the key.
>     
> -   `ReEncrypt*`: You can transfer data from one key to another.
>     
> -   `GenerateDataKey*`: You can create new "mini-keys" (data keys) for locking smaller chunks of data. These are temporary and are used when encrypting lots of data efficiently.
>     
> -   `DescribeKey:` You can get details about the key, like its name or usage policies.
>     



**Verify Access**

-   Return to the incognito window with your test user.

![Screenshot 2025-04-28 184310](https://github.com/user-attachments/assets/bb895dc0-06cf-4ee6-a9a7-68256cacccab)
    
-   Refresh the tab.


    
-   Wooohoo! Your test user can access the database's items now.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_43.png)

  
![Screenshot 2025-04-28 184441](https://github.com/user-attachments/assets/8728619e-fdd7-4b18-a0ba-247249c8501f)


> 💡 **What's the difference between encryption and other ways to control access?**  
>   
> 
> Other access controls, like security groups or permission policies, control access to a **resource** (e.g. a DynamoDB table) or an entire **service** (e.g. DynamoDB).
> 
> However, these don't protect the actual **data** within the resource, like the items inside a DynamoDB table. Once someone has access, they can see all the data they’re allowed to. These controls don’t prevent someone with access from reading or misusing the data.
> 
> If you use KMS encryption, you secure the data within the resource. Even if someone bypasses your access controls (like hacking into a server or intercepting data), they can’t understand the data unless they have the decryption key.
> 
> This adds a layer of security - only users with access permissions **and** decryption keys can view the actual data.

-------

  

## 🗑️ Before You Go

### Delete Your Resources

  

✋ **STOP**

Before diving into the steps for deleting your resources, why not challenge yourself to delete everything in this project on your own?

Keeping track of your resources, and deleting them at the end, is absolutely a skill that will help you reduce waste in your account.

  
  

🛑 **STEPS BELOW:**

-   Head back to the window with your IAM Admin User logged in.
    

  
  

**Delete the DynamoDB Table**

-   In the `DynamoDB` console, select **Tables** from the left hand sidebar.
    
-   Select your `nextwork-kms-table` table.
    
-   Select **Delete**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_11.png)

  

> **💡 What are these warnings about?**  
> 
> ![](https://learn.nextwork.org/projects/static/aws-security-kms/unprocessed_image_12.png)

![Screenshot 2025-04-28 185022](https://github.com/user-attachments/assets/73a04eca-3deb-401c-9d41-36a08890bce6)

> 
>   
> 
> -   **Delete all CloudWatch alarms:** Keep this **checked ✅** Deleting any CloudWatch alarms associated with this table will save you from unnecessary charges.
>     
> -   **Create an on-demand backup:** Keep this **unchecked** ❌ You can create a backup of your table to save for the long term, so you restore your data to its exact state before deleting it. Additional charges apply for on-demand backup and restore, so we won't use this option.
>     

-   Type `confirm` to confirm the deletion, then select **Delete**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_13.png)

  
![Screenshot 2025-04-28 185054](https://github.com/user-attachments/assets/3f9a3f48-4e11-4fcf-9b13-f8a5e4ce82a6)

  
  

**Schedule KMS Key Deletion**

-   In the `KMS` console, select **Customer-managed keys** from the left hand sidebar.
    
-   Select your `nextwork-kms-key` key.
    
-   Select **Key actions**.
    
-   Select **Schedule key deletion**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_14.png)

  ![Screenshot 2025-04-28 185127](https://github.com/user-attachments/assets/0d5c4139-425c-4212-b9a9-3f2aa3e0871c)


-   Under **Waiting period**, update the number of days to `7` to remove the key asap.
    

> **💡 What is a waiting period?**  
> The waiting period in AWS KMS is the time between you scheduling the deletion of a key and the key actually getting deleted. This delay gives you a window to cancel the deletion if it was scheduled by mistake or if you decide you still need the key. AWS requires a minimum waiting period of 7 days, but it can be extended to a maximum of 30 days.
> 
>   
> **💡 Why does a waiting period exist?**  
> Deleting a KMS key is a bit of a big deal - once the key is gone, any data encrypted under that key also becomes unrecoverable unless you have a backup or another way to decrypt it. This could lead to data loss if the deletion was a mistake or if you don't have backups.
> 
> Having a waiting period buys you the time to make sure no essential data is still encrypted under that key. It's also a great time for updating or reconfiguring any apps/systems to use a different key for the same data.

-   Tick the confirmation checkbox.
    
-   Select **Schedule deletion.**
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_61.png)

  
![Screenshot 2025-04-28 185154](https://github.com/user-attachments/assets/17a80416-0884-43b8-a9e1-b3b27659d6d3)

  
  ![Screenshot 2025-04-28 185206](https://github.com/user-attachments/assets/2a6ba9da-4eec-489f-a5d8-151098308964)


**Delete the IAM User**

-   In the `IAM` console, select **Users** from the left hand sidebar.
    
-   Select `nextwork-kms-user`
    
-   Select **Delete**.
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_16.png)

  

-   Enter your user's name `nextwork-kms-user`
    
-   Select **Delete user.**
    

![](https://learn.nextwork.org/projects/static/aws-security-kms/processed_image_17.png)

  ![Screenshot 2025-04-28 185306](https://github.com/user-attachments/assets/7fcd99d9-4019-414c-94b8-abd5724cefdb)

-   In your local computer, delete the **.csv** file containing your user's access details. The file should be called `nextwork-kms-user_credentials.csv` in your Downloads folder.
    

![Screenshot 2025-04-28 185322](https://github.com/user-attachments/assets/eb461db0-25e5-4eb5-a9c1-9f410785b530)


----------



🎉 Mission Accomplished

### That's a wrap!

  

Nice work! You've just built some solid skills in encryption, Amazon KMS and protecting your database.

![](https://learn.nextwork.org/projects/static/aws-security-kms/architecture-complete.png)

  

You've learned how to:

-   🔑 Create and manage encryption keys in KMS.
    
-   🗄️ Encrypt a DynamoDB table using an encryption key.
    
-   ➕ Add data to your encrypted table.
    
-   🧑‍💼 Use a test user to validate your encryption.
    
-   💎 Give your test user encryption access.
----

content owner : **Nextwork**
------