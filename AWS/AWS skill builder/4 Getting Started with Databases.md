


# Getting Started with Databases

The business world is constantly changing and evolving. By accurately recording, updating, and tracking data efficiently and on a regular basis, companies can use the immense potential from the insights that they obtain from their data. Database management systems are the crucial link for managing this data. Like other cloud services, cloud databases offer significant cost advantages over traditional database strategies.

In this module, you learn about database fundamentals and Amazon Relational Database Service (Amazon RDS). Amazon RDS is a managed web service that helps customers create and manage highly scalable and secure relational databases in the AWS Cloud. Customers aren’t responsible for hardware provisioning, database setup, software patching, and backups. AWS manages common database administrative tasks.

Amazon RDS supports most relational database engines, including commercial (such as Oracle and Microsoft SQL Server [MSSQL]), open source (MySQL, PostgreSQL, and MariaDB), and Amazon Aurora. With Amazon RDS, you store and transmit data securely.

In this module, you acquire the knowledge that you need to start using Amazon RDS. You learn about the key elements of Amazon RDS and explore how to configure them. You also learn the basic elements of high availability, backups, and security to set up a database that suits the needs of your workload.

# Creating an Amazon RDS Database

Traditionally, creating a database can be a complex process that requires either a database administrator or a systems administrator. In the cloud, you can reduce the number of steps that you take during this process by using Amazon Relational Database Service (Amazon RDS).  you learn how to use Amazon RDS to provision a MySQL database and perform a few basic administrative actions.

### OBJECTIVES

-   Launch a MySQL database using Amazon RDS Service.
-   Configure a web application to connect to the MySQL RDS database instance.
-   Perform operations (Stop, Start, Reboot) on the database instance.
-   Perform basic database monitoring.

1. your architecture will look like the following example:

