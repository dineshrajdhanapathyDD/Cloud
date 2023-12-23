
# Getting Started with Security

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to Amazon Web Services (AWS) resources. IAM enables you to securely manage access to AWS offerings and resources. Using IAM, you can create and manage AWS users and groups and use permissions to allow and deny their access to AWS resources. IAM is a feature of your AWS account that’s offered at no additional charge. You will be charged only for use of other AWS services by your users.

In this Module, you acquire the knowledge that you need to start using AWS Identity and Access Management (IAM). You learn about the key concepts and features of IAM. You learn how to write security policies, set up users, groups, and roles, apply permissions, and review credentials. You also learn about additional AWS security services.








# Introduction to IAM



you will explore users, groups, and policies in the AWS Identity and Access Management (IAM) service.

### Objectives

you will know how to:

-   Exploring pre-created **IAM Users and Groups**
-   Inspecting **IAM policies** as applied to the pre-created groups
-   Following a **real-world scenario**, adding users to groups with specific capabilities enabled
-   Locating and using the **IAM sign-in URL**
-   **Experimenting** with the effects of policies on service access



## Task 1: Explore the users and groups

In this task, you will explore the users and groups that have already been created for you in IAM.

1.  Open a AWS Management Console

![1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/3fa0c4f5-cf94-4e44-8ba5-40c1651c473c)

2.  First, note the Region that you are in; for example, **N. Virginia**. The Region is displayed in the upper-right corner of the console page.
    
    You might need this information later in the lab.
    
3.  Choose the **Services** menu, locate the **Security, Identity, & Compliance** services, and choose **IAM**.

![2](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/0c5f35cf-bbdc-45f7-8f82-ca301486da5e)
    
4.  In the navigation pane on the left, choose **Users**.
    
    The following IAM users have been created for you:
    
    -   user-1
    -   user-2
    -   user-3

![3](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e0e37bbd-f5fd-4532-a41a-ad723f705e6f)



5.  Choose the name of **user-1**.
    
   -   This brings you to a summary page for user-1. The **Permissions** tab will be displayed.

![4](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/2bf7a4cf-c801-4153-97d6-4a231b39c7f3)

   -   Notice that user-1 does not have any permissions.
    
6.  Choose the **Groups** tab.

![5](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/63510a66-fb55-4aa3-b708-8b15cd2790c9)
    
  -  Notice that user-1 also is not a member of any groups.
    
7.  Choose the **Security credentials** tab.

![6](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/11b6e6af-5fdf-4fe7-af22-f21b78ca548a) 
    
  -   Notice that user-1 is assigned a **Console password**. This allows the user to access the AWS Management Console.
    
8.  In the navigation pane on the left, choose **User groups**.
    
  -   The following groups have already been created for you:
    
    -   EC2-Admin
    -   EC2-Support
    -   S3-Support

![7](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/11a273b0-4252-47b1-84e6-04d9c8e9b508)

9.  Choose the name of the **EC2-Support** group.
    
   - This brings you to the summary page for the **EC2-Support** group.
    
10.  Choose the **Permissions** tab.

![8](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/0027e7b9-939b-4b6e-a1a8-455b79c8bb5c)

    
  -  This group has a managed policy called **AmazonEC2ReadOnlyAccess** associated with it. Managed policies are prebuilt policies (built either by AWS or by your administrators) that can be attached to IAM users and groups. When the policy is updated, the changes to the policy are immediately applied against all users and groups that are attached to the policy.


![9](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/4d000cff-d1b4-4f97-a0dc-cc7537288f36)
    
11.  Under **Policy Name**, choose the link for the **AmazonEC2ReadOnlyAccess** policy.
    
12.  Choose the **{} JSON** tab.

