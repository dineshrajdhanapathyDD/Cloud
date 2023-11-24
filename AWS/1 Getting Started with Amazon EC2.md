

#  Getting Started with Amazon EC2



### OBJECTIVES



-   Launch an EC2 instance with termination protection turned on.
-   Monitor your EC2 instance.
-   Modify the security group that your web server is using to allow HTTP access.
-   Connect to your EC2 instance using the AWS Systems Manager Fleet Manager.
-   Manage the state of an EC2 instance.
-   Change your EC2 instance type.
-   Test termination protection.
-   Explore Amazon EC2 limits.

## Task 1: Launching your EC2 instance

In this task, you launch an EC2 instance with termination protection. Termination protection prevents you from accidentally terminating an EC2 instance. You also deploy your instance with a user data script to deploy a simple web server.

3.  In the AWS Management Console on the  **Services**  menu, enter  **EC2**. From the search results, choose  **EC2**.

![1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/32caa939-bfd8-445e-8e69-81654283f981)
    
4.  In the left navigation pane, choose  **EC2 Dashboard**  to ensure that you are on the dashboard page.


![2](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/31c279a8-a49b-48be-af13-a8b640dc19db)
    
5.  In the  **Launch instance**  section, choose the  **Launch instance**  button.

![3](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/dd7bd62d-845d-45a8-a5e8-867d646dfda0)
    

### STEP 1: NAME YOUR EC2 INSTANCE

Using tags, you can categorize your AWS resources in different ways (for example, by purpose, owner, or environment). This categorization is useful when you have many resources of the same type. You can quickly identify a specific resource based on the tags that you have assigned to it. Each tag consists of a key and a value, both of which you define.

When you name your instance, AWS creates a key-value pair. The key for this pair is  **Name**, and the value is the name that you enter for your EC2 instance.

6.  In the  **Name and tags**  pane, in the  **Name**  text box, enter
    
    Web-Server
    
7.  Choose the  **Add additional tags**  link.
8.  From the  **Resource types**  dropdown list, select  **Instances**  and  **Volumes**.

![4 1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/dfc4c0c1-3ba9-428b-8f41-2b9ff06eb1fa)


### STEP 2: CHOOSE AN AMI

An Amazon Machine Image (AMI) provides the information required to launch an instance, which is a virtual server in the cloud. An AMI includes the following:

-   A template for the root volume for the instance (for example, an operating system or an application server with applications)
-   Launch permissions that control which AWS accounts can use the AMI to launch instances
-   A block device mapping that specifies the volumes to attach to the instance when it is launched

The  **Quick Start**  list contains the most commonly used AMIs. You can also create your own AMI or select an AMI from the AWS Marketplace, an online store where you can sell or buy software that runs on AWS.

9.  Locate the  **Application and OS Images (Amazon Machine Image)**  section. It is just below the  **Name and tags**  section.
10.  In the search box, enter
    
    Windows Server 2019 Base
    
    and press Enter.
    
11.  Next to  **Microsoft Windows Server 2019 Base**, choose  **Select**.

![4](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/86f8951b-2bb0-43ca-9dde-23c9a38e72a6)

12.  Choose  **Confirm Changes**.


![5](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/24d6416f-a3c9-42a1-9e76-0a2d42eba69d)

### STEP 3: CHOOSE AN INSTANCE TYPE

Amazon EC2 provides a wide selection of instance types that are optimized to fit different use cases. Instance types comprise varying combinations of CPU, memory, storage, and networking capacity and give you the flexibility to choose the appropriate mix of resources for your applications. Each instance type includes one or more instance sizes so that you can scale your resources to the requirements of your target workload.

In this step, you choose a  **t2.micro**  instance. This instance type has 1 virtual CPU and 1 GiB of memory.

13.  In the  **Instance type**  section, keep the default instance type,  **t2.micro**.

![6](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/3b65654a-c718-46c6-84ee-6b015d2be521)

### STEP 4: CONFIGURE A KEY PAIR

Amazon EC2 uses public key cryptography to encrypt and decrypt login information. To log in to your instance, you must create a key pair, specify the name of the key pair when you launch the instance, and provide the private key when you connect to the instance.

