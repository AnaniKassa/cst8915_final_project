
# About me 
### Full name: Anani Thierry Kassa
### Student ID: 041140713

# Lab Project: Cloud-Native App for Best Buy

### Details 

Diclaimer: The video is 30min long due to the explanation and troubleshooting!

### 0. Video link: https://youtu.be/xbkF-3dm_rQ

### 1. Updated Architecture Diagram (Draw.io).

![alt text](<Best Buy Architecture.drawio.png>)

### 2. Brief application explanation.

The Best Buy Cloud-Native Application is a modern, microservices-based system designed to demonstrate how large retail platforms can scale reliably in the cloud. The application follows real industry patterns used by enterprise e-commerce systems like Best Buy.
    
The application is composed of five independently developed and deployed microservices, each responsible for a specific business capability:
    
- Store-Front – A customer-facing web application where users can browse products, view item details, and place orders.

- Store-Admin – An internal web dashboard used by employees to manage inventory, products, and monitor orders.
        
- Product-Service – A backend API that handles product data, including creation, updates, and retrieval of product listings.
        
- Order-Service – A backend API responsible for order management, including checkout, order status, and integration with the makeline.
        
- Makeline-Service – A background worker that processes and fulfills orders asynchronously.
        
All services communicate through REST APIs and share a centralized MongoDB database, which is deployed as a StatefulSet to maintain persistent data.
        
To achieve production-grade reliability and scalability, the entire system is deployed on Azure Kubernetes Service (AKS). Configuration is externalized using ConfigMaps and Secrets, containerized using Docker, and automated through GitHub Actions CI/CD pipelines. These pipelines build, test, push images to Docker Hub, and automatically deploy new versions to Kubernetes.
        
This application demonstrates modern cloud-native principles such as microservices, containerization, distributed systems, DevOps automation, and Kubernetes orchestration. It provides a complete end-to-end view of how enterprise e-commerce workloads can be built and deployed in the cloud.

### 3. Deployment instructions.

The deployment of the Best Buy Cloud-Native Application follows a fully cloud-native workflow that includes microservices development, containerization, Kubernetes deployment, and CI/CD automation. The steps below outline the complete process:

1. Create Repositories for All Microservices

Set up five separate GitHub repositories, one for each microservice:

- Store-Front

- Store-Admin

- Product-Service

- Order-Service

- Makeline-Service

Each repository contains the source code and dependencies required for that specific microservice. This separation reflects real industry microservices architecture and enables independent development, scaling, and deployment.

2. Containerize Each Microservice

For every microservice:

- Create a Dockerfile at the root of the repository.

- Build the Docker image for that service.

- Push the images to Docker Hub or another container registry.

This ensures each service can be deployed independently into Kubernetes.

3. Deploy the Application to Kubernetes (AKS)

Create a Kubernetes cluster using Azure Kubernetes Service (AKS) through the Azure Portal.

Next, prepare the Kubernetes Deployment Manifests:

Create a Deployment Files/ directory that contains YAML files for all five microservices.

Include Kubernetes Deployments and Services for:

- Store-Front

- Store-Admin

- Product-Service

- Order-Service

- Makeline-Service

Deploy MongoDB using a StatefulSet to ensure persistent storage. Deploy other components such as RabbitMQ.

Use an apps-all-in-one.yaml file to group all deployments together.

4. Apply the Kubernetes Manifests

From your local machine or Cloud Shell, deploy all resources using:

kubectl apply -f apps-all-in-one.yaml


This will create and launch all microservices, internal communication paths, and supporting infrastructure (MongoDB, RabbitMQ, etc.) inside the AKS cluster.

5. Configure CI/CD Pipelines for Each Microservice

Each microservice repository must include its own GitHub Actions CI/CD pipeline with the following job stages:

- Build – Build the container image.

- Test – Run unit tests or API tests.

- Release – Push the image to Docker Hub.

- Deploy – Automatically update the AKS cluster.

Before enabling the pipelines:

Configure all required Secrets in GitHub (e.g., DOCKER_USERNAME, DOCKER_PASSWORD, AKS_CREDENTIALS, registry URLs, etc.).

Add pipeline environment variables for versioning, namespaces, and deployment file paths.

This ensures fully automated continuous integration and continuous deployment for every microservice in the Best Buy application.


### 4. Links Table: 

- Repository links 
    - https://github.com/AnaniKassa/store-admin-L9
    - https://github.com/AnaniKassa/order-service-L9
    - https://github.com/AnaniKassa/product-service-L9
    - https://github.com/AnaniKassa/makeline-service-L9
    - https://github.com/AnaniKassa/store-front-L9

- Docker Hub image links for all services.
    - kass0112/store-admin-l9:latest
    - kass0112/order-service-l9:latest
    - kass0112/product-service-l9:latest
    - kass0112/makeline-service-l9:latest
    - kass0112/store-front-l9:latest