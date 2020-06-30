pipeline {
  environment {
    registry = "hemantakumarpati/resultprocessingsystem"
    registryCredential = 'dockeruser'
    dockerImage = ''
 }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/Hemantakumarpati/ResultProcessingSystem.git'
      }
    }
    stage('Build'){
        sh "mvn clean install"
    }
    stage ('Code quality scan') {
      withSonarQubeEnv('SonarQube') {
      sh "${mvnHome}/bin/mvn sonar:sonar -f ResultProcessingSystem/pom.xml"
        }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          //withCredentials([usernamePassword( credentialsId: 'dockeruser', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          //docker.withRegistry('https://registry.hub.docker.com', 'dockeruser') {
          //sh "docker login -u ${USERNAME} -p ${PASSWORD}"
          //dockerImage.push("$BUILD_NUMBER")
          //dockerImage.push("latest")
          sh "/home/hemant_pati/dockerpushresult.sh ${BUILD_NUMBER}"
            //}
       // }
         }
       }
     }
  }
}
