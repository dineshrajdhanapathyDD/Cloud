




# Getting Started with VPC Networking and Google Compute Engine



## Overview

Google Cloud Virtual Private Cloud (VPC) provides networking functionality to Compute Engine virtual machine (VM) instances, Kubernetes Engine containers, and App Engine flexible environment. In other words, without a VPC network you cannot create VM instances, containers, or App Engine applications. Therefore, each Google Cloud project has a  **default**  network to get you started.

You can think of a VPC network as similar to a physical network, except that it is virtualized within Google Cloud. A VPC network is a global resource that consists of a list of regional virtual subnetworks (subnets) in data centers, all connected by a global wide area network (WAN). VPC networks are logically isolated from each other in Google Cloud.

In this lab, you create an auto mode VPC network with firewall rules and two VM instances. Then, you explore the connectivity for the VM instances.

### Objectives

In this lab, you learn how to perform the following tasks:

-   Explore the default VPC network
-   Create an auto mode network with firewall rules
-   Create VM instances using Compute Engine
-   Explore the connectivity for VM instances

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

## Task 1. Explore the default network

Each Google Cloud project has a  **default**  network with subnets, routes, and firewall rules.

### View the subnets

The  **default**  network has a subnet in  [each Google Cloud region](https://cloud.google.com/compute/docs/regions-zones/#available).

1.  In the Cloud Console, on the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **VPC network**  >  **VPC networks**.
 
![1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/13c33ee9-fc9d-4631-a236-01f592cc8173)

2.  Click  **default**.

 ![2](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/488afad7-ec46-4c98-b661-bbeac4f41d09)

Notice the  **default**  network with its subnets.  
Each subnet is associated with a Google Cloud region and a private RFC 1918 CIDR block for its internal  **IP addresses range**  and a  **gateway**.

### View the routes

Routes tell VM instances and the VPC network how to send traffic from an instance to a destination, either inside the network or outside Google Cloud. Each VPC network comes with some default routes to route traffic among its subnets and send traffic from eligible instances to the internet.

1.  In the left pane, click  **Routes**.
    
2.  In  **Effective Routes**  tab select  **default**  for network and select any region.
    
3.  Click  **VIEW**.

![3](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a5245fdf-06c3-48de-a967-548ddffd69cf)

    
    Notice that there is a route for each subnet and one for the  **Default internet gateway**  (0.0.0.0/0).  
    These routes are managed for you, but you can create custom static routes to direct some packets to specific destinations. For example, you can create a route that sends all outbound traffic to an instance configured as a NAT gateway.
    

### View the Firewall rules

Each VPC network implements a distributed virtual firewall that you can configure. Firewall rules allow you to control which packets are allowed to travel to which destinations. Every VPC network has two implied firewall rules that block all incoming connections and allow all outgoing connections.

-   In the left pane, click  **Firewall**.  
    Notice that there are 4  **Ingress**  firewall rules for the  **default**  network:
    -   default-allow-icmp
    -   default-allow-rdp
    -   default-allow-ssh
    -   default-allow-internal

![4](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/66ca4e4a-b6e7-4f6a-842b-52a9f1159af5)

**Note:** These firewall rules allow  **ICMP**,  **RDP**, and  **SSH**  ingress traffic from anywhere (0.0.0.0/0) and all  **TCP**,  **UDP**, and  **ICMP**  traffic within the network (10.128.0.0/9). The  **Targets**,  **Filters**,  **Protocols/ports**, and  **Action**  columns explain these rules.

### Delete the Firewall rules

1.  In the left pane, click  **Firewall**.
2.  Select all default network firewall rules.
3.  Click  **Delete**.
4.  Click  **Delete**  to confirm the deletion of the firewall rules.

![Firewall page with all listed firewall rules selected and the delete button highlighted](https://cdn.qwiklabs.com/8k%2BijUfKrspiL2tU2xNwFcthRpVmj47rO9BCqwLj%2BEA%3D)

### Delete the default network

1.  In the left pane, click  **VPC networks**.
2.  Select the  **default**  network.
3.  Click  **Delete VPC network**.
4.  Click  **Delete**  to confirm the deletion of the  **default**  network.  
    Wait for the network to be deleted before continuing.
5.  In the left pane, click  **Routes**.  
    Notice that there are no routes.
6.  In the left pane, click  **Firewall**.  
    Notice that there are no firewall rules.

**Note:** Without a VPC network, there are no routes and no firewall rules!

![6](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/12ad47ba-0e2f-4f3d-8824-80453589e2ed)

### Try to create a VM instance

Verify that you cannot create a VM instance without a VPC network.

1.  On the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)
2. , click  **Compute Engine**  >  **VM instances**.
3.  Click  **Create instance**.

![7](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/d152d636-e299-4948-9fd8-402b49399e4f)

4.  Accept the default values and click  **Create**. Notice the error.
5.  Click  **Go to Issues**.


![8](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/3d855f6f-6405-4721-95e4-2bdea3326bdf)

6.  In  **Network Interfaces**, notice the no more networks and no network available errors.
7.  Click  **Cancel**.

![9](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/ad1aba0d-cec4-4fcf-8f42-ed6fe2705aa8)


**Note:** As expected, you cannot create a VM instance without a VPC network!

## Task 2. Create a VPC network and VM instances

Create a VPC network so that you can create VM instances.

### Create an auto mode VPC network with Firewall rules

Replicate the  **default**  network by creating an auto mode network.

1.  On the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **VPC network**  >  **VPC networks**.
2.  Click  **Create VPC network**.
3.  For  **Name**, type  **mynetwork**.
4.  For  **Subnet creation mode**, click  **Automatic**.  
    Auto mode networks create subnets in each region automatically.
5.  For  **Firewall**, select all available rules.  
    These are the same standard firewall rules that the default network had.  
    The  **deny-all-ingress**  and  **allow-all-egress**  rules are also displayed, but you cannot check or uncheck them because they are implied. These two rules have a lower  **Priority**  (higher integers indicate lower priorities) so that the allow ICMP, custom, RDP and SSH rules are considered first.
6.  Click  **Create**.  
    When the new network is ready, notice that a subnet was created for each region.
7.  Explore the IP address range for the subnets in  `Lab Region`  and  **europe-west2**.

![10](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e31a96b3-c71a-46b9-9635-16ecb7305a8d)

**Note:** If you ever delete the default network, you can quickly re-create it by creating an auto mode network as you just did. After recreating the network, allow-internal changes to allow-custom firewall rule.

### **Create a VM instance in  `Lab Region`**

Create a VM instance in the  `Lab Region`  region. Selecting a region and zone determines the subnet and assigns the internal IP address from the subnet's IP address range.

1.  On the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **Compute Engine**  >  **VM instances**.
    
2.  Click  **Create instance**.
    
3.  Specify the following, and leave the remaining settings as their defaults:



|                |Property                       |Value (type value or select option as specified)              |
|----------------|-------------------------------|-----------------------------|
|1|Name          |    `mynet-us-vm`           |
|     2    |   Region         |        `Lab Region`      |
|    3      | Zone|`Lab Zone`|
|4|Series| `E2`|
|5|Machine type| `e2-micro (2 vCPU, 1 GB memory)`|


![12](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/48d169a1-4b02-49ea-b077-f5d871d57b82)


4.  Click  **Create**.
    

### Create a VM instance in europe-west2

Create a VM instance in the europe-west2 region.

1.  Click  **Create instance**.
    
2.  Specify the following, and leave the remaining settings as their defaults:
   
|                |Property                       |Value (type value or select option as specified)              |
|----------------|-------------------------------|-----------------------------|
|1|Name          |    `mynet-eu-vm`           |
|     2    |   Region         |        `europe-west2`     |
|    3      | Zone|`europe-west2-c`|
|4|Series| `E2`|
|5|Machine type| `e2-micro (2 vCPU, 1 GB memory)`|

![13](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/09b5ba3f-cfc4-4e3a-8333-eaa1a7c548de)

   
3.  Click  **Create**.
  
![14](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/b01d2206-f874-449f-9dc7-db0d9cf50e2e)  

**Note:** The  **External IP addresses**  for both VM instances are ephemeral. If an instance is stopped, any ephemeral external IP addresses assigned to the instance are released back into the general Compute Engine pool and become available for use by other projects.

When a stopped instance is started again, a new ephemeral external IP address is assigned to the instance. Alternatively, you can reserve a static external IP address, which assigns the address to your project indefinitely until you explicitly release it.

- Click  _Check my progress_  to verify the objective.

- Create a VPC network and VM instance

- Check my progress

![16](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/7e145177-7847-4b88-9c94-e380965ed6e1)

## Task 3. Explore the connectivity for VM instances

Explore the connectivity for the VM instances. Specifically, try to SSH to your VM instances using tcp:22, and ping both the internal and external IP addresses of your VM instances using ICMP. Then explore the effects of the firewall rules on connectivity by removing the firewall rules individually.

### Verify connectivity for the VM instances

The firewall rules that you created with  **mynetwork**  allow ingress SSH and ICMP traffic from within  **mynetwork**  (internal IP) and outside that network (external IP).

1.  On the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **Compute Engine**  >  **VM instances**.  
    Note the external and internal IP addresses for  **mynet-eu-vm**.
    
2.  For  **mynet-us-vm**, click  **SSH**  to launch a terminal and connect.
    
3.  If an  **Authorize**  popup appears, click on  **Authorize**
    
![17](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/8d188b3d-d2b6-4291-b97b-8a9967f8dbb8)

**Note:** You can SSH because of the  **allow-ssh**  firewall rule, which allows incoming traffic from anywhere (0.0.0.0/0) for  **tcp:22**. The SSH connection works seamlessly because Compute Engine generates an SSH key for you and stores it in one of the following locations:

-   By default, Compute Engine adds the generated key to project or instance metadata.
-   If your account is configured to use OS Login, Compute Engine stores the generated key with your user account.

Alternatively, you can control access to Linux instances by creating SSH keys and editing public SSH key metadata.

3.  To test connectivity to  **mynet-eu-vm**'s internal IP, run the following command, replacing  **mynet-eu-vm**'s internal IP:

ping -c 3 <Enter mynet-eu-vm's internal IP here>

Copied!

content_copy

You can ping  **mynet-eu-vm**'s internal IP because of the  **allow-custom**  firewall rule.

4.  To test connectivity to  **mynet-eu-vm**'s external IP, run the following command, replacing  **mynet-eu-vm**'s external IP:

ping -c 3 <Enter mynet-eu-vm's external IP here>

Copied!

content_copy

![18](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/63229d9d-0582-413c-bc6b-23d7f691e10c)



![19](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/d2cd5bf7-ac57-4650-b578-57ac7c8039c3)

**Note:** You can SSH to  **mynet-us-vm**  and ping  **mynet-eu-vm**'s internal and external IP address as expected. Alternatively, you can SSH to  **mynet-eu-vm**  and ping  **mynet-us-vm**'s internal and external IP address, which also works.

### Remove the allow-icmp firewall rules

Remove the  **allow-icmp**  firewall rule and try to ping the internal and external IP address of  **mynet-eu-vm**.

1.  On the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **VPC network**  >  **Firewall**.
    
2.  Select the  **mynetwork-allow-icmp**  rule.

![20](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/3d2e4ca1-f505-44fa-bfe9-45b03927518e)
    
3.  Click  **Delete**.
    
4.  Click  **Delete**  to confirm the deletion.  
    Wait for the firewall rule to be deleted.
    
5.  Return to the  **mynet-us-vm**  SSH terminal.
    
6.  To test connectivity to  **mynet-eu-vm**'s internal IP, run the following command, replacing  **mynet-eu-vm**'s internal IP:
    
ping -c 3 <Enter mynet-eu-vm's internal IP here>

Copied!

content_copy

![21](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/a8bc93f3-0366-4efc-8690-e65055a3cad2)


You can ping  **mynet-eu-vm**'s internal IP because of the  **allow-custom**  firewall rule.


7.  To test connectivity to  **mynet-eu-vm**'s external IP, run the following command, replacing  **mynet-eu-vm**'s external IP:

ping -c 3 <Enter mynet-eu-vm's external IP here>

Copied!

content_copy




**Note:** The  **100% packet loss**  indicates that you cannot ping  **mynet-eu-vm**'s external IP. This is expected because you deleted the  **allow-icmp**  firewall rule!

### Remove the allow-custom firewall rules

Remove the  **allow-custom**  firewall rule and try to ping the internal IP address of  **mynet-eu-vm**.

1.  On the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **VPC network**  >  **Firewall**.
2.  Select the  **mynetwork-allow-custom**  rule.
3.  Click  **Delete**.
4.  Click  **Delete**  to confirm the deletion.  
    Wait for the firewall rule to be deleted.

![22](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/86bd2abd-ca4d-4c3f-8ecc-e8ea4ae58ea3)


5.  Return to the  **mynet-us-vm**  SSH terminal.
6.  To test connectivity to  **mynet-eu-vm**'s internal IP, run the following command, replacing  **mynet-eu-vm**'s internal IP:

ping -c 3 <Enter mynet-eu-vm's internal IP here>

Copied!

content_copy

![24](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/6095f8d7-5a53-466c-b823-3cd722586403)

**Note:** The  **100% packet loss**  indicates that you cannot ping  **mynet-eu-vm**'s internal IP. This is expected because you deleted the  **allow-custom**  firewall rule!

7.  Close the SSH terminal:

exit

Copied!

content_copy

![25](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/9d33648d-3e6d-49d9-b6b7-edfbc21de916)

### Remove the allow-ssh firewall rules

Remove the  **allow-ssh**  firewall rule and try to SSH to  **mynet-us-vm**.

1.  On the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D "Navigation menu")), click  **VPC network**  >  **Firewall**.
2.  Select the  **mynetwork-allow-ssh**  rule.
3.  Click  **Delete**.
4.  Click  **Delete**  to confirm the deletion.
5.  Wait for the firewall rule to be deleted.

![23](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/23cc617c-a4b8-4351-ab09-f27d2ec9d33f)

![26](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/8e8c91f1-9bfc-43c8-b9c2-6c442cc067cb)

6.  On the  **Navigation menu**, click  **Compute Engine**  >  **VM instances**.

![27](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/35334562-4a65-4847-8875-3e12eca443ce)

7.  For  **mynet-us-vm**, click  **SSH**  to launch a terminal and connect.

![28](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/11b7b9b7-770c-4746-9ae9-07a716ee717d)


**Note:** The  **Connection failed**  message indicates that you cannot SSH to  **mynet-us-vm**  because you deleted the  **allow-ssh**  firewall rule!

## Task 4. Review

In this lab, you explored the default network along with its subnets, routes, and firewall rules. You deleted the default network and determined that you cannot create any VM instances without a VPC network.

Thus, you created a new auto mode VPC network with subnets, routes, firewall rules, and two VM instances. Then you tested the connectivity for the VM instances and explored the effects of the firewall rules on connectivity.

## End your lab

When you have completed your lab, click  **End Lab**. Google Cloud Skills Boost removes the resources you’ve used and cleans the account for you.
