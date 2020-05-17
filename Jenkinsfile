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
        git 'https://github.com/Hemantakumarpati/OnlineBookStore.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    /*stage('Test Image' ) {
                agent {
                docker { image 'hemantakumarpati/onlinebookstore:$BUILD_NUMBER' }
            }
            steps {
                sh 'docker --version'
            }
        }*/
    stage('Deploy Image') {
      steps{
        script {
          //withCredentials([usernamePassword( credentialsId: 'dockeruser', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          //docker.withRegistry('https://registry.hub.docker.com', 'dockeruser') {
          //sh "docker login -u ${USERNAME} -p ${PASSWORD}"
          //dockerImage.push("$BUILD_NUMBER")
          //dockerImage.push("latest")
          sh "/home/hemant_pati/dockerpush.sh ${BUILD_NUMBER}"
            //}
       // }
      }
    }
  }
  }
}
