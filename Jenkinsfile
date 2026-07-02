pipeline {
  agent any

  environment {
    IMAGE_NAME = "aowens/jenkins-demo-app"
   }

   stages {
     stage('Build Docker Image'){
       steps {
         script {
	   // use docker pipeline plugin to build image
	   dockerImage = docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
	 }
       }
    }
     stage('Push to Docker Hub'){
       steps {
         script {
	   // Use Docker Pipeline plugin to push w credentials
	   docker.withRegistry(https://registry.hub.docker.com', 'dockerhub-credentials') {
	     dockerImage.push("${BUILD_NUMBER}")
	     dockerImage.push("latest")
	   }
	 }
       }
      }
}
     post {
       success {
         echo "Pipeline succeeded! Image pushed: ${IMAGE_NAME}:${BUILD_NUMBER}"
       }
       failure{
         echo "Pipleline failed!"
       }
     }
     }