![10](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/4f962329-179a-4591-8d2b-26036aa19563)

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ec2:Describe*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "elasticloadbalancing:Describe*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "cloudwatch:ListMetrics",
                "cloudwatch:GetMetricStatistics",
                "cloudwatch:Describe*"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "autoscaling:Describe*",
            "Resource": "*"
        }
    ]
}
```
  
   -   A policy defines what actions are allowed or denied for specific AWS resources. This policy is granting permission to _List_ and _Describe_ (view) information about Amazon Elastic Compute Cloud (Amazon EC2), Elastic Load Balancing, Amazon CloudWatch, and Amazon EC2 Auto Scaling. This ability to view resources, but not modify them, is ideal for assigning to a support role.
        
    -   Statements in an IAM policy have the following basic structure:
        
        -   **Effect** says whether to _Allow_ or _Deny_ the permissions.
        -   **Action** specifies the API calls that can be made against an AWS service (for example, _cloudwatch:ListMetrics_).
        -   **Resource** defines the scope of entities covered by the policy rule (for example, a specific Amazon Simple Storage Service [Amazon S3] bucket or Amazon EC2 instance; an asterisk [ * ] means _any resource_).

13.  In the navigation pane on the left, choose **User groups**.
    
14.  Choose the name of the **S3-Support** group.
    
15.  Choose the **Permissions** tab.

![11](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/2b64b8b7-8bfa-4b78-8d1d-a4e75169fd69)
    
-    The S3-Support group has the **AmazonS3ReadOnlyAccess** policy attached.
    
16.  Under **Policy Name**, choose the link for the **AmazonS3ReadOnlyAccess** policy.
    
17.  Choose the **{} JSON** tab.


![12](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/02631a52-48e1-4371-9c71-13ce878415b6)
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:Get*",
                "s3:List*",
                "s3:Describe*",
                "s3-object-lambda:Get*",
                "s3-object-lambda:List*"
            ],
            "Resource": "*"
        }
    ]
}
```
    
 -   This policy has permissions to _Get_ and _List_ for _all_ resources in Amazon S3.
    
18.  In the navigation pane on the left, choose **User groups**.
    
19.  Choose the name of the **EC2-Admin** group.
    
20.  Choose the **Permissions** tab.

![13](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/46295e79-5a0b-4c74-a876-83e786002271)
    
   -  This group is different from the other two. Instead of a managed policy, the group has an _inline policy_, which is a policy assigned to just one user or group. Inline policies are typically used to apply permissions for specific situations.
    
21.  Under **Policy Name**, choose the name of the **EC2-Admin-Policy** policy.
    
22.  Choose the **JSON** tab.

![14](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/258cc831-9c90-4831-a0be-9fa7f0fee129)
```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Condition": {
				"ForAllValues:StringLikeIfExists": {
					"ec2:InstanceType": [
						"*.nano",
						"*.micro"
					]
				}
			},
			"Action": [
				"ec2:Describe*",
				"ec2:StartInstances",
				"ec2:StopInstances"
			],
			"Resource": [
				"*"
			],
			"Effect": "Allow"
		}
	]
}
```

    
  -  This policy grants permission to _Describe_ information about Amazon EC2 instances, and also the ability to _Start_ and _Stop_ instances.
    
23.  At the bottom of the screen, choose **Cancel** to close the policy.
    

## Business scenario

For the remainder of this Module, you will work with these users and groups to enable permissions that support the following business scenario.

Your company is growing its use of AWS services, and is using many Amazon EC2 instances and Amazon S3 buckets. You want to give access to new staff depending upon their job function, as indicated in the following table:

|        User        |In Group                         |Permissions                        |
|----------------|-------------------------------|-----------------------------|
user-1 | S3-Support | Read-only access to Amazon S3
user-2 |  EC2-Support | Read-only access to Amazon EC2
user-3 | EC2-Admin |View, Start, and Stop Amazon EC2 instances

## Task 2: Add users to groups

You have recently hired _user-1_ into a role where they will provide support for Amazon S3. You will add them to the _S3-Support_ group so that they inherit the necessary permissions via the attached _AmazonS3ReadOnlyAccess_ policy.

Ignore any "not authorized" errors that appear during this task. They are caused by your lab account having limited permissions and will not impact your ability to complete the lab.

### Add user-1 to the S3-Support group

24.  In the left navigation pane, choose **User groups**.

![15](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/46d9bb79-4091-43be-8c5e-daff8d2f9b3d)
    
25.  Choose the name of the **S3-Support** group.


