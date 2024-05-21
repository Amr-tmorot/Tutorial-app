# 3-Tier Tutorial Application with Spring Boot + Angular + PostgreSQL on Kubernetes

- Each Tutorial has id, title, description, published status.
- We can create, retrieve, update, delete Tutorials.
- We can also find Tutorials by title.

![spring-boot-angular-15-postgresql-example-crud.png](spring-boot-angular-15-postgresql-example-crud.png)

## Application Architecture

The application consists of a frontend, backend, and a database :

![image](https://github.com/Amr-tmorot/Tutorial-app/assets/88274242/e373387e-e17e-47cd-ac7e-8f02537b5b28)

- The frontend is implemented using angular, if you're using this project locally you can start the local angular web server using ng serve -- {port_number} and access the frontend on http://localhost:{port_number}
- The backend is implemented using spring boot, and listens for API calls on the default port of 8080
- The database used is PostgreSQL with the default port of 5432

## How this Repo is Organized

This project repo consists of the following:
- Helm-chart: this is the folder containing the helm chart for deploying the application. It mainly deploys the frontend and backend services.
- Kubernetes-manifests: this folder contains raw k8s YAML manifest files for each service. It contains 4 subfolders for the frontend, backend, database, and shared resources like secrets.
- angular-15-client : this folder contains the source for the angular frontend and the Dockerfile for building the image.
- spring-boot-server: this folder contains the source for the spring boot backend and the Dockerfile for building the image.
- Jenkinsfile: This is the Jenkinsfile used for CI/CD pipeline deployment using jenkins
- README.md file 


## Deployment Steps

This tutorial app can be deployed to Kubernetes in 3 different ways:
### 1- Manually using only the Kubernetes manifests:
- Step 1: deploy the secret resource under Kubernetes-manifests/shared-resources using kubectl apply -f 
- Step 2: deploy the postgres database under Kubernetes-manifests/postgres, use kubectl apply -f to deploy both the deployment and service files respectively.
- Step 3: deploy the backend service under Kubernetes-manifests/backend, use kubectl apply -f to deploy both the deployment and service files respectively
- Step 4: deploy the frontend service under Kubernetes-manifests/frontend, use kubectl apply -f to deploy both the deployment and service files respectively.

The app (frontend) should be exposed on a local port (nodeport) on all of the kubernetes cluster nodes 
### 2- Manually using Helm
### 3- Automated using Jenkins


      
## Notes



