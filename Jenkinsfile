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
    stage('Test OnlineBookStore' ) {
                agent {
                docker { image 'hemantakumarpati/resultprocessingsystem:$BUILD_NUMBER' }
            }
            steps {
                sh 'docker --version'
            }
        }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
