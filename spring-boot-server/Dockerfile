FROM maven:latest as builder
WORKDIR /app
COPY . .
RUN mvn clean install -Dmaven.test.skip

FROM openjdk:11
COPY --from=builder /app/target/spring-boot-jpa-postgresql-0.0.1-SNAPSHOT.jar /app.jar
EXPOSE 8080/tcp
ENTRYPOINT ["java", "-jar", "/app.jar"]
