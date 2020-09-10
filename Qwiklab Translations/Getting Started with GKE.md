# Lab Name: Getting started with GKE.

## Objectives:

In this lab, you learn how to perform the following tasks:


* Provision a **Kubernetes** cluster using **Kubernetes Engine**.


* Deploy and manage **Docker containers** using **Kubectl**.


## Task 1:  Confirm that needed APIs are enabled

## Steps:

1. Confirm that the needed APIs are enabled.

   `gcloud services list`

2. Scroll down in the list of enabled APIs, and confirm that both of these APIs 

are enabled:
 
* Kubernetes Engine API
* Container Registry API

3. If either API is missing, enable them by running the following commands:
  
 * For Kubernetes Engine API

   `gcloud services enable container.googleapis.com` 

 * For Container Registry API


    `gcloud services enable containerregistry.googleapis.com`


## Task 2: Start a Kubernetes Engine cluster 

## Steps:

1. Create a Kubernetes cluster managed by Kubernetes Engine named **webfrontend** and running on 2 nodes in zone **us-central1-a**: 

     `gcloud container clusters create webfrontend --zone us-central1-a --num-nodes 2`


2. After the cluster is created, check your installed version of Kubernetes using the _kubectl version_ command:
   
     `kubectl version`
  
  
   > The _gcloud container clusters_ create command automatically authenticated _kubectl_ for you.


## Task 3: Run and deploy a container 

## Steps:

1. Create a deployment consisting of a single pod containing the nginx 

container:

   `kubectl create deploy nginx --image=nginx:1.17.10`

2. View and confirm the pod running the nginx container:

   `kubectl get pods`

3. Expose the nginx container to the Internet by creating an external load balancer:

    `kubectl expose deployment nginx --port 80 --type LoadBalancer`

4. View and confirm the Service(Load Balancer):

   `kubectl get services`

5. Scale up the number of pods running on the service:

   `kubectl scale deployment nginx --replicas 3`

6. Confirm that Kubernetes has updated the number of pods:

   `kubectl get pods`

7. Confirm that your external IP address has not changed:

   `kubectl get services`


## Congratulations!

You configured a Kubernetes cluster in Kubernetes Engine. You populated the 

cluster with several pods containing an application, exposed the application, 

and scaled the application.



