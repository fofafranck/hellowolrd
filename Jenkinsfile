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
          docker.withRegistry('https://registry.hub.docker.com') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
   node() {
       checkout scm
       def a = load('a.groovy')
       echo("${env.BUILD_NUMBER}")
       echo("${a.LOADED_BUILD_NUMBER}")
      }
     }
    }
   }
  }
 }
}