![16](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/61049ea6-46f2-4960-9747-6a8fd837077c)
    
26.  On the **Users** tab, choose **Add users**.
    
27.  Select **user-1**, and choose **Add users**.
![17](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/5e63efb8-0b37-480a-83a2-6e9b2841b45f)

    
   - On the **Users** tab, notice that _user-1_ has been added to the group.

![18](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/7d9615dc-4697-4ea9-bc8d-735c8d5b734c)

### Add user-2 to the EC2-Support group

You have hired _user-2_ into a role where they will provide support for Amazon EC2. You will add them to the _EC2-Support_ group so that they inherit the necessary permissions via the attached _AmazonEC2ReadOnlyAccess_ policy.

![19](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/7eda568c-6038-4acb-be81-3de70eca7a84)

28.  Use what you learned from the previous steps to add _user-2_ to the _EC2-Support_ group. 

![20](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/36ea5f5d-521a-4702-93c4-443993ae21ba)
    
  -  _user-2_ should now be part of the _EC2-Support_ group.

![21](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a0fde04a-a029-416d-be5e-bc427be01453)
    

### Add user-3 to the EC2-Admin group

You have hired _user-3_ as your Amazon EC2 administrator to manage your EC2 instances. You will add them to the _EC2-Admin_ group so that they inherit the necessary permissions via the attached _EC2-Admin-Policy_.

29.  Use what you learned from the previous steps to add _user-3_ to the _EC2-Admin_ group.
    
  -  _user-3_ should now be part of the _EC2-Admin_ group.

![22](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/0d1ca7b0-5af9-4777-895b-eb14fc22a01a)

    
30.  In the navigation pane on the left, choose **User groups**.
    
 -  Each group should have a **1** in the **Users** column. This indicates the number of users in each group.

![23](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a57f5db0-8f4c-4608-bf52-09abe71eb25c)
    
   - If you do not have a **1** for the **Users** column for a group, revisit the previous steps to ensure that each user is assigned to a group, as shown in the table in the **Business scenario** section.

![24](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/d92e411f-97cd-4cff-89f6-06fb308e76c4)
    

![25](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/2f5827d2-2767-4ec5-ad0a-18987ec2e812)

## Task 3: Sign in and test users

In this task, you will test the permissions of each IAM user in the console.

### Get the console sign-in URL

31.  In the navigation pane on the left, choose **Dashboard**.

![26](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a2a70f6c-6ad9-4c67-bd75-949074071eea)
    
    Notice: the **Sign-in URL for IAM users in this account** section at the top of the page. The sign-in URL looks similar to the following: **https://123456789012.signin.aws.amazon.com/console**
    
   -  This link can be used to sign in to the AWS account that you are currently using.
    
32.  Copy the sign-in link to a text editor.
    

### Test user-1 permissions

33.  Open a private or incognito window in your browser.
    
34.  Paste the sign-in link into the private browser, and press ENTER.
    
    You will now sign-in as _user-1_, who has been hired as your Amazon S3 storage support staff.
    
35.  Sign in with the following credentials:
    
    -   **IAM user name:**  `user-1`
    -   **Password:**  `Lab-Password1`

![27 1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/217bd30f-1370-4df6-b387-751226adb610)

36.  Choose the **Services** menu, and choose **S3**.


![27](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/efe9dedf-96ad-4152-b482-eacea7ceee36)

    
37.  Choose the name of one of your buckets, and browse the contents.

![28](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/ebf81aa7-b2e7-4a36-bbb4-f17970efff17)
    
  -   Because this user is part of the _S3-Support_ group in IAM, they have permissions to view a list of Amazon S3 buckets and their contents.
    
  -   Now, test whether the user has access to Amazon EC2.
    
38.  Choose the **Services** menu, and choose **EC2**.

![29](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/0542f117-1f59-4b71-95a1-3faf2c3c72b0)
    
39.  In the left navigation pane, choose **Instances**.

![30](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/2a970a6c-1fd7-4bd3-9eab-b0337c3a954e)
    
   - You cannot see any instances. Instead, an error message says _you are not authorized to perform this operation_. This user has not been assigned any permissions to use Amazon EC2.