In this lab, you do not connect to your instance using an SSH key, so you do not need to configure a key pair.

14.  In the  **Key pair (login)**  section, from the  **Key pair name -  _required_**  dropdown list, choose  **Proceed without a key pair (not recommended)**.

![6 1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/545704be-cc92-4bae-86bc-d1b9d2f62787)


### STEP 5: CONFIGURE THE NETWORK SETTINGS

You use this pane to configure networking settings.

The virtual private cloud (VPC) indicates which VPC you want to launch the instance into. You can have multiple VPCs, including different ones for development, testing, and production.

15.  In the  **Network settings**  section, choose  **Edit**.
    
16.  From the  **VPC -  _required_**  dropdown list, choose  **Lab VPC**.
    

The Lab VPC was created using an AWS CloudFormation template during the setup process of your lab. This VPC includes two public subnets in two different Availability Zones.

17.  For  **Security group name -  _required_**, choose  **Select existing security group**.
    
18.  From  **Common security groups**, select  **Web Server security group**.



![7](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/b21c06ee-7d10-4ef9-9993-77348697948c)
    

A security group acts as a virtual firewall that controls the traffic for one or more instances. When you launch an instance, you associate one or more security groups with the instance. You add rules to each security group that allow traffic to or from its associated instances. You can modify the rules for a security group at any time; the new rules are automatically applied to all instances that are associated with the security group.

### STEP 6: ADD STORAGE

Amazon EC2 stores data on a network-attached virtual disk called Amazon Elastic Block Store (Amazon EBS).

You launch the EC2 instance using a default 30 GiB disk volume. This is your root volume (also known as a boot volume).

19.  In the  **Configure storage**  section, keep the default storage configuration.

### STEP 7: CONFIGURE ADVANCED DETAILS

20.  Expand the  **Advanced details**  section.
    
21.  For  **IAM instance profile**, choose the role that has  **LabInstanceProfile**  in the name.
    

When you no longer require an EC2 instance, you can terminate it, which means that the instance stops, and Amazon EC2 releases the instance’s resources. You cannot restart a terminated instance. If you want to prevent your users from accidentally terminating the instance, you can turn on (enable) termination protection for the instance, which prevents users from terminating instances.

22.  From the  **Termination protection**  dropdown list, choose  **Enable**.


![8](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/312b6bf9-d97c-4b6b-a9ff-7a379ba5a870)

When you launch an instance in Amazon EC2, you have the option of passing user data to the instance. These commands can be used to perform common automated configuration tasks and even run scripts after the instance starts.

23.  Copy the following commands, and paste them into the  **User data**  text box.

![9](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/ddefb738-e025-4ba9-8907-d4bd4a3658c2)
    
    


    ```
    <powershell>
    # Installing web server
    Install-WindowsFeature -name Web-Server -IncludeManagementTools
    # Getting website code
    wget https://us-east-1-tcprod.s3.amazonaws.com/courses/CUR-TF-100-EDCOMP/v1.0.4.prod-ef70397c/01-lab-ec2/scripts/code.zip -outfile "C:\Users\Administrator\Downloads\code.zip"
    # Unzipping website code
    Add-Type -AssemblyName System.IO.Compression.FileSystem
    function Unzip
    {
        param([string]$zipfile, [string]$outpath)
        [System.IO.Compression.ZipFile]::ExtractToDirectory($zipfile, $outpath)
    }
    Unzip "C:\Users\Administrator\Downloads\code.zip" "C:\inetpub\"
    # Setting Administrator password
    $Secure_String_Pwd = ConvertTo-SecureString "P@ssW0rD!" -AsPlainText -Force
    $UserAccount = Get-LocalUser -Name "Administrator"
    $UserAccount | Set-LocalUser -Password $Secure_String_Pwd
    </powershell>
    
    ```
    
  
    
  The script does the following:
  
-   Installs a Microsoft Internet Information Services (IIS) web server
-   Creates a simple web site
-   Sets the password for the Administrator user

### STEP 8: LAUNCH AN EC2 INSTANCE

