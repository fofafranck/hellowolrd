pipeline {
  agent any
  tools {
     maven 'M2_HOME'
  }
  environment {
    registry = "fofafranck/jenkinspipeline"
    registryCredential = 'DockerID'
  }
  stages {
    stage('Build'){
      steps {
        sh 'mvn clean'
        sh 'mvn install'
        sh 'mvn package'
      }
    }
  stage('test'){
      steps {
        sh 'mvn test'
      }  
   }
  stage('deploy'){
      steps {
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
   }
  stage('Push image') {
    steps {
      script {
         docker.push registry + ":$BUILD_NUMBER"  
       }
    }
  }
 }
}
