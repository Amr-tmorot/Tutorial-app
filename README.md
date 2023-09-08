# Spring Boot + Angular 15 + PostgreSQL + Kubernetes CRUD example

Full-stack Angular 15 + Spring Boot + PostgreSQL CRUD Tutorial Application in that:
- Each Tutorial has id, title, description, published status.
- We can create, retrieve, update, delete Tutorials.
- We can also find Tutorials by title.

![spring-boot-angular-15-postgresql-example-crud.png](spring-boot-angular-15-postgresql-example-crud.png)

For more detail, please visit:
> [Spring Boot + Angular 15 + PostgreSQL: CRUD example](https://www.bezkoder.com/spring-boot-angular-15-postgresql/)

Run both Back-end & Front-end in one place:
> [Integrate Angular with Spring Boot Rest API](https://www.bezkoder.com/integrate-angular-spring-boot/)

More Practice:
> [Angular + Spring Boot: File upload example](https://www.bezkoder.com/angular-15-spring-boot-file-upload/)

> [Angular + Spring Boot: JWT Authentication and Authorization example](https://www.bezkoder.com/angular-15-spring-boot-jwt-auth/)

## Run Spring Boot application
```
mvn spring-boot:run
```
The Spring Boot Server will export API at port `8081`.

## Run Angular Client
```
npm install
ng serve --port 8081
```

## Deployment
Pre-requisite:
- Create Azure Resources
    - Kubernetes with AGIC
    - Application Gateway
    - Azure Database for PostgreSQL (single or flexible server)
- Change values in deployment.yml
    - Replace value of \<certificate-name> to the name of the certificate added in Listener TLS certificates tab of Application Gateway resource.
    - Replace value of \<host-name> to your desired host name.
    - Replace values of \<username>, \<password>, \<postgres-host> to the username, password and host of Azure Database for PostgreSQL resource.
    - Replace value of \<repository>/\<springboot-image>:\<tag> to your chosen repository, springboot image and tag.
    - Replace value of \<repository>/\<angular-image>:\<tag> to your chosen repository, angular image and tag.
      
### Create and push Docker images (Change directory to where the Dockerfile is placed.)
```
docker build -t <repository>/<image-name>:<tag> .
docker push <repository>/<image-name>:<tag>
```

### Create pods, service and ingress resources in Kubernetes (Change directory to where the deployment.yml is placed.)
```
kubectl apply -f deployment.yml
```