Now that you have configured your EC2 instance settings, it is time to launch your instance.

24.  In the  **Summary**  section, choose  **Launch instance**.

![9](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/ddefb738-e025-4ba9-8907-d4bd4a3658c2)


A message indicates that you have successfully initiated the launch of your instance.

![10](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f52d56ea-6791-4130-9dcf-adf133aff3f0)


25.  Choose  **View all instances**

![11](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/d1981dbd-7269-4a56-8ebc-c07f61c10105)

The instance appears in a  **Pending**  state, which means that it is being launched. It then changes to  **Running**, which indicates that the instance has started booting. There will be a short time before you can access the instance.

The instance receives a public Domain Name System (DNS) name that you can use to contact the instance from the Internet.

26.  Next to your  **Web-Server**, select the  check box. The  **Details**  tab displays detailed information about your instance.

To view more information in the  **Details**  tab, drag the window divider upward.

Review the information displayed in the  **Details, Security**  and  **Networking**  tabs.

27.  Wait for your instance to display the following:

**Note:**  Refresh if needed.

-   **Instance State:**  Running
-   **Status Checks:**  2/2 checks passed

![12](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/83b890b0-dc7f-40d1-ab46-a6755f258adf)

----------

## Task 2: Monitor your instance

Monitoring is an important part of maintaining the reliability, availability, and performance of your EC2 instances and your AWS solutions.

28.  Choose the  **Status checks**  tab.

With instance status monitoring, you can quickly determine whether Amazon EC2 has detected any problems that might prevent your instances from running applications. Amazon EC2 performs automated checks on every running EC2 instance to identify hardware and software issues.

Notice that both the  **System reachability**  and  **Instance reachability**  checks have passed.


![13](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/11876b5d-f422-49d5-b897-741c3ed7fa1f)


29.  Choose the  **Monitoring**  tab.

This tab displays Amazon CloudWatch metrics for your instance. Currently, there are not many metrics to display because the instance was recently launched.

You can choose a graph to see an expanded view.

Amazon EC2 sends metrics to Amazon CloudWatch for your EC2 instances. Basic (5 minute) monitoring is turned on by default and is free. You can turn on detailed (1 minute) monitoring. With detailed monitoring, you will be charged per metric that you send to CloudWatch.

30.  At the top of the page, choose the  **Actions**  dropdown menu. Select  **Monitor and troubleshoot**  **Get system log**.

![14](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/4022e362-0a2f-4fe4-afdd-a425e247f326)

The system log displays the console output of the instance, which is a valuable tool for problem diagnosis. It is especially useful for troubleshooting service configuration issues that could cause an instance to terminate or become unreachable. If you do not see a system log, wait a few minutes and then try again.

31.  Scroll through the log and review the messages in the output.
    
32.  To return to the Amazon EC2 dashboard, choose  **Cancel**.
    
33.  With your  **Web-Server**  selected, choose the  **Actions**  dropdown menu, and select  **Monitor and troubleshoot**  **Get instance screenshot**.
    
This option shows you what your EC2 instance console would look like if a screen were attached to it. Because this is a Windows instance, the screenshot shows a locked log-in screen.

![15](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/86645dbb-4e01-4452-830b-f60fcf35c7ed)

If you are unable to reach your instance via SSH or RDP, you can capture a screenshot of your instance and view it as an image. This option provides visibility about the status of the instance for quicker troubleshooting.

34.  At the bottom of the page, choose  **Cancel**.

----------

## Task 3: Updating your security group and accessing the web server

When you launched the EC2 instance, you provided a script that installed a web server and created a simple web page. In this task, you access content from the web server.

35.  Select the check box next to the Amazon EC2  **Web-Server**  that you created, and then choose the  **Details**  tab.
    
36.  Copy the  **Public IPv4 address**  of your instance to your clipboard.
    
37.  In your web browser, open a new tab, paste the IP address you just copied, and then press Enter.
    

![16](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/4866e53a-ceba-4b51-adfc-fd8fd0f872ea)

**Question:**  Are you able to access your web server? Why not?

