
# Dynamic Web Project developed in Java, packaged using Maven, QA using SonarQube, and deployed on Apache Tomcat using Jenkins pipeline along with notifications.
Eclipse IDE used to develop the project and the same was converted into maven and was hosted on the Apache Tomcat server with the help of the Jenkins tool.

As soon as a commit happens on the master branch, webhook will trigger the build to create new package/artifact and the project will be deployed on Apache Tomcat in realtime.

The whole project is carried out on AWS Cloud.

Prerequisite:
1. Java 17 & Apache Tomcat needs to be installed on the server before Jenkins installation.
2. JDK8 & Maven 3.9 need to be installed in the tools section of Jenkins as this project is built using jdk8.
3. "Deploy to Container" plugin also needs to be installed. Note - Not installed by default.

Apache Tomcat configuration:
1. Go to the Tomcat configuration directory, find server.xml, and change the port number from 8443 to your desired port number.
2. Add tomcat-user in the conf/tomcat-users.xml and restart tomcat. You can access the below URL with your new credentials:
```
http://<domain/ip>:8081/manager
```

We have kept the port number of Tomcat as 8081 as per our choice.

The Jenkinsfile is kept on GitHub as the best practice. 

Screenshots:

1. Jenkins Workspace
![pipelinesteps](https://github.com/bhikeshkhute/java-maven-pipeline/assets/35907619/415fb0e3-8749-449d-8c46-59deeecf49f5.png)

---
2. Sonarube Results
![sonarqube](https://github.com/bhikeshkhute/java-maven-pipeline/assets/35907619/12a26bc9-ec93-435b-aa72-97206437ed1c.png)

---
3. Web 
![pipeline](https://user-images.githubusercontent.com/35907619/231505304-4c564fa8-d114-46dd-b260-116be4283f4a.jpg)

---
4. Whatsapp Notification
   
![whatsapp](https://github.com/bhikeshkhute/java-maven-pipeline/assets/35907619/d3546a0d-b1fa-4f4e-a4c5-f6c8c4cc6536.jpg)

Would love to hear feedback on - bhikesh.khute@outlook.com :heart:



