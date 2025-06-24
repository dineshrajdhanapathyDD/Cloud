<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy Backend with Kubernetes

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks4)

**Author:** Dineshraj Dhanapathy  
**Email:** dineshrajdhanapathy@gmail.com

---

## Deploy Backend with Kubernetes

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-compute-eks4_6cfb382f2)

---

## Introducing Today's Project!

In this project, I will set up the backend of an app for deployment because deploying the backend is essential to making the application accessible and functional. I will install kubectl to manage and interact with the Kubernetes cluster. Then, I’ll deploy the backend on the Kubernetes cluster to ensure it runs reliably. Finally, as a secret mission, I will track the Kubernetes deployment using EKS to monitor its health and performance.

### Tools and concepts

I used Kubernetes, ECR, kubectl, and eksctl to deploy and manage my backend application on a scalable cluster. Key concepts include using manifests to define desired states for Deployments and Services, containerizing the app with Docker for consistent environments, and pushing images to ECR for easy access by Kubernetes. These tools and concepts enabled automated, reliable deployment and seamless scaling of my backend in a cloud-native way.

### Project reflection

This project took me approximately 1 hour to complete. The most challenging part was configuring the Kubernetes manifests correctly to ensure smooth deployment and service exposure. My favourite part was seeing the backend successfully deployed and accessible through the Kubernetes Service, which made all the setup feel rewarding. Overall, it was a great hands-on experience with container orchestration and cloud-native deployment.

---

## Project Set Up

### Kubernetes cluster

To set up today's project, I launched a Kubernetes cluster. The cluster's role in this deployment is to provide a scalable, managed environment to run and orchestrate containerized backend applications. I used eksctl to create the cluster with specified node groups, enabling automatic management of nodes and resources. This setup ensures my app runs reliably with high availability, load balancing, and easy scaling across multiple containers.

### Backend code

I retrieved backend code by cloning the GitHub repository using Git commands. Pulling code is essential to this deployment because it gives me the exact, up-to-date version of the backend application, including all necessary files like the app code, Dockerfile, and dependencies. This ensures that I build and deploy the correct version of the app, allowing Kubernetes to run the backend smoothly and consistently across environments.

### Container image

Once I cloned the backend code, I built a container image because it packages the app and all its dependencies into a single, portable unit. Without an image, it would be difficult for Kubernetes to deploy the backend consistently across different nodes and environments. The container image ensures the app runs reliably, making scaling and updating easier within the Kubernetes cluster.

I also pushed the container image to a container registry, which is Amazon ECR, because it provides a secure and scalable way to store and retrieve container images. ECR facilitates scaling for my deployment because it integrates seamlessly with EKS, allowing Kubernetes to pull images on demand and deploy multiple replicas efficiently without needing manual image transfers.

---

## Manifest files

Kubernetes manifests are configuration files written in YAML or JSON that define the desired state of Kubernetes resources like Pods, Deployments, and Services. Manifests are helpful because they let you describe how your application should run, including container images, replicas, ports, and more. Kubernetes reads these manifests to automatically set up and manage your app, ensuring consistency, reliability, and easier deployment across environments.

A Deployment manifest manages how an application is deployed and maintained on a Kubernetes cluster. It defines the number of replicas, the container image to use, and the desired app state. The container image URL in my Deployment manifest tells Kubernetes which image to pull and run in each Pod. This ensures that every replica uses the same version of the app, making deployments consistent, scalable, and fault-tolerant.

A Service resource exposes an application running in a set of Pods so it can be accessed from outside the Kubernetes cluster. My Service manifest sets up a NodePort Service that routes traffic to Pods labeled app: nextwork-flask-backend and listens on port 8080. It forwards traffic from that port to the same port on the target Pods. This setup allows users to access the backend using the node's IP address and the assigned NodePort, making it ideal for learning and testing.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-compute-eks4_b01876554)

---

## Backend Deployment!

To deploy my backend application, I used kubectl apply to apply the Deployment and Service manifests I created. These manifests gave Kubernetes the instructions it needed to create pods running my backend container and expose them to traffic using a NodePort Service. This step made my app accessible from outside the cluster. I also verified the deployment using kubectl get pods and kubectl get svc to confirm everything was running properly.

### kubectl

kubectl is the command-line tool used to interact with Kubernetes resources such as Deployments and Services. I need this tool to apply manifest files, manage workloads, and monitor the health of my application once the cluster is running. I can't use eksctl for the job because eksctl is mainly for setting up and managing EKS clusters—not for deploying applications or interacting with individual Kubernetes resources like pods and services.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-compute-eks4_6cfb382f2)

---

## Verifying Deployment

My extension for this project is to use the EKS console to visually inspect and verify the resources running in my Kubernetes cluster, such as Pods and Services. I had to set up IAM access policies because the console needs permission to display and interact with my cluster resources securely. I set up access by attaching the necessary IAM policies to my user or role and enabling cluster access using the aws-auth ConfigMap to map IAM identities to Kubernetes roles.

Once I gained access to my cluster's nodes, I discovered pods running inside each node. Pods are the smallest deployable units in Kubernetes that bundle one or more containers together to work as a unit. Containers in a pod share the same network space and storage, enabling them to communicate easily and share data efficiently. Pods ensure that containers are co-located and managed together within the Kubernetes cluster environment.

The EKS console shows you the events for each pod, where I could see important steps like the pod being assigned an internal IP, the container image being pulled from Amazon ECR, the image successfully downloaded, and the container created and started. This validated that my backend container was deployed correctly and is now running inside the Kubernetes cluster. It confirmed that Kubernetes successfully scheduled the pod, fetched the right image, and launched the container, meaning my backend is operational and ready to handle requests within the cluster network.

![Image](http://learn.nextwork.org/positive_purple_innocent_lemon/uploads/aws-compute-eks4_3b391f873)

---

---
