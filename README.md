![Jenkins_Pipeline](https://github.com/norfluxX/Docker-Java-WebApp-DevOps-Pipeline/assets/35907619/193869bb-66ee-4d2d-a91b-5976b6a3fdaa)
# Dynamic Web Project developed in Java, packaged using Maven, QA using SonarQube, and deployed on Alpine Tomcat Container(~200MB) using Jenkins pipeline along with notifications.
Eclipse IDE used to develop the project and the same was converted into maven and was hosted on the Alpine Tomcat Container with the help of the Jenkins tool.

As soon as a commit happens on the master branch, webhook will trigger the build to create new package/artifact and the project will be deployed on Apache Tomcat in realtime.

The whole project is carried out on AWS Cloud.

Prerequisite:
1. Java 17 & Apache Tomcat needs to be installed on the server before Jenkins installation.
2. JDK8 & Maven 3.9 need to be installed in the tools section of Jenkins as this project is built using jdk8.
3. "Deploy to Container" plugin also needs to be installed. Note - Not installed by default.

Apache Tomcat configuration done in the docker file itself.
```
http://<container-ip>:8080/manager
```

We have kept the port number of Tomcat as 8080 as per our choice.

The Jenkinsfile is kept on GitHub as the best practice. 

Screenshots:

1. Jenkins Workspace
![Jenkins_Pipeline](https://github.com/norfluxX/Docker-Java-WebApp-DevOps-Pipeline/assets/35907619/2a19ff18-25d8-4200-a744-728bae95ea0a)

---
2. Web 
![Web](https://github.com/norfluxX/Docker-Java-WebApp-DevOps-Pipeline/assets/35907619/5de9ff05-d48c-4ac8-b4ea-594433319856)

---
4. Whatsapp Notification

Would love to hear feedback on - bhikesh.khute@outlook.com :heart:



