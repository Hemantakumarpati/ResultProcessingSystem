node{

   def tomcatWeb = 'C:\\Users\\heman\\Tomcat\\apache-tomcat-9.0.33-windows-x64\\apache-tomcat-9.0.33\\webapps'
   def tomcatBin = 'C:\\Users\\heman\\Tomcat\\apache-tomcat-9.0.33-windows-x64\\apache-tomcat-9.0.33\\bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/Hemantakumarpati/ResultProcessingSystem.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      //def mvnHome =  tool name: 'maven-3', type: 'maven'   
      //bat "${mvnHome}\\bin\\mvn package"
      bat "mvn package"
      }
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.bat"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
     bat "copy target\\ResultProcessingSystem.war \"${tomcatWeb}"
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
         //bat "${tomcatBin}\\startup.bat"
         bat "C:\\Users\\heman\\Tomcat\\apache-tomcat-9.0.33-windows-x64\\apache-tomcat-9.0.33\\bin\\startup.bat"
         sleep(time:100,unit:"SECONDS")
   }
}


/*pipeline {
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
    /*stage('Deploy Image') {
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
}*/
