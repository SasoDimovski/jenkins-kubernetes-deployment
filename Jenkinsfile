pipeline {
  environment {
    dockerimagename = "sasodimovski/react-app"
    dockerImage = ""
	KUBECONFIG = "C:\\Users\\SASHO\\.kube\\config"
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/SasoDimovski/jenkins-kubernetes-deployment.git'
      }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    stage('Pushing Image') {
      environment {
          registryCredential = 'dockerhub-credentials'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploying React.js container to Kubernetes') {
      steps {
          script {
		 bat 'kubectl apply -f D:\\! PROJECTS - APP\\Finki Vezbi\\homework5\\jenkins-deploy\\jenkins-kubernetes-deployment\\deployment.yaml'
		 bat 'kubectl apply -f D:\\! PROJECTS - APP\\Finki Vezbi\\homework5\\jenkins-deploy\\jenkins-kubernetes-deployment\\service.yaml'
        }
      }
    }
  }
}