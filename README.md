# Assignment4
## STEP 11: 
Write a docker file for the program modified in STEP 8.
FROM openjdk:8-jdk-alpine
LABEL MAINTAINER = "AbhishekKamath" 
ADD target/demo-0.0.1-SNAPSHOT.jar spring-boot-hibernate-crud-demo.jar
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","spring-boot-hibernate-crud-demo.jar"]

## STEP 12: 
Create a docker image and PUSH the image to a Cloud Artifact registry on GCP.
mvn clean package
sudo docker build -t spring-boot-hibernate-crud-demo:latest .
sudo docker run -p 8081:8080 spring-boot-hibernate-crud-demo:latest

## docker images
gcloud docker -- push asia.gcr.io/dba-datalake-prod/backend/curd:latest

curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo tee /usr/share/keyrings/cloud.google.gpg
sudo apt-get update && sudo apt-get install google-cloud-cli
 sudo apt-get update
 sudo apt-get install apt-transport-https ca-certificates gnupg
cd /etc/apt/sources.list.d
sudo apt-get install apt-transport-https ca-certificates gnupg
sudo apt-get update && sudo apt-get install google-cloud-cli
gcloud init
gcloud docker -- push asia.gcr.io/dba-datalake-prod/backend/curd:latest
docker tag spring-boot-hibernate-crud-demo:latest asia.gcr.io/dba-datalake-prod/backend/curd:abhishek
docker images
gcloud docker -- push asia.gcr.io/dba-datalake-prod/backend/curd:abhishek

## STEP 13: Create a kubernetes deployment file to deploy the application to google kubernetes engine (GKE).
![image](https://user-images.githubusercontent.com/118809942/209423006-63e70ac1-864b-436e-b06e-d57c556899b2.png)


## STEP 14: Write Unit test cases for the API created
package com.howtodoinjava.demo;
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.MethodOrderer;
import org.junit.jupiter.api.Order;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.TestMethodOrder;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.TestEntityManager;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.test.annotation.Rollback;
import com.howtodoinjava.demo.model.EmployeeEntity;
import com.howtodoinjava.demo.repository.EmployeeRepository;
import javax.sql.DataSource;
import java.util.List;
import java.util.Optional;
@DataJpaTest
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
public class ProductTest {
@Autowired
private EmployeeRepository employeeRepository;
@Test
@Order(1)
@Rollback(value = false)
public void saveEmployeeTest(){

EmployeeEntity employee = EmployeeEntity.builder()
.firstName(&quot;Abhishek&quot;)
.lastName(&quot;Kamath&quot;)
.email(&quot;kamath.h.abhishek@gmail.com&quot;)
.build();
employeeRepository.save(employee);
Assertions.assertThat(employee.getId()).isGreaterThan(0);
}
@Test
@Order(2)
public void getEmployeeTest(){
EmployeeEntity employee = employeeRepository.findById(1L).get();
Assertions.assertThat(employee.getId()).isEqualTo(1L);
}
@Test
@Order(3)
public void getListOfEmployeesTest(){
List&lt;EmployeeEntity&gt; employees = employeeRepository.findAll();
Assertions.assertThat(employees.size()).isGreaterThan(0);
}
@Test
@Order(4)
@Rollback(value = false)
public void updateEmployeeTest(){
EmployeeEntity employee = employeeRepository.findById(1L).get();
employee.setEmail(&quot;kamath.h.abhishek@gmail.com&quot;);
EmployeeEntity employeeUpdated = employeeRepository.save(employee);

Assertions.assertThat(employeeUpdated.getEmail()).isEqualTo(&quot;demon@gmail.com&quot;);
}
}

## STEP 15: Measure the code coverage of the API using SonarLint.
![image](https://user-images.githubusercontent.com/118809942/209422949-c78a04c7-a9b8-4f2a-8ee2-68955bb22aba.png)
