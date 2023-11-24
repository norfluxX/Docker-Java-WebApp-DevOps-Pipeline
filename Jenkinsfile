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
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
    stages {
        stage('Clone Source') {
            steps {
                cleanWs()
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/norfluxX/Docker-Java-WebApp-DevOps-Pipeline.git'
                  }
                            }   
        stage('Build & QA'){
            steps {
                withSonarQubeEnv('SonarQube') {
                sh "mvn clean verify sonar:sonar \
                -Dsonar.projectKey=java-pipeline \
                -Dsonar.projectName='java-pipeline' \
                -Dsonar.host.url=http://localhost:9000 \
                -Dsonar.token=sqp_3afa86ea04df49c64459b41af426cc280730c89f"
                }
            }
        }
        stage('Copy artifact'){
            steps{
                sh 'mv target/*.war .'
            }
        }
        stage('DockerHub Login'){
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    def build_id = sh( script: 'wget -qO- http://localhost:8080/job/Java_Docker/lastSuccessfulBuild/buildNumber', returnStdout: true );
                }
                sh "echo ${build_id}"
                sh """ sed -i '1s/FROM bhikeshk7:.*/FROM bhikeshk7:${build_id}/' Dockerfile """ 
                sh 'docker build -t bhikeshk7/tomcatalpine:${BUILD_NUMBER} -f Dockerfile .'  
            }
        }
        stage('Push Image to DockerHub'){
            steps{
                sh 'docker push bhikeshk7/tomcatalpine:${BUILD_NUMBER}'
            }
        }
        stage('Deploy to the container'){
            steps{
             sh 'docker ps | grep bhikesh | awk "{print $1}" | xargs docker stop || true '
             sh 'docker run -dp 8888:8080 bhikeshk7/tomcatalpine:${BUILD_NUMBER}'  
            }
        }  
        stage("Send Notification"){
            steps{
                    sh "node /home/ubuntu/Desktop/twilio/wa.js"
                }
        }
    }
}