You are not currently able to access your web server because the security group is not permitting inbound traffic on port 80, which is used for HTTP web requests. This step is a demonstration of how to use a security group as a firewall to restrict the network traffic that is allowed in and out of an instance.

To correct this issue, you now update the security group to permit web traffic on port 80.

38.  Keep the browser tab open, but return to the  **EC2 Management Console**  tab.
    
39.  In the left navigation pane, choose  **Security Groups**.
    
40.  Next to  **Web Server security group**, select the  check box.
    
41.  Choose the  **Inbound rules**  tab.
    

The security group currently has no rules.

42.  Choose  **Edit inbound rules**, and then choose  **Add rule**, and configure the following options:

-   **Type:**  Choose  **HTTP**.
-   **Source:**  Choose  **Anywhere-IPv4**.

![17](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/0ddc7bdf-3b7c-4110-bf54-f028fa67bfe7)

**Note:**  Notice the  _“Rules with source of 0.0.0.0/0 allow all IP addresses to access your instance. We recommend setting security group rules to allow access from known IP addresses only.”_  While this is true and common best practice, this lab allows access from any IP address (Anywhere) to simplify both the security group configuration and testing of the website running on your EC2 instance.

In this lab, you can only add a new Ingress rule. You cannot change it a rule it has been created. Double check the configuration before choosing  **Save rules**.

43.  Choose  **Save rules**


![18](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/c5ce657e-ffe4-4425-8391-ab7e63fb642b)

    
44.  Return to the web server browser tab with the public IPv4 address that you previously opened, and choose  to refresh the page.
    

You should now find a web website with the message  **Welcome Students!**

**Note:**  If the web site is not loading, verify that the URL in the address bar begins with

http://

![20](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/716f4900-f8f9-422e-b276-fb3a6f7783bc)

and not

https://

.![19](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/41ae98d2-e672-4266-9f73-72d2fe9c0197)

----------

## Task 4: Connecting to your instance using AWS Systems Manager Fleet Manager

With the Fleet Manager capability of AWS Systems Manager, you can remotely manage and configure your managed nodes. A managed node is any machine configured for Systems Manager.

When you started this lab, your AWS user was automatically given permissions to use Systems Manager. In addition, the AWS Identity and Access Management (IAM) policy that you selected when configuring your EC2 instance turned on Systems Manager for your Web-Server instance.

One convenient feature of Fleet Manager is the ability to connect to your EC2 instance using a browser. In this task, you connect to your Windows desktop using Fleet Manager.

45.  In the AWS Management Console on the  **Services**  menu, search for and select  **Systems Manager**.


![21](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/c4da461e-ebf6-4838-add5-0c7a4254dfc0)

    
46.  In the left nagivation pane, select  **Fleet Manager.**


![22](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e3d0e0a5-0555-4735-bbef-1577627cffb8)
    
47.  Under  **Managed nodes**, select  your  **Web-Server**  EC2 instance.

![25](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/f498a956-30a1-4b65-887e-d93be6b4128e)
    
48.  From the  **Node actions**  dropdown list, choose  **Connect with Remote Desktop**.



![23](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/b3a9eb1d-a842-4123-b693-9dcb1619bc57)
    

A new tab opens.

49.  Enter the following values:

-   **Username:**   `Administrator`
    
-   **Password:** `P@ssW0rD!`
    

50.  Choose  **Connect**.

After several seconds, the pane displays the Windows desktop. You can navigate this desktop just like you would on a local computer. As you learned earlier, with Amazon EC2, you can quickly access compute resources. Instead of buying physical hardware and configuring an operating system, all you have to do is launch an EC2 instance, and all of that work is done for you automatically in minutes.

51.  To disconnect from your  **Web-Server**  instance, choose  **Action**  and then choose  **End session**.
    
52.  In the pop-up window, choose  **End session**  again .
    
![24](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/6ffcac57-f735-49dc-927f-9c66b7c5a9fe)

----------

## Task 5: Resizing your instance

As your needs change, you might find that your instance is overutilized (too small) or underutilized (too large). If so, you can change the instance type. For example, if a t2.micro instance is too small for its workload, you can change it to an m5.medium instance.

