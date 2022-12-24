# Assignment4
## STEP 11: 
Write a docker file for the program modified in STEP 8.
FROM openjdk:8-jdk-alpine
LABEL MAINTAINER = "Chandrashekhar" 
ADD target/demo-0.0.1-SNAPSHOT.jar spring-boot-hibernate-crud-demo.jar
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","spring-boot-hibernate-crud-demo.jar"]
