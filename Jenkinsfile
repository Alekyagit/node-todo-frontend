pipeline {
    agent any
    environment
     {
        VERSION = "${BUILD_NUMBER}"
        PROJECT = 'nodeapp'
        IMAGE = "$PROJECT:$VERSION"
        registry = "alekyadock/nodejs"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
     
    stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/gustavoapolinario/node-todo-frontend'
             
          }
        }
      stage('Build') {
		  steps {
		      sh 'npm install'
	    }
      }
      stage('Test') {
		  steps {
		      sh 'npm test'
	    }
      }
      stage('Image Build'){
           steps{
               script{
                     dockerImage = docker.build registry + ":$BUILD_NUMBER"
                 }
             }
         }
      stage('Deploy our image') {
          steps{
            script {
              docker.withRegistry( '', registryCredential ) {
              dockerImage.push()
            }
        }
            }
        }
}
} 