### STOP YOUR INSTANCE

Before you can resize an instance, you must stop it.

When you stop an instance, it is shut down. There is no charge for a stopped EC2 instance, but the storage charge for attached EBS volumes remains.

53.  From the AWS Management Console on the  **Services**  menu, choose  **EC2**
    
54.  On the  **EC2 Management Console**, in the left navigation pane, choose  **Instances**.
    
55.  Select the check box next to your  **Web-Server**  instance. At the top of the page, choose the  **Instance state**  dropdown menu, and choose  **Stop instance**.
    
56.  In the  **Stop instance?**  pop-up window, choose  **Stop**.


![26](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/065220e2-ee8b-46a7-9ec9-e0ad93132466)
    

Your instance performs a normal shutdown and then stops running.

57.  Wait for the  **Instance state**  to display  **Stopped**.


![27](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/73d31c49-5910-47c9-bbc5-15d181ec6d6b)

### CHANGE THE INSTANCE TYPE

58.  Select the check box next to your  **Web-Server**. From the  **Actions**  dropdown menu, select  **Instance settings**  **Change instance type**, and then configure the following option:

-   **Instance type:**  Select  **t2.nano**.

![28](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/8184c80d-5702-45cd-b20e-d8a83b352691)

59.  Choose  **Apply**

**Note**: You are restricted from using other instance types in this lab.

### START THE RESIZED INSTANCE

When the instance is started again, it is a t2.nano instance. You now start the instance again, which has less memory but more disk space.

60.  In left navigation pane, choose  **Instances**. Next to your  **Web-Server**, select the  check box.
    
61.  From the  **Instance state**  dropdown menu, choose  **Start instance**.


![29](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/6166a767-3635-4a30-8f81-309089ab7e42)
    

Once the instance is restarted, the  **Instance state**  displays  **Running**.


![30](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/588d14d7-575f-43b1-8855-0aec49b37a73)


----------

## Task 6: Testing termination protection

You can delete your instance when you no longer need it. This is referred to as terminating your instance. You cannot connect to or restart an instance after it has been terminated.

In this task, you learn how to use termination protection.

62.  Select the check box next to your  **Web-Server**  instance. From the  **Instance state**  dropdown menu, choose  **Terminate instance**.

![31](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e847873d-14f8-4872-a9cf-87c6556ca0ec)
    
63.  Notice the message next to the  **Terminate instance**  option:  _Termination protection is enabled for one or more of the selected instances._


![32](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/d2de7209-3851-496a-ba83-07a9ff98925e)
    

This is a safeguard to prevent the accidental termination of an instance. If you really want to terminate the instance, you need to turn off termination protection.



You can easily enable and disable termination protection from the  **Actions**  dropdown menu.

64.  From the  **Actions**  dropdown menu, choose  **Instance settings**, and then choose  **Change termination protection**.

![33](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/be5cf611-b8fb-4000-bff7-465b7c1abc03)



    
65.  Clear the check box for  **Enable**.



![35](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/8ae5d21c-9ee0-4434-b7af-e53f9449baeb)

    
66.  Choose  **Save**.


![34](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/1f2aa3ea-ab90-470e-952d-8165c536f39f)
    
67.  Now, try to terminate the instance again.
    

The instance state will now successfully be terminated.

----------

## Task 7: Exploring EC2 limits

Amazon EC2 provides different resources that you can use. These resources include images, instances, volumes, and snapshots. When you create an AWS account, there are default limits on these resources on a per-Region basis.

68.  In the left navigation pane, choose  **Limits**.

**Note:**  There is a limit on the number of instances that you can launch in this Region. When launching an instance, the request must not cause your usage to exceed the current instance limit in that Region.

You can request an increase for many of these limits.

----------

## Summary

 EC2 instance and learned to manage instance properties such as the instance type. You modified security group settings to make the website reachable, and you learned how to use termination protection to prevent instance deletion. You learned how to stop, start, and terminate an EC2 instance. Finally, you learned how to find the EC2 limits for your AWS account. Great job!




**credits: AWS Educate** 