![Final Architecture](https://us-west-2-tcprod.s3.us-west-2.amazonaws.com/courses/CUR-TF-100-EDDBAS/v1.0.3.prod-774844da/1-lab-rds/instructions/en_us/images/rds-guided-lab-arch.png)





2.  To open the AWS account, choose  Open Console.

You are automatically signed in to the AWS Management Console in a new web browser tab.


![1](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/51dcc7eb-38bc-4e3c-9725-b115f2c098f9)


----------

## Task 1: Creating an Amazon RDS database

In this task, you create a MySQL database in your virtual private cloud (VPC). MySQL is a popular open-source relational database management system (RDBMS), so there are no software licensing fees.

3.  On the  **Services** menu, choose  **RDS**.

![2](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/95942f28-f4e5-498d-830a-e042267fcc45)
    
4.  Choose  **Create database**

![3](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/706ae0c4-af1c-4632-81e2-250a9826462f)
    

-  you will keep the  **Choose a database creation method**  as  **Standard create**  to understand the full set of features available.


![5](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/5a86c094-02cf-4d9f-9571-6d5ce277bb48)


5.  Under  **Engine options**, select  **MySQL**.

-   For Version, keep MySQL 8.0.28.

In the options, you might notice Amazon Aurora. Aurora is a global-scale relational database service built for the cloud with full MySQL and PostgreSQL compatibility. If your company uses large-scale MySQL or PostgreSQL databases, Aurora can provide enhanced performance.

![6](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/b8a34be4-7c01-4325-ac89-c222c6dcdf1a)


6.  In the  **Templates**  section, select  **Dev/Test**.

You can now select a database configuration, including software version, instance class, storage, and login settings. The  _Multi-AZ deployment_  option automatically creates a replica of the database in a second Availability Zone for high availability.

7.  In the  **Availability and durability**  section, choose  **Single DB instance**
    
8.  In the  **Settings**  section next, configure the following options :
    

-   **DB instance identifier:**  `inventory-db`
    
-   **Master username:** `admin`
    
-   **Master password:** `lab-password`
    
-   **Confirm password:** `lab-password`

![7](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/10267175-81a0-42f1-bbca-20b59ec02afe)
    

**Note:**  Please use these values  _verbatim_, do not make any changes.

9.  In the  **Instance configuration**  section, configure the following options for DB instance class:

-   Choose  **Burstable classes (includes t classes)**.
-   Choose  **db.t3.micro**.

10.  In the  **Storage**  section next,

-   For  **Storage type**  choose  **General Purpose SSD (gp2)**  from the Dropdown menu.
-   For  **Allocated storage**  keep :  `20`
    
    .
-   Clear or Deselect  **Enable storage autoscaling**.

![8](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/fabb099c-c636-4de7-a75a-80e180f9f45f)

11.  In the  **Connectivity**  section, configure the following options:

-   For  **Compute resource**
    -   keep default  **Don’t connect to an EC2 compute resource**, as you will establish this manually at a later stage.
-   For  **Virtual private cloud (VPC)**  Choose  **Lab VPC**  from the Dropdown menu.
-   For  **DB Subnet group**, keep default value  **rds-lab-db-subnet-group**
-   For  **Public access**  Keep default value (**No**)


![9](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/4019d8bb-095a-4175-ad5f-e69d260fab67)


-   For  **VPC security group (firewall)**
    -   Choose the  **X**  on  **default**  to remove this security group.
    -   Choose  **DB-SG**  from the dropdown list to add it.
    -   For  **Availability Zone**, Keep default  **No preference**
-   For  **Database authentication**  keep default value  **Password authentication**

![10](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/76fcac22-6a39-4f04-9fdd-802222368748)

12.  In the  **Monitoring**  section

-   Clear/DeSelect the  **Enable Enhanced monitoring**  option.

13.  Expand the following  **Additional configuration**  section by choosing

-   Under  **Database options**, for  **Initial database name**, enter :    `inventory`

![11](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/bf3afacf-2104-43e1-a11c-ead5a4ddb825)

This is the logical name of the database that the application will use.

You can review the few other options displayed on the page, but leave them set to their default values. Options include  **automatic backups**,  **Log exports**,  **Encryption**  and  **automatic version upgrades**. The ability to activate these features with check boxes demonstrates the power of using a fully managed database solution instead of installing, backing up, and maintaining the database yourself.

![12](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/33e6e3a7-a476-49bf-89ec-41279f4d83ce)


14.  At the bottom of the page, choose  **Create database**

![13](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/2256d269-f9c3-4148-909b-c40889fdb4ea)

You should receive this message:  **Creating database inventory-db**.

![14](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/143b9851-3ad0-4101-a528-5a302641d20b)

If you receive an error message that mentions  **rds-monitoring-role**, confirm that you have cleared the  **Enable Enhanced monitoring**  option in the previous step, and then try again.

Before you continue to the next task, the database instance status must be  **Available**. This process could take several minutes.

## Task 2: Configuring web application communication with the database instance

This  automatically deployed an Amazon Elastic Compute Cloud (Amazon EC2) instance with a running web application. You must use the IP address of the instance to connect to the application. I this task, you will use application to configure connection settings which will be stored in  **AWS Secrets Manager**  for further use.

![Application Security](https://us-west-2-tcprod.s3.us-west-2.amazonaws.com/courses/CUR-TF-100-EDDBAS/v1.0.3.prod-774844da/1-lab-rds/instructions/en_us/images/application-architecture.png)

15.  On the  **Services** menu, choose  **EC2**.


![15](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/84f13c14-7354-4670-bf9a-613e7941a2ea)
    
16.  In the left navigation pane, choose  **Instances**.
    

In the center pane, there should be a running instance that is named  **App Server**.

17.  Select the check box for the  **App Server**  instance.

![16](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/492eca88-b410-4e94-b0c6-16dcdf965f01)
    
18.  In the  **Details**  tab, copy the  **Public IPv4 address**  to your clipboard.

 ![17](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/5f721d2e-69d5-47cd-ae1a-85304ea3eba7)   


**Tip:**  You can choose copy  to copy the displayed value the displayed value.

19.  Open a new web browser tab, paste the IP address into the address bar, and then press Enter.

The web application should appear. It does not display much information because the application is not yet connected to the database.

20.  Choose  **Settings**.

![18](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/8c121e06-ee70-4841-9c48-af9e4eb3458e)

You can now configure the application to use the Amazon RDS database instance that you created earlier. You first retrieve the database endpoint so that the application knows how to connect to a database.

21.  Return to the AWS Management Console, but do not close the application tab. (You will return to it soon).
    
22.  On the  **Services** menu, choose  **RDS**.

![19](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/a53988b6-6201-4bda-8d68-2425995d704f)
    
23.  In the left navigation pane, choose  **Databases**.
    
24.  Under  **DB identifier**, Choose ‘inventory-db’.

![20](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/1faa6b1e-2ea4-4ccc-80cb-39f5e92b432f)
    
25.  From the  **Connectivity & security**  section, copy the  **Endpoint**  to your clipboard.
    

It should look similar to this example:  `inventory-db.crwxbgqad61a.rds.amazonaws.com`

![21](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/02dcb89c-3e59-4822-9e39-64b099bce5c1)


26.  Return to the browser tab with the inventory application, and enter the following values:

![22](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/3ec3b1f1-a5fb-407b-8a64-bc04817cda48)

-   For  **Endpoint**, paste the endpoint you copied earlier.
-   For  **Database**, enter : `inventory`
    
-   For  **Username**, enter : `admin`
    
-   For  **Password**, enter : `lab-password`
    
-   Choose  **Save**.



![23](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/e5809d5a-8d4b-4619-9048-911d676338aa)

The application will now Save this information into **AWS Secrets Manager ** and connect to the database, load some initial data, and display information.

![24](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/9ebd9595-6041-48cd-848e-45b901021f8c)

27.  You can use the web application to  Add inventory,  edit, and  delete inventory information.

![25](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/1c045ff9-c01b-4a18-a618-8e39f9cb55ef)


The inventory information is stored in the Amazon RDS MySQL database that you created earlier in the lab. This means that any failure in the application server will not lead to loss of any data. It also means that multiple application servers can access the same data.

28.  Insert new records into the table. Ensure that the table has  **5**  or more inventory records.

![26](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/743280c1-4588-43cc-b439-79e7aa0351a2)


You have now successfully launched the application and connected it to the database.

**Optional:**  To access the saved parameters, go to the AWS Management console. On the  **Services** menu, choose  **Secrets Manager**  , choose  **Secrets**.

![27](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/72a2c691-b727-4dc0-8450-d9df150da081)

![28](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/5062fdd3-36cd-4778-bcfd-e18d5b93a418)


## Task 3: Monitoring the Database Instance

Monitoring is an important part of maintaining the reliability, availability, and performance of any database. Amazon RDS service provides many useful metrics to monitor the health of your database instance. In this task you will explore few useful metrics for the database instance you created.

29.  Return to the AWS Management Console.
    
30.  On the  **Services**  menu , choose  **RDS**.

![29](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/15eb82e4-ba45-46b4-8205-22c351843d46)
    
31.  Choose  **Databases**.


![30](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/3dfa1bf8-34e0-4a36-94d9-fdb0448b0c96)

    
32.  Choose `inventory-db`.
    
33.  In the pane below, choose  **Monitoring**  tab.
  
34.  Observe the CloudWatch metrics indicating respective database Instance parameters as shown in example below.
    

![CloudWatch Metrics](https://us-west-2-tcprod.s3.us-west-2.amazonaws.com/courses/CUR-TF-100-EDDBAS/v1.0.3.prod-774844da/1-lab-rds/instructions/en_us/images/rds-lab-monitoring.png)

35.  Perform various operations on the web application like add, update or remove records from inventory database and observe the changes in the values mentioned above.
    
36.  Scroll down further to observe other available metrics.
    
![31](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/bddabd9d-af2e-4c2e-baef-7ecdf35b4e31) 

## Task 4: Performing operations on Database.

In this task, you learn about a few administrative tasks that can be performed on the database in Amazon RDS.

37.  Return to the RDS Management Console (if you have navigated out)
38.  Choose  **Databases**.
39.  Choose `inventory-db`
40.  Under  **Actions**  menu, there are various operations to perform e.g.  **Stop temporarily**,  **Reboot**, etc.
41.  Choose  **Stop temporarily**, to stop the instance temporarily. (Database automatically restarts after 7 days)

![32](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/2a8512b2-d9b2-4a4b-98b3-3c6f236e2752)

-   Select checkbox under ‘Acknolwedgement’
-   Choose  **Stop temporarily**


![33](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/5f9a98c2-4cc3-4640-a8b5-3837d9573337)

​  **Note:**  Stopping the instance also stops the billing charges associated with the running instance. Database(s) continues to occupy storage space and incur billing charges).

42.  Refresh the browser after few minutes to verify that the instance is stopped. (Status = Stopped)

![34](https://github.com/dineshrajdhanapathyDD/Cloud/assets/52989362/c3d1b0dc-17bd-4b49-b502-e586a1775a80)

- Optional - You can  **Start**  the instance, re-connect it to the web application and continue to use.

-  you launched MYSQL RDS database instance, configured an existing web application to interact with the database instance. Then you performed basic tasks such as querying, updating records and monitored the various metrics to gain insights into the health of the database and finally performed basic database administrative operations.

## Keytakeaway

By the end of this module you will be able to:

-   key database concepts.
-   Compare and contrast relational and nonrelational databases.
-   Identify the AWS database services.
-   Discuss the features and concepts of Amazon RDS.
-   Describe the benefits and use cases of Amazon RDS.
-   Describe how to set up an RDS instance using the console.
-   Identify how to connect to the database instance.
-   Discuss how to use SQL commands to read and write to the database.


**Credits : AWS Educate**