pipeline{
    agent any
     tools {
        maven 'Maven-3.6.1'
    }
    
    stages{
        stage("Git Checkout"){
            steps{
                git 'https://github.com/ramgub/jenkins-file.git'
            }
        }
        stage("Maven Build"){
            steps{
                script{
                   withSonarQubeEnv(credentialsId: 'sonar') {
                   sh "mvn clean sonar:sonar package"
                   }     
                }
            }
        }
        stage('Upload War To Nexus'){
            steps{
                  nexusArtifactUploader artifacts: [
                       [
                            artifactId: 'myweb', 
                            classifier: '', 
                            file: "target/myweb-8.2.0.war", 
                            type: 'war'
                       ]
                  ], 
                  credentialsId: 'nexus3', 
                  groupId: 'in.javahome', 
                  nexusUrl: '18.218.173.211:8081', 
                  nexusVersion: 'nexus3', 
                  protocol: 'http', 
                  repository: 'tomcat-release', 
                  version: '8.2.0'  
              }
            }
       /* stage('Build Docker Image'){
            steps{
                 sh 'docker build -t raghunadh181/spring-boot-mongo .'
                 sh 'docker build -t tomcat:${BUILD_NUMBER} .'
                 sh 'docker run -itd --name srini26 -p 3900:8080 tomcat:${BUILD_NUMBER}'
             }
         }
        stage('Push Docker Image'){
             steps{
                  withCredentials([string(credentialsId: 'DOCKER_HUB_CREDENTIALS', variable: 'DOCKER_HUB_CREDENTIALS')]) {
                      sh "docker login -u raghunadh181 -p ${DOCKER_HUB_CREDENTIALS}"
            }
            sh 'docker push raghunadh181/spring-boot-mongo'
        }
      } */
        
        
    }
}
