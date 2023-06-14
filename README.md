# Kubernetes Microservice Cluster Flask Application With MongoDB  

This is a microservice application built using Flask and deployed on Kubernetes. It is designed to demonstrate how to build and deploy microservices on a Kubernetes cluster.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Installation

To install and run the application on your Kubernetes cluster, follow these steps:

1. Clone this repository to your local machine.
2. Navigate to the project root directory.
3. Create a Kubernetes deployment and service by running the following command:

`kubectl apply -f kubernetes.yaml`

4. Verify that the deployment and service have been created successfully by running the following command:

`kubectl get deployments,services`
