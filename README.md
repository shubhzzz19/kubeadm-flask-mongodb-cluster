# Kubernetes Microservice Cluster Flask Application With MongoDB  

This is a microservice application built using Flask and deployed on Kubernetes. It is designed to demonstrate how to build and deploy microservices on a Kubernetes cluster.

![K8s Cluster](https://github.com/shubhzzz19/kubeadm-flask-mongodb-cluster/assets/73218792/880988e7-0fcd-422b-8742-ae725ab54375)

## Requirements

Create two AWS Linux EC2 instances 
1. kub-master (t2.medium)
2. kub-worker (t2.medium)

## Installation

To install and run the application on your Kubernetes cluster, follow these steps:

1. Clone this repository to your local machine.
2. Navigate to the project root directory.
3. Create a Kubernetes deployment and service by running the following command:

`kubectl apply -f kubernetes.yaml`

4. Verify that the deployment and service have been created successfully by running the following command:

`kubectl get deployments,services`
