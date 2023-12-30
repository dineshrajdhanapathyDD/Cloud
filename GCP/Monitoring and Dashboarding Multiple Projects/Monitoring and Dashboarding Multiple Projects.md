

# Monitoring and Dashboarding Multiple Projects


Google Cloud Monitoring empowers users with the ability to monitor multiple projects from a single metrics scope. In this exercise, you start with three Google Cloud projects, two with monitorable resources, and the third you use to host a metrics scope. You attach the two resource projects to the metrics scope, build uptime checks, and construct a centralized dashboard.

### Objectives

-   Configure a Worker project.
-   Create a metrics scope and link the two worker projects into it.
-   Create and configure Monitoring Groups.
-   Create and test an uptime check.

## Setup and requirements

you get a new Google Cloud project 

 Initial sign-in steps, the project dashboard appears.

![The Project Dashboard which includes tiles for Project Info, APIs, Resources, Trace, Billing, and Error reporting ](https://cdn.qwiklabs.com/dxfeoOcn1ObyC0BYyoqqqSi4rO%2FeMdbWPFjoK6C0YYk%3D)

### Activate Google Cloud Shell

Google Cloud Shell is a virtual machine that is loaded with development tools. It offers a persistent 5GB home directory and runs on the Google Cloud.

Google Cloud Shell provides command-line access to your Google Cloud resources.

1.  In Cloud console, on the top right toolbar, click the Open Cloud Shell button.
    
    ![Highlighted Cloud Shell icon](https://cdn.qwiklabs.com/00tA48qOVOyHrSa1DA7LwccfwQ9Z%2BE6dkvQ1MYPHzhQ%3D)
    
2.  Click  **Continue**.
    

It takes a few moments to provision and connect to the environment. When you are connected, you are already authenticated, and the project is set to your  _PROJECT_ID_. For example:

![Project ID highlighted in the Cloud Shell Terminal](https://cdn.qwiklabs.com/hmMK0W41Txk%2B20bQyuDP9g60vCdBajIS%2B52iI2f4bYk%3D)

**gcloud**  is the command-line tool for Google Cloud. It comes pre-installed on Cloud Shell and supports tab-completion.

-   You can list the active account name with this command:

gcloud auth list

**Output:**

Credentialed accounts:
 - @.com (active)

**Example output:**

Credentialed accounts:
 - google1623327_student@qwiklabs.net

-   You can list the project ID with this command:

gcloud config list project


**Output:**

project = 

**Example output:**

project = qwiklabs-gcp-44776a13dea667a6

**Note:** Full documentation of  **gcloud**  is available in the  [gcloud CLI overview guide](https://cloud.google.com/sdk/gcloud) .

## Task 1. Configure the resource projects

It has three projects pre-created in it, the project IDs are displayed in the upper-left corner of the lab steps page.

![The Lab Details panel with credentials for multiple projects listed](https://cdn.qwiklabs.com/YSYl63KqoOqGgz9Cj%2FqISbU6l9STKjwTXQEmXbdiTeE%3D)

The first project (ID 1) will be the scoping project. Projects ID 2 and ID 3 will be the monitored/resource projects. Per Google's recommended best practices, the project we use to host the metrics scope will not be one of the projects actually housing monitored resources.

In this task, you:

-   Create an NGINX web server in each of your worker projects.

### Configure two resource projects

Let's start by building some resources to monitor.

1.  Open a text document on your computer and in it, make note of the three project IDs.
    
    -   Label Project ID 1 as  **Monitoring Project**.
    -   Label Project ID 2 as  **Worker 1**.
    -   Label Project ID 3 as  **Worker 2**.
    
    In the rest of this exercise, the project IDs are referred to by these names.
    
2.  In the Google Cloud Console page, use the project dropdown near the upper-left corner of the interface to switch to the  `Worker 1`  project. Remember, it is the project with the ID you labeled  **Worker 1**  in the text file you created in Step 1.
    

**Note:**  If you don't see all three projects, type  **qwiklabs**  in the search box and the missing projects should appear.

3.  In the Cloud console, on the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **Compute Engine**  >  **VM Instances**.
    
    This may take a minute to initialize for the first time.
    
4.  To create a new instance, click  **CREATE INSTANCE**.
    
5.  There are many parameters you can configure when creating a  **new instance**. Use the following for this lab:
  
Field

Value

Additional Information

**Name**

**worker-1-server**

Name for the VM instance

**Region**

`<REGION>`

For more information about regions, see the Compute Engine guide,  [Regions and Zones](https://cloud.google.com/compute/docs/zones).

**Zone**

`<ZONE>`

**Note:**  Remember the zone that you selected to use later. For more information about zones, see the Compute Engine guide,  [Regions and Zones](https://cloud.google.com/compute/docs/zones).

**Series**

**E2**

Name of the series

**Machine Type**

**2 vCPU**

This is an (e2-medium), 2-CPU, 4GB RAM instance. Several machine types are available, ranging from micro instance types to 32-core/208GB RAM instance types. For more information, see the Compute Engine guide,  [About machine families](https://cloud.google.com/compute/docs/machine-types).  **Note:**  A new project has a default  [resource quota](https://cloud.google.com/compute/docs/resource-quotas), which may limit the number of CPU cores. You can request more when you work on projects outside this lab.

**Boot Disk**

**New 10 GB balanced persistent disk**  **OS Image: Debian GNU/Linux 11 (bullseye)**

Several images are available, including Debian, Ubuntu, CoreOS, and premium images such as Red Hat Enterprise Linux and Windows Server. For more information, see Operating System documentation.

**Firewall**

**Allow HTTP traffic**

Select this option in order to access a web server that you install later.  **Note:**  This automatically creates a firewall rule to allow HTTP traffic on port 80.

6.  Click  **Create**.
    
    It should take about a minute for the VM,  `worker-1-server`, to be created. After  `worker-1-server`  is created, the  **VM Instances**  page lists it in the VM instances list.
    
7.  To use  **SSH**  to connect to the VM, click  **SSH**  to the right of the instance name,  `worker-1-server`.
    
    This launches an SSH client directly from your browser.
    
    **Note:**  Learn more about how to use SSH to connect to an instance from the Compute Engine guide,  [Connect to Linux VMs using Google tools](https://cloud.google.com/compute/docs/instances/connecting-to-instance).
    

Now you install an NGINX web server, one of the most popular web servers in the world, to connect your VM to something.

8.  Update the OS:
    
    `sudo apt-get update`
    
 
    
    **Expected output:**
    
     Get:1 http://security.debian.org stretch/updates InRelease [94.3 kB]
     Ign http://deb.debian.org strech InRelease
     Get:2 http://deb.debian.org strech-updates InRelease [91.0 kB]
     ...
    
9.  Install NGINX:
    
    `sudo apt-get install -y nginx`
 
    **Expected output:**
    
     Reading package lists... Done
     Building dependency tree
     Reading state information... Done
     The following additional packages will be installed:
     ...
    
10.  Confirm that NGINX is running:
    
   `ps auwx | grep nginx`

   **Expected output:**
    

 root      2330  0.0  0.0 159532  1628 ?        Ss   14:06   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
 www-data  2331  0.0  0.0 159864  3204 ?        S    14:06   0:00 nginx: worker process
 www-data  2332  0.0  0.0 159864  3204 ?        S    14:06   0:00 nginx: worker process
 root      2342  0.0  0.0  12780   988 pts/0    S+   14:07   0:00 grep nginx

11.  To see the web page, return to the Cloud console and click the  **External IP**  link in the row for your machine, or add the  **External IP**  value to  `http://EXTERNAL_IP/`  in a new browser window or tab.

This default web page should open.

![Default nginx page; Welcome to nginx!](https://cdn.qwiklabs.com/05LibSZYP0ZTRd4%2BakTULc%2BcHIFcdmXiF4MYcOAH6rk%3D)

12.  Use the project dropdown to switch to  `Worker 2`  project.
    
13.  Perform similar steps in Worker 2:
   
   -   Create a VM instance with  **worker-2-server**.
    -   Allow HTTP traffic.
    -   SSH the VM instance.
    -   Install NGINX.
14.  Use the project dropdown to switch back to  `Worker 1`  project.
    
15.  Use the  **Navigation menu**  to view your new  **Compute Engine > VM instances**.
    
16.  Copy the  `External IP`  and paste it in a new browser tab. Make sure you can see your new Worker 1 web server.
    
17.  In the text file you created in Step 1, add a new entry  **worker-1-server**, and next to it, paste your copied external IP.
    
18.  Use the project dropdown to switch to  `Worker 2`  project. You should still be on the  `VM instances`  page. Again:
    
   -   Copy the  `External IP`  value.
    -   Paste it in the browser and view the new server 2 home page
    -   Add a new  **worker-2-server**  entry into your text file and add its IP.

To check your progress in this lab, click  **Check my progress**  below. A checkmark means you're successful.



## Task 2. Create a metrics scope and link the two worker projects into it

There are a number of ways you might want to configure the relationship between the host project doing the monitoring, and the project or projects being monitored.

In general, if you're going for the multiple projects being centrally monitored approach, then it's recommended that the monitoring project contains nothing but monitoring related resources and configurations. That's exactly the approach taken here.



-   Configure the central monitoring link to the Worker 1 and 2 projects.

### Configure the monitoring link to the Worker 1 and 2 projects

1.  Use the project dropdown to switch to the  `Monitoring Project`.
    
2.  Use the  **Navigation menu**  to switch to the  **Monitoring > Overview**  page. Because this is the first time you visited Monitoring in this project, Google Cloud will automatically create a metrics scope. You may have to wait for the metrics scope to be created.
    
3.  Once the metrics scope is created and the Cloud Monitoring overview displays, in the left-hand menu, click  **Settings**.
    

![Settings page with the summary tab selected](https://cdn.qwiklabs.com/FD6Yil%2BxIU672ywcwyME77lydjsUfl6C%2BSgOc0S9jxg%3D)

4.  Click  **ADD GCP PROJECTS**.
    
5.  Click  **Select Project**  and select the  `Worker 1`  and  `Worker 2`  projects.
    
6.  Click  **ADD PROJECTS**.
    
7.  Switch to the  **Dashboards**  page.
    

**Note:**  If you don't see anything, refresh the page and after a minute or two, you'll see the Disks, Firewalls, Infrastructure Summary, and VM Instances from the other two projects.

8.  Click  **VM Instances**. Take a few minutes and explore the dashboard.
    
9.  Click  **Dashboards**  and take a few minutes exploring the other available dashboards, especially Infrastructure Summary.
    

## Task 3. Create and configure Monitoring groups

Google Cloud Monitoring lets you monitor a set of resources together as a single group. Groups can then be linked to alerting policies, dashboards, etc. Each metrics scope can support up to five-hundred groups and up to six layers of sub-groups. Groups can be created using a variety of criteria, including labels, regions, and applications.

You add a label  `component=frontend`  to each of the web servers as a way to track your servers that are externally facing. In this case, it also allow you to easily add them to the same group.

In this task, you:

-   Assign labels to the web servers to make them easier to track.
-   Create a resource group and place the servers into it.
-   Create a sub-group just for frontend dev servers.

### Assign labels to your web servers to make them easier to track

1.  Use the  **Navigation menu**  to navigate to the  **Cloud overview > Dashboard**  page.
    
2.  Use the project dropdown to switch to the  `Worker 1`  project.
    
3.  Use the  **Navigation menu**  to navigate to your  **Compute Engine > VM instances**.
    
4.  Click the link to navigate to the  **worker-1-server**  settings.
    
5.  Click the  **Edit**  button.
    
6.  Click the  **Manage labels**  button.
    
7.  Click the  **+Add label**  button and create a label with the key  `component`  and the value  `frontend`.
    
8.  Click the  **+Add label**  button and create a label with the key  `stage`  and the value  `dev`.
    
9.  Click  **Save**.
    
10.  **Save**  the configuration changes.
    
11.  Use the project dropdown to switch to the  `Worker 2`  project.
    
12.  Perform similar tasks:
    
   -   Edit the settings for the  **worker-2-server**.
    -   Click the  **Manage labels**  button.
    -   Click the  **+Add label**  button and create a label with the key  `component`  and the value  `frontend`.
    -   Click the  **+Add label**  button and create a label with the key  `stage`  and the value  `test`. (Note the  **test**  value)
    -   **Save**  the changes.

### Create a resource group and place the servers into it

1.  Use the project dropdown to switch to the  `Monitoring Project`, then navigate to the  **Monitoring > Overview**.
    
2.  In the left-hand menu, navigate to  **Groups**.
    
3.  Create a new monitoring group using the  **+CREATE GROUP**  link.
    
4.  Name the group  `Frontend Servers`.
    
5.  For the criteria, use:

    
**Setting**| Type   |**Tag**                       |Operator               | Value
|----------------|-------------------------------|-----------------------------|------------| -----|
|**Value**|**Tag** | **component**|**Equals**  | **frontend**

6.  Make sure that  `Resources Selected`  on the right hand of the page is displaying  **2 VM Instances currently selected.**  If not, double-check your criteria.
    
7.  **Create**  the group.
    
8.  Refresh the page and after a minute or so, you should see several metrics and charts for your two VMs.
    

### Create a sub-group just for frontend dev servers

1.  In the  `Frontend Servers`  group, locate the  `Subgroups`  section and click  **CREATE SUBGROUP**.
    
2.  Configure the subgroup with the following settings:
    
|          Setting      |Name     |                                           |
|----------------|-------------------------------|-----------------------------|
Value |`Frontend Dev`


**Criteria 1**

|        Type     |Tag   |     Operator   | Value                                   |
|----------------|-------------------------------|-----------------------------|-----|
`Tag` |`component`|`Equals`|`frontend`|


3.  Click  **Done**  for the first criteria, then  **Add a criterion**:

Setting

Value

**Criteria 2**

|        Type     |Tag   |     Operator   | Value                                   |
|----------------|-------------------------------|-----------------------------|-----|
`Tag` |`stage`|`Equals`|`dev`|



4.  Click  **Done**  for the second criteria, then select the  **And**  combine criteria operator to join them.
    
5.  Click  **Create**.
    
6.  Navigate back to the  `Groups`  home page. Notice how the  `Frontend Servers`  group can now be expanded to show its sub-group. The UI also displays a clickable link containing a little information about the types of resources contained by the group.
    

## Task 4. Create and test an uptime check

Google Cloud uptime checks test the liveliness of externally facing HTTP, HTTPS, or TCP applications by accessing said applications from multiple locations around the world. The subsequent report includes information on uptime, latency, and status. Uptime checks can also be used in alerting policies and dashboards.

-   Create an uptime check for the Frontend Servers group.
-   Investigate out how an uptime check handles failure.

### Create an uptime check for the Frontend Servers group

If you've already created a group that contains the same resources that need to be uptime checked, then it's easy to create a single uptime check for multiple servers.

1.  In the Monitoring section of your  `Monitoring Project`, click  **Uptime checks**.
    
2.  At the top of the page, follow the link to  **+CREATE UPTIME CHECK**.
    
3.  Configure a new uptime check with the following settings (don't press Save yet):
    
| Setting     |Protocol   |   Resource Type | Applies To                                |Group|Path|Check Frequency
|----------------|-------------------------------|-----------------------------|-----|------|----|----|
Value|`HTTP`|`Instance`|`Group`|`Frontend Servers`|`/`|`1 minute`

4.  Click  **Continue**, to leave other options as defaults.
    
5.  Click  **Continue**, in the Response Validation section.
    
6.  If you like, in the  **Alert & Notification**  section, click  **Notification Channels**  dropdown and use  **Manage Notification Channels**  to add your email address as a valid notification option. The Alert will be enabled by default but won't actually notify anyone otherwise.
    
7.  Click  **Continue**.
    
8.  Set Title as  `Frontend Servers Uptime`.
    
9.  Click  **Test**  and verify a 200 response.
    
10.  **Create**  the uptime check.
    
11.  In the list of uptime checks, click your new  **Frontend Servers Uptime**  to view its dashboard.
    
12.  Wait a few minutes and refresh. The dashboard populates information about the check results. Explore the charts and data.
    
13.  On the right side of the page in the  `Configuration`  box, copy the  `Check ID`  value and paste it in your notes text file. It should read  `frontend-servers-uptime.`
    

### Check out how an uptime check handles failure

Our uptime check is working, but how about if there was a failure? Let's trigger a failure and investigate the resulting uptime check and alert behavior.

1.  Make sure you have a few minutes of data in your uptime check's dashboard before proceeding.
    
2.  Using the  **Navigation menu**  to navigate to the  **Cloud overview > Dashboard**  page.
    
3.  Use the project dropdown to switch to the  `Worker 1`  project.
    
4.  Use the  **Navigation menu**  to navigate to your  **Compute Engine > VM instances**.
    
5.  Select the checkbox next to  **worker-1-server**  and  **STOP**  it running.
    
6.  Refresh the  `VM instances`  page and wait until you see the server has stopped running.
    
7.  Use the project dropdown to switch to the  `Monitoring Project`, then navigate to  **Monitoring > Uptime checks > Frontend Servers Uptime**.
    
8.  Examine the  `Uptime Check Latency`  and the  `Passed Checks`  chart. It could take a minute for the failures to start displaying.
    

### What can Cloud Monitoring, Logging, and Alerting tell us?

1.  Navigate to  **Monitoring > Metrics explorer**.
    
2.  Click  `Metric`  dropdown, select  **VM Instance > Uptime_check > Check passed**  and click  **Apply**. On a side note, after you investigate the Check passed metric, you might try searching for "uptime_check" will display some of the other metrics you might like to investigate.
    
3.  Set the labels in  `Group By`  to  **checked_resource_id**  (you might have to scroll) to group the check results by server and click  **OK**  .
    
4.  Take a moment to examine the results.
    
5.  Use the  **Navigation menu**  to navigate to  **Logging > Logs Explorer**.
    
6.  Enable  **Show query**, and delete anything there. Click  **Log name**. Locate and add the  **uptime_checks**  log, then select  **Apply**. Click  **Run query**.
    
7.  Expand and examine one of the log entries. What useful information does it provide?
    
8.  In the same entry, examine the  `labels`  section and locate the  `check_id.`  Consult your text notes document and compare the id you recorded there. They should match.
    
9.  Use the  **Navigation menu**  to navigate to  **Monitoring > Alerting**.
    
10.  Investigate the firing alert. If you added yourself as a notification channel, review the email.
    

**Note:** If a Monitoring group is created based on labels, then the group will keep checking for powered off server for 5 minutes. After 5 minutes, Google Cloud determines the server should no longer be counted as a member of the group.

**This is important because if an uptime check is tied to the group, then it will only report failures while the group reports that missing server.**

When the group quits reporting the off server, the uptime check quits checking for it, and suddenly the check starts passing again. This can be a real issue if you're not careful.

## Task 5. Create a custom dashboard

There will be times when the humans running a Google Cloud system want to investigate its status. This may be related to curiosity, capacity planning, or perhaps in response to an alert.

Regardless, when data is expressed in chart form, as opposed to a list of items or values, it tends to be easier to spot trends, anomalies, and highs or lows. In this task, we add a chart for our developers to use as a way to track some of the happenings on the frontend servers.

In this task, you:

-   Create a developer dashboard and add an uptime chart to it.
-   Add and test a CPU utilization chart to the dashboard.

### Create a developer dashboard and add an uptime chart to it

If you were interested in what was happening on your developer webserver, it would be helpful to have a dashboard of charts just for that single server. In this section, you create a dashboard with an uptime check summary chart.

1.  Using the  **Navigation menu**, navigate to the  **Cloud overview > Dashboard**  page.
    
2.  Use the project dropdown to switch to the  `Worker 1`  project.
    
3.  Use the  **Navigation menu**  to navigate to your  **Compute Engine > VM instances**.
    
4.  Select the checkbox next to  **worker-1-server**  and  **START**  it running.
    
5.  Use the project dropdown to switch to the  `Monitoring Project`, then navigate to  **Monitoring > Dashboards**.
    
6.  At the top of the page, press  **+CREATE DASHBOARD**.
    
7.  For  **New Dashboard Name**, type  **Developer's Frontend**.
    
8.  Click  **+ ADD WIDGET**  and click  **Line**  chart.
    
|     Setting           |Widget Title                        |Metric                       |
|----------------|-------------------------------|-----------------------------|
Value|`Dev Server Uptime`|`VM Instance > Uptime_check > check_passed`|

9.  Click  **Apply**.
    
10.  Examine the values displayed on the chart. Our worker-1-server is our core development server. Take note of the  `checked_resource_id`  value from one of its check response rows. You must pick the value from a list in the next step.
    
11.  Click  `ADD FILTER`:

|     Setting           |Label                       |Value                     |
|----------------|-------------------------------|-----------------------------|
Value|`instance_id`|`Select from dropdown`|    

12.  In  **Datapoint Alignment**, set the  `Alignment function`  to  **Count true**. Set  `Min alignment period`  **5m**.
    
13.  Click  **Apply**.
    

### Add and test a CPU utilization chart to the dashboard

Another key piece of information about what's going on inside your development server is its CPU load. Overall it is nice to know what's happening with the NGINX server itself, but without the installation of the logging and monitoring agents, you can't do that yet.

1.  Add another chart to our dashboard. Click  **+ ADD WIDGET**  and click  **Line**  chart.
    
2.  In the  **Metric**, search/select  **VM Instance > Instance > cpu utilization**.
    
3.  Click  **Apply**.
    
4.  Click  `ADD FILTER`:
    
|     Setting           |Label                       |Value                     |
|----------------|-------------------------------|-----------------------------|
Value|`instance_name`|`worker-1-server`|  

5.  Click  **Apply**.
    
6.  Cloud Shell doesn't always work well as a platform for generating load test traffic, since it sometimes thinks you're doing something malicious and terminates your session. Use your second web server to generate the load instead. Expand the  **Navigation menu**, right-click  **Compute Engine**, and open the link in a new tab or window.
    
7.  Use the project dropdown to switch to the  `Worker 2`  project.
    
8.  **SSH**  into your  `worker-2-server`.
    
9.  Update the server's package database and install the apache2-utils. Apache Bench is a quick easy tool you can use to generate HTTP load:
    
```
sudo apt-get update
sudo apt-get install apache2-utils
```


Enter  `Y`  if asked "Do you want to continue? [Y/n]"

10.  Before you use Bench, set up a URL to your server. Find your  `worker-1-server`  external IP in your notes file and use it to construct the URL environmental variable below. Don't omit the "http://":

```
URL=http://[worker-1-server ip]
```

11.  Throw some load at your server. The following command executes 100 requests at a time and continues to do so up to a total of 100,000 requests. Don't miss the trailing "/" after the URL:

```
ab -s 120 -n 100000 -c 100 $URL/
```


12.  Once Bench finishes its run, wait a minute or so and then execute:

```
ab -s 120 -n 500000 -c 500 $URL/
```

13.  While the second series of traffic is generated, switch back to your dashboard. After a little time, you see the two distinct spikes in CPU load.



## Review

You now know how to set up a central project for monitoring other projects, can create monitoring resource groups, uptime checks, and custom dashboards. You are well on your way. Nice job.

**Credits: GCP Cloudlab** 