![31](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/ac00b714-cac1-4ded-a51f-b7d6d655f9c4)
    
  -  You will now sign in as _user-2_, who has been hired as your Amazon EC2 support person.
    
40.  First, sign out _user-1_ from the console:
    
   -   In the upper-right corner of the page, choose **user-1**.
    -   Choose **Sign Out**.

### Test user-2 permissions

41.  Paste the sign-in link into the private browser again, and press ENTER.
    
42.  Sign in with the following credentials:
    
    -   **IAM user name:**  `user-2`
    -   **Password:**  `Lab-Password2`

![32](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/69ab7fa6-c45f-4950-9608-5b01f83db70e)

43.  Choose the **Services** menu, and choose **EC2**.
    
44.  In the navigation pane on the left, choose **Instances**.

![33](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/398cddeb-7a58-4f1c-86b4-584a96afe17e)
    
   -   You are now able to see an EC2 instance. However, you cannot make any changes to Amazon EC2 resources because you have read-only permissions.
    -   If you cannot see an EC2 instance, then your Region might be incorrect. In the upper-right corner of the page, choose the Region name, and then choose the Region that you were in at the beginning of the lab (for example, **N. Virginia**).


![34](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/5e5b550a-4770-4eae-9c3d-f8165ac98a6f)
    
45.  Select the EC2 instance.

![36](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/86148b93-28a9-4e0b-94d8-95eab70bd9ab)

46.  Choose the **Instance state** menu, and then choose **Stop instance**.
    
49.  To confirm that you want to stop the instance, choose **Stop**.
    
   -  An error message appears and says that _You are not authorized to perform this operation_. This demonstrates that the policy only allows you to view information without making changes.

![37](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/2cf8ecb7-6596-4274-a2a6-cbdb4553a517)
    
   Next, check if _user-2_ can access Amazon S3.
    
48.  Choose the **Services** menu, and choose **S3**.
    
 -    An message says _No buckets_ because _user-2_ does not have permissions to use Amazon S3.

![38](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/c0050a68-0b7a-426b-8b06-e6cad3b08674)
    
   You will now sign-in as _user-3_, who has been hired as your Amazon EC2 administrator.
   
49.  First, sign out _user-2_ from the console:
   -   In the upper-right corner of the page, choose **user-2**.
   -   Choose **Sign Out**.

### Test user-3 permissions

50.  Paste the sign-in link into the private browser again, and press ENTER.
    
51.  Sign in with the following credentials:
    
   -   **IAM user name:**  `user-3`
    -   **Password:**  `Lab-Password3`
    - 
![39](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/47ad7d92-ff64-4cdf-8a68-9f6af4691594)

52.  Choose the **Services** menu, and choose **EC2**.
    
53.  In the navigation pane on the left, choose **Instances**.
    
    -   An EC2 instance is listed. As an Amazon EC2 Administrator, this user should have permissions to _Stop_ the EC2 instance.
    -   If you cannot see an EC2 instance, then your Region might be incorrect. In the upper-right corner of the page, choose the Region name, and then choose the Region that you were in at the beginning of the lab (for example, **N. Virginia**).


![40](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a1aaefca-f75e-4650-8b7b-463153fe403c)

54.  Select the EC2 instance.
    
55.  Choose the **Instance state** menu, and then choose **Stop instance**.
    
56.  To confirm that you want to stop the instance, choose **Stop**.

![41](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/7197c81e-ccca-43ab-9d57-72172225c970)

    
   This time, the action is successful because _user-3_ has permissions to stop EC2 instances. The **Instance state** changes to _Stopping_ and starts to shut down.


![42](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/23654e0d-fa05-4fbf-9a45-9a5ce830b039)

    
57.  Close your private browser window.
    

----------

## Keytakeaway


By the end of this module, you will be able to do the following:

-   Describe security fundamental concepts.
-   Explain AWS IAM features, benefits, and use cases.
-   Discuss how to create and configure IAM user, groups, and roles.
-   Discuss IAM policies.
-   Discuss how to setup multi-factor authentication (MFA).
-   Describe how to set up password policies.
-   Identify other AWS security services.

**Credits : AWS Educate**