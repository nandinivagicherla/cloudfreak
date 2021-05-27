pipeline {
  agent any
    tools {
      maven 'maven3'
                 jdk 'JDK8'
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
	stage('Example') {
            steps {
                echo "Running ${env.BUILD_NUMBER}"
            }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('9948/petclinic', "./docker")
                 docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
