




## Overview

In this lab, you use Google Cloud Marketplace to quickly and easily deploy a LAMP stack on a Compute Engine instance. The Bitnami LAMP Stack provides a complete web development environment for Linux that can be launched in one click.

![1](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/e07c3c6b-72b5-443f-bc89-eee7637f43c5)

You can learn more about the Bitnami LAMP stack from the Bitnami Documentation article  [Google Cloud Platform](https://docs.bitnami.com/google/).



## Objectives

In this lab, you learn how to launch a solution using Cloud Marketplace.

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
    
![2](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/1fd83c0b-5942-45e1-88b0-4fe22acfe0e9)

**Note:**  Do not click  **End Lab**  unless you have finished the lab or want to restart it. This clears your work and removes the project.


## Task 2. Use Cloud Marketplace to deploy a LAMP stack

1.  In the Google Cloud Console, on the  **Navigation menu**  (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), click  **Marketplace**.
    
2.  In the search bar, type  `LAMP`  and then press  **ENTER**.
    
3.  In the search results, click  **LAMP Packaged by Bitnami**.
    
![3](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/512701f7-6d8e-4649-be36-5a5220493e8e)

    If you choose another LAMP stack, such as the Google Click to Deploy offering, the lab instructions will not work as expected.
    
4.  On the LAMP page, click  **GET STARTED**.
    
5.  On the Agreements page, check the box for  **Terms and agreements**, and click  **AGREE**.
    
6.  On the  **Successfully agreed to terms**  pop up, click  **DEPLOY**.
    
    If this is your first time using Compute Engine, the Compute Engine API must be initialized before you can continue.
    
7.  For  **Zone**, select the deployment zone that Qwiklabs assigned to you.
    
8.  For  **Machine Type**, select  **E2**  as the  **Series**  and  **e2-medium**  as the  **Machine Type**.
    
9.  Leave the remaining settings as their defaults.
    
10.  Accept the Google Cloud Marketplace Terms of Service near the bottom of the page.
    
11.  Click  **Deploy**.
    
12.  If a  **Welcome to Deployment Manager**  message appears, click  **Close**  to dismiss it.
    
    The status of the deployment appears in the console window:  **lampstack-1 is being deployed**. When the deployment of the infrastructure is complete, the status changes to  **lampstack-1 has been deployed**.
    
    After the software is installed, a summary of the details for the instance, including the site address, is displayed.
    
![4](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/36d9dcf7-57a9-4970-9af7-b687b59eb2bb)

- Click  _Check my progress_  to verify the objective.

- Use Cloud Marketplace to deploy a LAMP stack

- Check my progress

## Task 3. Verify your deployment

1.  When the deployment is complete, click the  **Site address**  link in the right pane. (If the website is not responding, wait 30 seconds and try again.) If you see a redirection notice, click on that link to view your new site.
    
    Alternatively, you can click  **Visit the site**  in the  **Get started with LAMP Packaged by Bitnami**  section of the page. A new browser tab displays a congratulations message. This page confirms that, as part of the LAMP stack, the Apache HTTP Server is running.
    
2.  Close the congratulations browser tab.

![5](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/c9e748d5-09a3-43e7-a233-5947a4620a4d)
    
3.  On the Google Cloud Console, under  **Get started with LAMP Packaged by Bitnami**, click  **SSH**.
    
    In a new window, a secure login shell session on your virtual machine appears.
    
4.  In the SSH window, to change the current working directory to  `/opt/bitnami`, execute the following command:
    
      `cd /opt/bitnami`
    
   -  Copied!
    
    - content_copy
    
5.  To copy the  `phpinfo.php`  script from the installation directory to a publicly accessible location under the web server document root, execute the following command:
      
        `sudo sh -c 'echo "<?php phpinfo(); ?>" > apache2/htdocs/phpinfo.php'
   
   - Copied!
    - content_copy 
    - The phpinfo.php script displays your PHP configuration. It is often used to verify a new PHP installation.
    
6.  To close the SSH window, execute the following command:
    
   - exit
   - Copied!
    -  content_copy
    
![6](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/557f142f-b84e-4327-833c-cd5993c7bbd3)

7.  Open a new browser tab.
    
8.  Enter the following URL, and replace  `SITE_ADDRESS`  with the URL in the  **Site address**  field in the right pane of the  **lampstack**  page.
    
    http://SITE_ADDRESS/phpinfo.php
    
    Copied!
    
    content_copy
    
    A summary of the PHP configuration of your server is displayed.
    

**Note:** If you can't see the web page in the browser on your corporate laptop: If possible, exit any corporate VPN/network and try again. Enter the IP address on another device, such as a tablet or even a phone.

9.  Close the  **phpinfo**  tab.





![7](https://github.com/dineshrajdhanapathyDD/kodekloud-Engineer_project/assets/52989362/b20cfc67-fc67-4edb-9ac2-3ccf1f1a28cf)
 

## Congratulations!

In this lab, you deployed a LAMP stack to a Compute Engine instance.