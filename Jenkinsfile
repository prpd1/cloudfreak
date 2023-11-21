pipeline {
  agent any
    tools {
      maven 'mvn'
                 jdk 'JAVA_HOME'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('qwerty703/hello', "./docker/")
                 docker.withRegistry('https://registry.hub.docker.com', 'qwerty703') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
