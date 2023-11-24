pipeline {
    agent any
    options { buildDiscarder(logRotator(numToKeepStr: '1')) }
    tools { 
        maven 'maven3.9.1' 
        jdk 'jdk11' 
    }
    triggers {
        githubPush()
    }
    stages {
       stage('Clone Source') {
            steps {
                cleanWs()
                git 'https://github.com/bhikeshkhute/java-maven-pipeline.git'
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean verify sonar:sonar \
                -Dsonar.projectKey=java-pipeline \
                -Dsonar.projectName='java-pipeline' \
                -Dsonar.host.url=http://localhost:9000 \
                -Dsonar.token=<Get from SonarQube project>"
            
            }
        }
        stage('Deploy'){
            steps{
                deploy adapters: [tomcat8(credentialsId: '<Generate from Jenkins pipeline>', path: '', url: 'http://localhost:8081')], contextPath: '/', onFailure: false, war: '**/*.war'
            }
        }
        stage("Send Notification"){
            steps{
                    sh "node <Nodejs program to send an SMS/Whatsapp notification using Twilio>"
                }
        }
    }
            
}
