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
- Step 2: deploy the postgres database under Kubernetes-manifests/postgres, use kubectl apply -f to deploy both the statefulset and service files respectively.
- Step 3: deploy the backend service under Kubernetes-manifests/backend, use kubectl apply -f command to deploy both the deployment and service files respectively
- Step 4: deploy the frontend service under Kubernetes-manifests/frontend, use kubectl apply -f command to deploy both the deployment and service files respectively.
 
### 2- Manually using Helm
- Step 1: deploy the secret resource under Kubernetes-manifests/shared-resources using kubectl apply -f 
- Step 2: deploy the postgres database under Kubernetes-manifests/postgres, use kubectl apply -f to deploy both the statefulset and service files respectively.
- Step 3: deploy the backend and frontend services using the helm chart under Helm-chart folder, use helm upgrade --install command and it will install all the required resources

### 3- Automated using Jenkins
- Step 1: deploy the secret resource under Kubernetes-manifests/shared-resources using kubectl apply -f 
- Step 2: deploy the postgres database under Kubernetes-manifests/postgres, use kubectl apply -f to deploy both the statefulset and service files respectively.
- Step 3: Use the Jenkinsfile as the pipeline script for your jenkins pipeline to deploy the frontend and backend services

      
### Notes
- In any of the above deployment methods, the app (frontend) should be exposed on a local port (nodeport) 30163 on all of the kubernetes cluster nodes. You should be able to access the app on http://{node-ip}:30163
- You can build the images for the frontend and backend using the Dockerfile under each of their source folder. The dockerfiles use a multistage build where the first stage builds the code and the second uses the output artifact (dist folder or jar file) to build the final image. This makes it more easy instead of setting up a dedicated environment for building the code.
- The reason we deploy the postgres manually in all the methods is that databases are typically not part of automated CI/CD or helm deployments. The frequent changes usually happen on the app microservices (code) which requires frequent deployments.
- The postgres statefulset manifest doesn't contain a persistent volume for storing data, so it will use an ephemeral emtpydir where data will be wiped out if the pod is deleted. However, it is often a requirement for stateful workloads like DBs to use a persistent storage.
- It is recommended to use an ingress to expose the app rather than a nodeport.
- The secret manifest contains env variables used for initializing the postgres database and for setting the backend connection string to the DB, so it must be deployed first before other resources.


![image](https://github.com/Amr-tmorot/Tutorial-app/assets/88274242/8f964969-67ab-4df6-8ba7-e72579cd3d97)


  



